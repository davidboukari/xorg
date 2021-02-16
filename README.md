# xorg

Configure xorg: http://doc.ubuntu-fr.org/xorg
```
sudo X -configure
$ sudo cp ~/xorg.conf.new /etc/X11/xorg.conf
$ sudo cat /etc/X11/default-display-manager
/usr/sbin/gdm3
$ sudo systemctl restart gdm3.service
```

## VNC
* https://www.teknotut.com/en/install-vnc-server-with-gnome-display-on-ubuntu-18-04/

## Fluxbox session with vnc
```
cat .vnc/xstartup
#!/bin/sh
#
# fluxbox startup-script:
#
# Lines starting with a '#' are ignored.

# Change your keymap:
xmodmap "/home/bad/.Xmodmap"

# Applications you want to run with fluxbox.
# MAKE SURE THAT APPS THAT KEEP RUNNING HAVE AN ''&'' AT THE END.
#
# unclutter -idle 2 &
# wmnd &
# wmsmixer -w &
# idesk &
#
# Debian-local change:
#   - fbautostart has been added with a quick hack to check to see if it
#     exists. If it does, we'll start it up by default.
which fbautostart > /dev/null
if [ $? -eq 0 ]; then
    fbautostart
fi

# And last but not least we start fluxbox.
# Because it is the last app you have to run it with ''exec'' before it.

/usr/bin/terminator &
/usr/bin/gnome-panel &
#/usr/bin/gnome-power-manager &
/usr/bin/indicator-cpufreq &
/usr/bin/nm-applet &
```
