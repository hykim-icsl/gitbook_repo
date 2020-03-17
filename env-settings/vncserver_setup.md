# Tightvnc server setup

```bash
sudo add-apt-repository universe
sudo apt-get update
```

install Xfce desktop:

```bash
sudo apt-get install xfce4 xfce4-session
```

install tightvncserver package:

```bash
sudo apt-get install tightvncserver
```

start a new VNC session by using the tightvncserver

```bash
tightvncserver
```

stop Ubuntu VNC server :

```bash
tightvncserver -kill :[session number]
```

open ~/.vnc/xstartup and make sure it is similar to following configuration:

```bash
#!/bin/sh

unset SESSION_MANAGER
xrdb $HOME/.Xresources
xsetroot -solid grey
[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
startxfce4 &
```

Save the config file and start a new VNC session:

```bash
tightvncserver :1 -geometry 1366x768 -depth 24
```


ref : https://www.ubuntu18.com/install-vnc-server-ubuntu-18/