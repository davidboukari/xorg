# xorg

## Ubuntu
```
sudo apt-get install xorg
```

## Get the display
```
[root@control-plane ~]# xauth list $DISPLAY
control-plane.minikube.internal/unix:11  MIT-MAGIC-COOKIE-1  5b761113eb13baa6694b754a354b84b4
[root@control-plane ~]# echo $DISPLAY
localhost:11.0
```

## Centos 7
```
yum grouplist 

yum groupinstall MATE
```

## Install the group GUI Centos 8
* https://www.itzgeek.com/how-tos/linux/centos-how-tos/how-to-install-gnome-gui-on-rhel-8.html
```
dnf groupinstall "Server with GUI" -y

systemctl set-default graphical

dnf install tigervnc-server.x86_64 tigervnc.x86_64

reboot
```

## X11 forwarding
```
yum install  xorg-x11-server-Xorg xorg-x11-xauth xorg-x11-apps -y

vim /etc/ssh/sshd_config
X11Forwarding yes

systemctl restart sshd
```

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
* https://github.com/davidboukari/xorg-x11-vnc

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
* gnome vnc startup
```
$ cat $HOME/.vnc/xstartup |egrep -v '#'|grep -v "^$"
[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
vncconfig -iconic &
x-terminal-emulator -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" &
x-window-manager &
exec /usr/bin/mate-session

$ systemctl get-default
$ systemctl set-default graphical.target
```
