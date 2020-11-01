# Summary #

This project builds a container image for running TP-Link's Omada AP controller software in a Linux container with systemd-nspawn.

# Building #

To build the container image, run:

``` shell
$ mkosi -if
```

# Testing #

To boot the image to test it, run:

``` shell
$ mkosi boot
```

By default, you won't be able to log into the booted image.
If you need to log in to poke around and debug, run:

``` shell
$ mkosi shell
```

to get a shell as root in the image.
Then remove or set the root password with:


``` shell
$ passwd -d root # removes root password
# or
$ passwd # sets a password
$ exit # closes shell
```

Then boot the image again, and log in as root and hack away.

# Installing #

To install the image, run:

``` shell
$ cp omada.raw /var/lib/machines/
$ cp omada.nspawn /etc/systemd/nspawn/
$ machinectl enable omada
$ machinectl start omada
```

## Known Limitations ##

For some reason `machinectl shell omada` doesn't seem to work with Debain 9 (used for the container's OS).
However, as a work around, `machinectl shell omada /bin/bash` does work.

# Version Numbering #

This project aims to follow the debian package numbering policy. This means
that tags follow the form UpstreamVersionNumber-PackageRevision. So a tag of
1.2.3-4 would be the 4th revision of this project containing Omada Controller
version 1.2.3. The revision level is reset to 1 each time the packaged Omada
Controller version is updated in this project. See the debain version pollicy
for further info (try `man deb-version` on debian based distros).

# Upgrading from a Previous Version #

If upgrading from a previous version of the controller, TP-Link has an [Upgrade
Guide] which you should read first.

[Upgrade Guide]: https://www.tp-link.com/omada-sdn/controller-upgrade/
