# Autologin greeter for lightdm

I occasionally need autologin for X. I once wrote [nodm](https://github.com/spanezz/nodm)
for it, but I am not developing it anymore.

I have instead written a minimal autologin greeter for [lightdm](https://freedesktop.org/wiki/Software/LightDM/)
that has the same autologin behaviour as nodm, but being based on lightdm it
stays on top of modern display manager requirements.

Some instructions for setting a custom greeter in lightdm can be found
[here](https://wiki.ubuntu.com/LightDM#Changing_the_Greeter)

The difference between lightdm's built-in autologin and this greeter, are the
behaviour in case of 0-seconds autologin delay: when lightdm autologs in with
no delay, upon logout it will show the login window again. The intent is that
if the default user logged out, they probably intend to log in again as a
different user.

In my case, managing a kiosk-like setup, if the X session quits then the
desired behaviour is to just start it again.

Lightdm with an autologin timeout of 1 or more seconds would work as I need it,
but one sees the login dialog window appear and disappear on screen at each
system startup. While it is functional, on a kiosk setup it looks estetically
unprofessional to my taste.

With this greeter, the X session starts right away, and is restarted if it
quits, without any flicker of a login dialog box.

If one is not setting up a kiosk-like setup, it's very likely that the default
autologin behaviour of lightdm is the way to go, and that this greeter is not
needed.

### Dependencies

|                     | arch           | ubuntu           | fedora          | suse                   |
| ------------------- | -------------- | ---------------- | --------------- | ---------------------- |
| **lightdm**         | lightdm        | lightdm          | lightdm         | lightdm                |
| **lightdm-gobject** | lightdm        | gir1.2-lightdm-1 | lightdm-gobject | liblightdm-gobject-1-0 |
| **PyGObject**       | python-gobject | python-gobject   | pygobject3      | python3-gobject        |

### Installation

| Distribution | Installation command                                                 |
| ------------ | -------------------------------------------------------------------- |
| **arch**     | `sudo pacman -S lightdm python-gobject`                              |
| **ubuntu**   | `sudo apt-get install lightdm gir1.2-lightdm-1 python-gobject`       |
| **fedora**   | `sudo dnf install lightdm lightdm-gobject pygobject3`                |
| **suse**     | `sudo zypper install lightdm liblightdm-gobject-1-0 python3-gobject` |

1. Install the dependencies.
2. Clone/download the project.
3. Copy the files in `bin/` and `share/` to `/usr`.
4. Ensure no other greeter is configured and reboot.

You'll now be using the autologin greeter!
