# xorg

Configure xorg: http://doc.ubuntu-fr.org/xorg
```
sudo X -configure
$ sudo cp ~/xorg.conf.new /etc/X11/xorg.conf
$ sudo cat /etc/X11/default-display-manager
/usr/sbin/gdm3
$ sudo systemctl restart gdm3.service
```
