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

