This purpose of this project is to allow mobile devices connect automatically to the closest router to them in case they move away from the original router. 
In fact, router typically has a special mode called "promiscuous mode" which allows router to capture every packet around it. What we do in this project is modifying the OpenWrt firmware of the router to sniff packets from the target device to get information about the strength signal of the target device toward the router.Then,the information is sent to another router which acts as a server router. Base on strength signals come from the client routers, the server decides whether the device should reconnect to a more closer router to it or not. If yes,it sends request to the router which is currently connected to the device to disconnect to the device for a while. The device then automatically find the nearest router to get connect again.

Installation
1. Building openwrt firmware from this repository and follow instruction.Make sure to install czmq packet before making .This making progress takes quite a long time and requires 10-15 gb on the drive.
https://github.com/openwrt/openwrt
2. Replace <build_root>/build_dir/target-mips_24kc_musl/linux-ar71xx_tiny/backports-2017-11-01/drivers/net/wireless/ath/ath9k/recv.c in building directory with corresponding recv.c from this respository.
3. Copy folder signal_measurement and its Makefile to path <build_root>/build_dir/target-mips_24kc_musl/linux-ar71xx_tiny/backports-2017-11-01/drivers/net/wireless/ath
4. Copy czmq_client and czmq_server to <build_root>/package
5. Remake openwrt with changes:
make package/kernel/mac80211/compile
make package/czmq_clent/compile
make package/czmq_server/compile
6. Connect PC and router through cable . Replace default firmware of the router by openwrt firmware. For example: Replace firmware TP-Link wr841n:
https://www.youtube.com/watch?v=P-svaYB-Ffs&t=391s
Connect to router through SSH.
7. Find ath9k .ipk package in
<build_root>/bin/targets/ar71xx/tiny/packages
find czmq_client and czmq_server .ipk package and copy these .ipk packages to /tmp directory of router.
8. Install packages:
cd /tmp
opkg install –force-reinstall kmod-ath9k*
opkg install  czmq_client (In client router)
opkg install  czmq_server (In server router)
9. Restart client and server routers.
