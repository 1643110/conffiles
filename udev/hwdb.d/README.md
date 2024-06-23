# Kensington Slimblade Trackball
## Display device information.
$ less /proc/bus/input/devices  
I: Bus=0003 Vendor=047d Product=2041 Version=0110  
N: Name="Kensington Kensington Slimblade Trackball"  
P: Phys=usb-0000:00:14.0-3.3/input0  
S: Sysfs=/devices/pci0000:00/0000:00:14.0/usb1/1-3/1-3.3/1-3.3:1.0/0003:047D:2041.0005/input/input12  
U: Uniq=  
H: Handlers=mouse1 event9   

## Get mapping number.
$ sudo evtest /dev/input/event9  
Event: time 1669213576.168905, type 4 (EV_MSC), code 4 (MSC_SCAN), value **ff000002**  
Event: time 1669213576.168905, type 1 (EV_KEY), code 276 (BTN_EXTRA), value 0  
Event: time 1669213576.168905, -------------- SYN_REPORT ------------  
Event: time 1669213576.448910, type 4 (EV_MSC), code 4 (MSC_SCAN), value **ff000001**
Event: time 1669213576.448910, type 1 (EV_KEY), code 275 (BTN_SIDE), value 1  

## Create hwdb files.(Left_top:back / Right_top:forward)
$ sudo vim /etc/udev/hwdb.d/99-slimblade.hwdb  
evdev:name:Kensington Kensington Slimblade Trackball:*  
  KEYBOARD_KEY_**ff000001**=btn_side  
  KEYBOARD_KEY_**ff000002**=btn_extra  

## hwdb update.
sudo udevadm hwdb --update && sudo udevadm trigger

# Expert Wireless Trackball Mouse
## Display device information.
$ less /proc/bus/input/devices  
I: Bus=0003 Vendor=047d Product=8018 Version=0111
N: Name="Kensington Expert Wireless TB Mouse"
P: Phys=usb-0000:00:14.0-3.3/input0
S: Sysfs=/devices/pci0000:00/0000:00:14.0/usb1/1-3/1-3.3/1-3.3:1.0/0003:047D:801
8.0005/input/input10
U: Uniq=
H: Handlers=mouse1 **event7** 
B: PROP=0
B: EV=17
B: KEY=1b0000 0 0 0 0
B: REL=1943
B: MSC=10

## Get mapping number.
$ sudo evtest /dev/input/**event7**
Event: time 1719145369.811030, -------------- SYN_REPORT ------------
Event: time 1719145369.901032, type 4 (EV_MSC), code 4 (MSC_SCAN), value **90003**
Event: time 1719145369.901032, type 1 (EV_KEY), code 275 (BTN_SIDE), value 0
Event: time 1719145369.901032, -------------- SYN_REPORT ------------
Event: time 1719145370.391039, type 4 (EV_MSC), code 4 (MSC_SCAN), value **90004**
Event: time 1719145370.391039, type 1 (EV_KEY), code 276 (BTN_EXTRA), value 1
Event: time 1719145370.391039, -------------- SYN_REPORT ------------


## Create hwdb files.(Left_top:back / Right_top:forward)
$ sudo vim /etc/udev/hwdb.d/98-Expert_Wireless_Trackball_Mouse.hwdb
evdev:name:Kensington Expert Wireless TB Mouse:*
  KEYBOARD_KEY_**90003**=btn_side
  KEYBOARD_KEY_**90004**=btn_extra

## hwdb update.
sudo udevadm hwdb --update && sudo udevadm trigger

**Reference input-event-codes.h for event codes. : /usr/include/linux/input-event-codes.h.**  
**If imwheel is enabled, keybindings may conflict, so please disable imwheel.**