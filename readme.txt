This purpose of this project is to help mobile devices connect automatically to the closest router to them in case they move away from the original router. In fact, router typically has a special mode called "promiscuous mode" which allows router to capture every packet around it. What we do in this project is modifying the OpenWrt firmware of the router to sniff packets from the target device to get information about the strength signal of the target device toward the router.Then,the information is sent to another router which acts as a server router. Base on strength signals come from the client routers, the server decides whether the device should reconnect to the more closer router to it or not. If yes,it sends request to the router which is currently connected to the device to disconnect to the device for a while. The device then automatically find the nearest router to get connect again.

Installation
1. Replace the default firmware of the router by openwrt firmware. For example: Replace firmware TP-Link wr841n:
https://www.youtube.com/watch?v=P-svaYB-Ffs&t=391s
2. Building your own openwrt firmware by clone this repository and follow instruction.Make sure to install czmq packet before make .This making progress takes quite a long time and require 10-15 gb on the drive.
https://github.com/openwrt/openwrt
3. Replace file recv.c in 
