# Monitoring PC through Ethernet / Wifi with VNC viewer

Identify ethernet / wifi adapter

```bash
ifconfig
sudo apt install -y nano
sudo nano /etc/network/interfaces
```
Delete all text and then copy the following code:

```bash
auto lo
iface lo inet loopback
auto eth0 //eth0 = Refers to ethernet adapter 
iface eth0 inet static
address 192.168.123.23 // 23 is free to choose IP
netmask 255.255.255.0 //default
```
Restart network interface
```bash
sudo systemctl networking restart
```
# Enabling Desktop Sharing
Note: Desktop Sharing in Fresh installed Jetpack on Xavier NX is Crash, we need to solve that by following this [Link](http://vrzin.blogspot.com/2019/09/fix-desktop-sharing-setting-on-l4t.html)

1. Open the Activities overview and start typing Desktop Sharing.
2. After launching the utility, you can easily enable VNC server in Ubuntu by checking the boxes that say:
   - In Sharing section
     - Allow other users to view your desktop
     - Allow other users to control your desktop (Optional)
   - In Security section
     - Disable You must confirm each access to this machine
     - Enable require the user to enter this password, to secure login access.

# Enabling Remote Access permission
1. Install dconf editor
```bash
sudo apt install -y dconf-editor
```
2. Open the Activities Overview and start typing dconf editor.
   - When it opens, navigate to org -> gnome -> desktop -> remote-access, and uncheck the value of “require-encryption” in right.
3. Reboot

# Dummy video driver for ubuntu
For set screen resolution without monitor in vnc viewer run the following command in the terminal (Ctrl+Alt+T) one at a time:
```bash
sudo apt-get install xserver-xorg-core
sudo apt-get install xserver-xorg-video-dummy
sudo apt-get install --reinstall xserver-xorg-input-all
sudo nano /usr/share/X11/xorg.conf.d/xorg.conf
```
add following code:
```bash
Section "Module"
        
    Disable     "dri"
        SubSection  "extmod"
            Option  "omit xfree86-dga"
        EndSubSection
    EndSection

    Section "Device"
        Identifier  "Tegra0"
        Driver      "nvidia"
        Option      "AllowEmptyInitialConfiguration" "true"
    EndSection

    Section "Monitor"
       Identifier "DSI-0"
       Option    "Ignore"
    EndSection

    Section "Screen"
       Identifier    "Default Screen"
       Monitor        "Configured Monitor"
       Device        "Default Device"
       SubSection "Display"
           Depth    24
           Virtual 1280 720
       EndSubSection
    EndSection
```



Copyright © 2024, The instructions contained remains the property of Customade Costumes & Merchandise Pte. Ltd. and PT D'Costume Magnifique. Do not executed or delivered by another company without the express permission of the owners.
***
