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

Update packages:
#### opkg update

Install hostapd:
#### opkg install hostapd

A wireless file should already be created in /etc/config

remove "option disabled 1" from  /etc/config/wireless

> note, if wireless file is not configured properly for your driver type, you may need to reconfigure. 
> Issue these commmands to erase and reload configuration while your driver is pluged into Squirrel:
> #### rm -f /etc/config/wireless
> ##### wifi detect > /etc/config/wireless 

Once the device(network adapter) interface on /etc/config/wireless is properly configured, all the file needs is a wifi interface defining the network that sits on top of the device(network adapter).

Here is an example: 

config 'wifi-iface'
        option 'device'     'wl0'
        option 'network'    'wireless'
        option 'mode'       'ap'
        option 'ssid'       'MyWifiAP'
        option 'encryption' 'psk2'
        option 'key'        'secret passphrase'

> Refer to the wireless file on this respitory to view the full contents of this configuration file.

Build and store the network configuration.
> Refer to the network file on this respitory to view the full contents of this configuration file.
#### nano /usr/lib/network_config/evil
place your desired network configurations for this network mode on this file as it will not be overwritten.

Edit contents of /usr/bin/NETMODE:
Within the case statement of this file, a new netmode named "EVIL" should be added.

"EVIL") cp /usr/lib/network_config/evil /etc/config/network
		/etc/init.d/firewall disable
		/etc/init.d/firewall stop
		;;
    
> Refer to the netmode file on this respitory to view the full contents of this configuration file.

Editing DHCP file:
For the internal DHCP server to run how we want on the Squirrel, we must configure the network 'wan' to be ignored and the network 'wireless' to run. 

config dhcp 'wireless'
	option interface 'wireless'
	option start '100'
	option limit '150'
	option leasetime '12h'
	option dhcpv6 'server'
	option ra 'server'

condig dhcp 'wan'
	option interface 'wan'
	option ignore '1'
 
Editing payloads/switch3/payload.sh

> It is worth noting we chose to run this configuration on payload 3 as the oenvpn service is not being used for 
> this scenerio.

  /usr/bin/NETMODE VPN
} || {
	# replace BRIDGE with EVIL for seperated network AP
	/usr/bin/NETMODE EVIL
  
> Refer to the payload file on this respitory to view the full contents of this configuration file.





