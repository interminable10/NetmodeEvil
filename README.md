# NetmodeEvil :+1:
Custom netmode created on Hak5's Packet Squirrel
Virmware version 1.2

Edited Files:
-/etc/config/wireless
-/usr/lib/network_config/evil
-/usr/bin/NETMODE
-/etc/config/DHCP
-payloads/switch3/payload.sh


## Steps:

(Make sure squirrel is connected to internet)

#### opkg update

#### opkg install hostapd

This will create a wireless file in /etc/config

remove "option disabled 1" from  /etc/config/wireless

> note, if wireless file is not configured properly for your driver type, you may need to reconfigure. 
> Issue these commmands to erase and reload configuration while your driver is pluged into Squirrel:
> #### rm -f /etc/config/wireless
> ##### wifi detect > /etc/config/wireless 




