# RTL8814AU linux driver with monitor mode and frame injection modified to work for Ubuntu
Credit to astsam, ulli-kroll, madmantm, and the kali linux folks for porting this driver.  I simply made some minor tweaks to get it working on my Ubuntu 14.04/16.04 setups.
Note : i do not own these drivers, not looking for credit, only a method to make these work with my setup. 
It's the most stable/functional driver I've found on github.


Functionality:

Tested that "iw phy" shows VHT support.
Connects at 11ac speeds to AP.
11ac sniffing works; can see radiotap headers + data packets + others.  Some people had issue getting anything other than beacons - but it works for me following below instructions.


Installation:

make RTL8814=1
sudo make RTL8814=1 install
sudo modprobe 8814au


Sniffing:

Make sure USB 3.0 is enabled on your machine.
sudo airmon-ng check kill
sudo ifconfig wlx18d6c70900a3 down
sudo iw dev wlx18d6c70900a3 set monitor none
sudo ifconfig wlx18d6c70900a3 up

To sniff 11ac on channel 36 at 40MHz bandwidth:
sudo iw dev wlx18d6c70900a3 set channel 36 HT40+

To sniff 11ac on channel 40 at 80MHz bandwidth:
sudo iw dev wlx18d6c70900a3 set freq 5200 80 5210

Run wireshark and click on both promisc + monitor for the iface.

Sometimes you may need to down/up the interface if things don't work the first time.  Rebooting the computer can fix other issues.
