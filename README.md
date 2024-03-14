# Monitoring PC through Ethernet / Wifi with VNC viewer

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
Section "Monitor"
  Identifier "Monitor0"
  HorizSync 28.0-80.0
  VertRefresh 48.0-75.0
  # https://arachnoid.com/modelines/
  # 1920x1080 @ 60.00 Hz (GTF) hsync: 67.08 kHz; pclk: 172.80 MHz
  Modeline "1920x1080_60.00" 172.80 1920 2040 2248 2576 1080 1081 1084 1118 -HSync +Vsync
EndSection

Section "Device"
  Identifier "Card0"
  Driver "dummy"
  VideoRam 256000
EndSection

Section "Screen"
  DefaultDepth 24
  Identifier "Screen0"
  Device "Card0"
  Monitor "Monitor0"
  SubSection "Display"
    Depth 24
    Modes "1920x1080_60.00"
  EndSubSection
EndSection
```
# Uninstall Dummy video driver for ubuntu
Removing dummy video driver using this code : 
```bash
sudo apt remove xserver-xorg-video-dummy
sudo apt autoclean && sudo apt autoremove
```




Copyright © 2024, The instructions contained remains the property of Customade Costumes & Merchandise Pte. Ltd. and PT D'Costume Magnifique. Do not executed or delivered by another company without the express permission of the owners.
***
