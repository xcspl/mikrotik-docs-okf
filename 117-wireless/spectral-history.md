---
type: Reference
title: "Spectral history"
description: "Plots spectrogram. Power values that fall in different ranges are printed as different colored characters with the same foreground and background color, so it is possible to copy and paste the terminal output of this com."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Spectral history

/interface/wifi/spectral-history <wifi interface name> range=

Plots spectrogram. Power values that fall in different ranges are printed as different colored characters with the same foreground and background color, so it is possible to copy and paste the terminal output of this command.

data-min/max/avg, by default average is used for data. The average should be used in most scenarios, but in some cases "min" can be useful to check if there are any frequencies that have a constant signal output on them. Max will show the strongest signal that was detected, instead of the average signal. interv - interval of how often to update the data values; interval-interval at which spectrogram lines are printed; duration-terminate command after a specified time. default is indefinite; range-scan specific range, required; resolution-frequency step; show-interference-yes/no

Possible types of classified interference:

Microwave oven ( )O Continuous Wave ( )C WLAN (Wideband)  ( )W Cordless phone 2.4 ( )T Cordless phone 5 ( )T Bluetooth (BB) Frequency hopping spread spectrum ( )F

WPS

### WPS client

The wps-client command enables obtaining authentication information from a WPS-enabled AP.

/interface/wifi/wps-client wifi1

### WPS server

An AP can be made to accept WPS authentication by a client device for 2 minutes by running the following command.

/interface/wifi wps-push-button wifi1

## Radios

Information about the capabilities of each radio can be gained by running the `/interface/wifi/radio print detail` command.  It can be useful to see what bands are supported by the interface and what channels can be selected. The country profile that is applied to the interface will influence the results.

interface/wifi/radio/print detail Flags: L-local 0 L radio-mac=48:A9:8A:0B:F7:4A phy-id=0 tx-chains=0,1 rx-chains=0,1 bands=5ghz-a:20mhz,5ghz-n:20mhz,20/40mhz,5ghz-ac:20mhz,20/40mhz,20/40/80mhz,5ghz-ax:20mhz, 20/40mhz,20/40/80mhz ciphers=tkip,ccmp,gcmp,ccmp-256,gcmp-256,cmac,gmac,cmac-256,gmac-256 countries=all 5g-channels=5180,5200,5220,5240,5260,5280,5300,5320,5500,5520,5540,5560,5580,5600,5620,5640,5660, 5680,5700,5720,5745,5765,5785,5805,5825 max-vlans=128 max-interfaces=16 max-station-interfaces=3 max-peers=120 hw-type="QCA6018" hw-caps=sniffer interface=wifi1 current-country=Latvia current-channels=5180/a,5180/n,5180/n/Ce,5180/ac,5180/ac/Ce,5180/ac/Ceee,5180/ax,5180/ax/Ce, 5180/ax/Ceee,5200/a,5200/n,5200/n/eC,5200/ac,5200/ac/eC,5200/ac/eCee,5200/ax...

...5680/n/eC,5680/ac,5680/ac/eC,5680/ax,5680/ax/eC,5700/a,5700/n,5700/ac,5700/ax current-gopclasses=115,116,128,117,118,119,120,121,122,123 current-max-reg-power=30
While Radio information gives us information about supported channel width, it is also possible to deduce this information from the product page, to do so you need to check the following parameters: number of chains, max data rate. Once you know these parameters, you need to check the modulation and coding scheme (MCS) table, for example, here: https://mcsindex.com/.

If we take hAP ax, as an example, we can see that number of chains is 2, and the max data rate is 12 2 00 - 1201 in the MCS table. In the MCS table we need to find entry for 2 spatial streams-chains, and the respective data rate, which in this case shows us that 80MHz is the maximum supported channel width.

## Registration table

'/interface/wifi/registration-table/' displays a list of connected wireless clients and detailed information about them.

De-authentication

Wireless peers can be manually de-authenticated (forcing re-association) by removing them from the registration table.

/interface/wifi/registration-table remove [find where mac-address=02:01:02:03:04:05]

## WiFi CAPsMAN

Note

This section describes the operation of the CAPsMAN feature inb the wifi-qcom and wifi-qcom-ac package. For devices with the older "wireless" package, see the respective manual here. Here and further below, when talking about "WiFi", we mean the new WiFi menu, not the technology.

Controlled Access Point system Manager (CAPsMAN) allows applying wireless settings to multiple MikroTik WiFi AP devices from a central configuration interface, ie. allows the centralization of wireless network management. When using CAPsMAN, the network will consist of a number of 'Controlled Access Points' (CAP) that provide wireless connectivity and a 'system Manager' (CAPsMAN) that manages the configuration of the APs, it also takes care of client authentication.

Requirements:

Any RouterOS device, that supports the WiFi package, can be a controlled wireless access point (CAP) as long as it has at least a Level 4 RouterOS license. WiFi CAPsMAN server can be installed on any RouterOS device that supports the WiFi package, even if the device itself does not have a wireless interface Unlimited CAPs (access points) supported by CAPsMAN

WiFi CAPsMAN can only control WiFi interfaces, and WiFi CAPs can join only WiFi CAPsMAN, similarly, regular CAPsMAN only supports non- WiFi caps.

The CAPs don't send traffic usage information to CAPsMAN.

### CAPsMAN Discovery by CAP

CAP discovers CAPsMAN address/hostname via:

Layer 2 discovery. DHCP option 138 (CAPsMAN address). DHCP option 15 (custom domain): resolves _capsman._tcp.<domain>. Default MikroTik 'lan' domain: resolves _capsman._tcp.lan.

### Radio Provisioning

Once configuration templates have been created, you can select which devices should be provisioned with each of the template. Of course, in simple setups it is enough to have only one provisioning rule, but if you wish to send one configuration to 2.4GHz interfaces and a different one to 5GHz interfaces, you can create two provisioning rules and define, which template is sent where, using supported-bands parameter.

CAPsMAN distinguishes between actual wireless interfaces (radios) based on their built-in MAC address (radio-mac). This implies that it is impossible to manage two radios with the same MAC address on one CAPsMAN. Radios currently managed by CAPsMAN (provided by connected CAPs) are listed in**/** **interface/wifi/radio** menu, this list will also include the built-in wifi interfaces that are present on CAPsMAN itself if there are any:

[admin@c52i] > interface/wifi/radio/print Flags: L-LOCAL Columns: CAP, RADIO-MAC, INTERFACE # CAP RADIO-MAC INTERFACE 0 L 18:FD:74:AF:F4:28 wifi1 1 L 18:FD:74:AF:F4:29 wifi2 2 hapAX3@192.168.88.30 48:A9:8A:0B:F7:4B cap1

When CAP connects, CAPsMAN at first tries to bind each CAP radio to CAPsMAN master interface based on radio-mac. If an appropriate interface is found, the radio gets set up using master interface configuration and configuration of slave interfaces that refer to a particular master interface. At this moment interfaces (both master and slaves) are considered bound to radio and radio is considered provisioned. This happens only if there were matching static entries already present under /interface/wifi, typically if the entry was made previously either manually, or with provisioning rules that contain action "create-enabled" or "create-disabled".

If no matching master interface for radio is found, CAPsMAN executes 'provisioning rules', which are defined under /interface/wifi/provisioning/. Provisioning rules is an ordered list of rules that contain settings that specify which radio to match and settings that determine what action to take if a radio matches.

When CAP joins CAPsMAN, and there is no matching interface for it present under /interface/wifi, provisioning rules will automatically be checked, once a match is found, the CAP's wireless interface will appear under /interface/wifi. Such an interface is "provisioned", provisioned in this context means that there is a wifi interface present for the radio, and it has a configuration profile assigned to it.

There is also an option to manually provision interfaces, which will make CAPsMAN start evaluating provisioning rules against the specific interface, and a new interface will be created upon match. If there was already an entry present for the radio under /interface/wifi/, that entry will be deleted and re- created. Manual provisioning re-creates the interface and is generally not needed, since provisioning rules are evaluated automatically, and if you change the configuration profile associated with the provisioning rule, the changes will be applied to all wifi interfaces that use that configuration. If you manually provision interfaces, the interface ID or name can change, resulting in broken references to other objects, for example, bridge ports.

Manual provision can be done under /interface/wifi/capsman/remote-cap/provision to provision all radios associated with specific CAPs, it can also be done under /interface/wifi/radio/provision, to provision specific radios.

CAPsMAN cannot manage it's own wifi interfaces using configuration.manager=capsman, it is enough to just set the same configuration profile on local interfaces manually as you would with provisioning rules, and the end result will be the same as if they were CAPs. That being said, it is also possible to provision local interfaces via /interface/wifi/radio menu, it should be noted that to regain control of local interfaces after provisioning, you will need to disable the matching provisioning rules and press "provision" again, which will return local interfaces to an unconfigured state.

Provision must be done only initially, and is done automatically upon CAP joining if there are matching provisioning rules that are enabled. If you adjust any configuration profile that is linked to the provisioned interface, all changes will be "pushed" as soon as you apply changes to the profile, with no need to re-create the already existing interface. Provisioning itself is not for sending configuration, it is for essentially creating a new interface. In most cases, there is no reason to perform manual provisioning once you already have CAP interfaces running.

### CAPSMAN Datapath

Datapath settings control data forwarding related aspects. On CAPsMAN datapath settings are configured in the datapath profile menu /interface/wifi /datapath/ or directly in a configuration profile or interface menu as settings with datapath. prefix.

There are 2 major forwarding/traffic-processing modes:

local forwarding mode (traffic-processing=on-cap), where CAP is locally forwarding data to and from wireless interface; CAPsMAN forwarding mode (traffic-processing=on-capsman), where CAP sends to CAPsMAN all data received over wireless and only sends out the wireless data received from CAPsMAN.

CAPsMAN forwarding is only possible starting with 7.21beta2 version. On older versions, only CAP forwarding is supported.

CAPsMAN forwarding is not supported by wifi-qcom-ac devices (wifi-qcom-ac drivers only support local forwarding).

### CAPsMAN-CAP simple configuration example:

CAPsMAN in WiFi uses the same menu as a regular WiFi interface, meaning when you pass configuration to CAPs, you have to use the same configuration, security, channel configuration, etc. as you would for regular WiFi interfaces.

You can configure sub-configuration menus, directly under "/interface/wifi/configuration" or reference previously created profiles in the main configuration profile

CAPsMAN:

#create a security profile /interface wifi security add authentication-types=wpa3-psk name=sec1 passphrase=HaveAg00dDay

#create configuraiton profiles to use for provisioning /interface wifi configuration add country=Latvia name=5ghz security=sec1 ssid=CAPsMAN_5 add name=2ghz security=sec1 ssid=CAPsMAN2 add country=Latvia name=5ghz_v security=sec1 ssid=CAPsMAN5_v

#configure provisioning rules, configure band matching as needed /interface wifi provisioning add action=create-dynamic-enabled master-configuration=5ghz slave-configurations=5ghz_v supported-bands=\ 5ghz-n add action=create-dynamic-enabled master-configuration=2ghz supported-bands=2ghz-n

#enable CAPsMAN service /interface wifi capsman set ca-certificate=auto enabled=yes

CAP:

#enable CAP service, in this case CAPsMAN is on same LAN, but you can also specify "caps-man-addresses=x.x.x.x" here /interface/wifi/cap set enabled=yes

#set configuration.manager= on the WiFi interface that should act as CAP /interface/wifi/set wifi1,wifi2 configuration.manager=capsman-or-local

If the CAP is hAP ax or hAP ax, it is strongly recommended to enable RSTP in the bridge configuration, on the CAP 2 3

configuration.manager should only be set on the CAP device itself, don't pass it to the CAP or configuration profile that you provision.

The interface that should act as CAP needs additional configuration under "interface/wifi/set wifiX configuration.manager="

### CAPsMAN-CAP VLAN configuration example:

In this example, we will assign VLAN10 to our main SSID, and will add VLAN20 for the guest network, ether5 from CAPsMAN is connected to CAP.

CAPs using "wifi-qcom" package can get "vlan-id" via Datapath from CAPsMAN, CAPs using "wifi-qcom-ac" package will need to use the configuration provided at the end of this example.

CAPsMAN:

/interface bridge add name=br vlan-filtering=yes /interface vlan add interface=br name=MAIN vlan-id=10 add interface=br name=GUEST vlan-id=20 /interface wifi datapath add bridge=br name=MAIN vlan-id=10 add bridge=br name=GUEST vlan-id=20 /interface wifi security add authentication-types=wpa2-psk,wpa3-psk ft=yes ft-over-ds=yes name=Security_MAIN passphrase=HaveAg00dDay add authentication-types=wpa2-psk,wpa3-psk ft=yes ft-over-ds=yes name=Security_GUEST passphrase=HaveAg00dDay /interface wifi configuration add datapath=MAIN name=MAIN security=Security_MAIN ssid=MAIN_Network add datapath=GUEST name=GUEST security=Security_GUEST ssid=GUEST_Network /ip pool add name=dhcp_pool0 ranges=192.168.1.2-192.168.1.254 add name=dhcp_pool1 ranges=192.168.10.2-192.168.10.254 add name=dhcp_pool2 ranges=192.168.20.2-192.168.20.254 /ip dhcp-server add address-pool=dhcp_pool0 disabled=yes interface=br name=dhcp1 add address-pool=dhcp_pool1 interface=MAIN name=dhcp2 add address-pool=dhcp_pool2 interface=GUEST name=dhcp3 /interface bridge port add bridge=br interface=ether5 add bridge=br interface=ether4 add bridge=br interface=ether3 add bridge=br interface=ether2 /interface bridge vlan add bridge=br tagged=br,ether5,ether4,ether3,ether2 vlan-ids=20 add bridge=br tagged=br,ether5,ether4,ether3,ether2 vlan-ids=10 /interface wifi capsman set enabled=yes interfaces=br /interface wifi provisioning add action=create-dynamic-enabled master-configuration=MAIN slave-configurations=GUEST supported-bands=5ghz-ax add action=create-dynamic-enabled master-configuration=MAIN slave-configurations=GUEST supported-bands=2ghz-ax /ip address add address=192.168.1.1/24 interface=br network=192.168.1.0 add address=192.168.10.1/24 interface=MAIN network=192.168.10.0 add address=192.168.20.1/24 interface=GUEST network=192.168.20.0 /ip dhcp-server network add address=192.168.1.0/24 gateway=192.168.1.1 add address=192.168.10.0/24 gateway=192.168.10.1 add address=192.168.20.0/24 gateway=192.168.20.1 /system identity set name=cAP_Controller

CAP using "wifi-qcom" package:

/interface bridge add name=bridgeLocal /interface wifi datapath add bridge=bridgeLocal comment=defconf disabled=no name=capdp /interface wifi set [ find default-name=wifi1] configuration.manager=capsman datapath=capdp disabled=no set [ find default-name=wifi2] configuration.manager=capsman datapath=capdp disabled=no /interface bridge port add bridge=bridgeLocal comment=defconf interface=ether1 add bridge=bridgeLocal comment=defconf interface=ether2 add bridge=bridgeLocal comment=defconf interface=ether3 add bridge=bridgeLocal comment=defconf interface=ether4 add bridge=bridgeLocal comment=defconf interface=ether5 /interface wifi cap set discovery-interfaces=bridgeLocal enabled=yes slaves-datapath=capdp /ip dhcp-client add interface=bridgeLocal disabled=no

CAP using "wifi-qcom-ac" package:

/interface bridge add name=bridgeLocal vlan-filtering=yes /interface wifi set [ find default-name=wifi1] configuration.manager=capsman disabled=no set [ find default-name=wifi2] configuration.manager=capsman disabled=no /interface bridge port add bridge=bridgeLocal comment=defconf interface=ether1 add bridge=bridgeLocal comment=defconf interface=ether2 add bridge=bridgeLocal comment=defconf interface=ether3 add bridge=bridgeLocal comment=defconf interface=ether4 add bridge=bridgeLocal comment=defconf interface=ether5 add bridge=bridgeLocal interface=wifi1 pvid=10 add bridge=bridgeLocal interface=wifi21 pvid=20 add bridge=bridgeLocal interface=wifi2 pvid=10 add bridge=bridgeLocal interface=wifi22 pvid=20 /interface bridge vlan add bridge=bridgeLocal tagged=ether1 untagged=wifi1,wifi2 vlan-ids=10 add bridge=bridgeLocal tagged=ether1 untagged=wifi21,wifi22 vlan-ids=20 /interface wifi cap set discovery-interfaces=bridgeLocal enabled=yes slaves-static=yes

Check the dynamically created interface and assign the PVID to the appropriate one. Make sure not to use /interface/bridge/port/add bridge=bridgeLocal interface=all, as this will prevent you from applying PVIDs to wifi interfaces.

Additionally, the configuration below has to be added to the CAPsMAN configuration:

/interface wifi datapath add bridge=br name=DP_AC /interface wifi configuration add datapath=DP_AC name=MAIN_AC security=Security_MAIN ssid=MAIN_Network add datapath=DP_AC name=GUEST_AC security=Security_GUEST ssid=GUEST_Network /interface wifi provisioning add action=create-dynamic-enabled master-configuration=MAIN_AC slave-configurations=GUEST_AC supported- bands=5ghz-ac add action=create-dynamic-enabled master-configuration=MAIN_AC slave-configurations=GUEST_AC supported- bands=2ghz-n

Passing datapaths "MAIN/GUEST" from the start of the example to "wifi-qcom-ac" CAP would be misconfiguration, make sure to use datapath without "vlan-id" specified to such devices.

With wifi-qcom-ac drivers, datapath setting on the CAPSMAN is not needed. The example, simply, showcases that "vland-id" must be omitted.

### CAPsMAN-OWE configuration example:

CAPsMAN:

/interface wifi configuration add country=Latvia disabled=no hide-ssid=yes name=OWE security.authentication-types=owe .owe-transition- interface=auto ssid=MikroTik_OWE add country=Latvia disabled=no name=open security.owe-transition-interface=auto ssid=Mikrotik_open

/interface wifi provisioning add action=create-dynamic-enabled disabled=no master-configuration=open slave-configurations=OWE

/interface wifi capsman set ca-certificate=auto enabled=yes

CAP:

/interface/wifi/cap set enabled=yes /interface/wifi/set wifi1,wifi2 configuration.manager=capsman-or-local

## Advanced examples

Enterprise wireless security with User Manager v5

## Replacing 'wireless' package

Some MikroTik Wi-Fi 5 APs, which ship with their interfaces managed by the 'wireless' menu, can install the additional 'wifi-qcom-ac' package to make their interfaces compatible with the 'wifi' menu instead.

To do this, it is necessary to uninstall the 'wireless' package, then install 'wifi-qcom-ac'.

Please note that "wifi-qcom-ac" drivers are much more resource-heavy. You will have less availible RAM when using the new package and that is something to keep in mind.

Compatibility

The wifi-qcom-ac package includes alternative drivers for IPQ4018/4019 and QCA9984 radios that make them compatible with the WiFi configuration menu. For possible, wifi-qcom-ac/wifi-qcom/wireless, package combinations, please see the package types section here.

As a rule of thumb, the package is compatible with 802.11ac products, which have an ARM CPU. It is NOT compatible with any of our 802.11ac products which have a MIPS CPU.

|which have a MIPS CPU.|||
|---|---|---|
|Compatibility|Devices||
|Compatible|Audience, Audience LTE kit, Chateau (all variants of D53), hAP ac,|, hAP ac^3, cAP ac, cAP XL ac, LDF 5 ac LHG XL 5 ac LHG XL SXTsq 5 ac|
|Incompatible|RB4011iGS+5HacQ2HnD-IN (no support for the 2.4GHz interface), Cube 60Pro ac (no support for 60GHz interface), wAP ac (RBwAPG-5HacT2HnD) and all other devices with a MIPSBE CPU||

,, ^2 wAP ac (RBwAPG-5HacD2HnD), 52 ac NetMetal ac^2, mANTBox 52 15s,

Benefits

WPA3 authentication and OWE (opportunistic wireless encryption)

802.11w standard management frame protection
802.11r/k/v MU-MIMO and beamforming 400Mb/s maximum data rate in the 2.4GHz band for IPQ4019 interfaces These benefits apply both to the wifi-qcom and wifi-qcom-ac packages.
### Lost features

The following notable features are lost when running 802.11ac products with drivers that are compatible with the 'wifi' management interface

Nstreme and Nv2 wireless protocols VLAN configuration in the wireless settings (Per-interface VLANs can be configured in bridge settings) Compatibility with station-bridging as implemented in the 'wireless' package, station-bridge only works between the same type of drivers. Wifi to Wifi, and Wireless to Wireless.

## Property Reference

### AAA properties

Properties in this category configure an access point's interaction with AAA (RADIUS) servers.

Certain parameters in the table below take format-string as their value. In a format-string, certain characters are interpreted in the following way:

Character Interpretation

a Hexadecimal character making up the MAC address of the client device in lowercase

A Hexadecimal character making up the MAC address of the client device in upper case

i Hexadecimal character making up the MAC address of the AP's interface in lowercase

I (capital 'i') Hexadecimal character making up the MAC address of the AP's interface in upper case

N The entire name of the AP's interface (e.g. 'wifi1')

S The entire SSID

All other characters are used without interpreting them in any way. For examples, see default values.

Property Description

called-format (format-string Default:; II-II-Format for the value of the Called-Station-Id RADIUS attribute, in AP's messages to RADIUS servers. II-II-II-II:S)

calling-format (format-string Default:; ***AA:*** Format for the value of the Calling-Station-Id RADIUS attribute, in AP's messages to RADIUS servers. ***AA:AA:AA:AA:AA**)*

interim-update (time interval; Default: 5m) Interval at which to send interim updates about traffic accounting to the RADIUS server.

mac-caching (time interval; Default: disabl Length of time to cache RADIUS server replies, when MAC address authentication is enabled. ed) This resolves issues with client device authentication timing out due to (comparatively high latency of RADIUS server replies.

name (string Default:; no) A unique name for the AAA profile.

nas-identifier (string) Value of the NAS-Identifier attribute, in AP's messages to RADIUS servers. Defaults to the host name of the device (/system/identity).

password-format (format-string) Format for value to use in calculating the value of the User-Password attribute in AP's messages to RADIUS servers when performing MAC address authentication.

Default value: "" (an empty string).

username-format (format-string Default:; ***A*** Format for the value of the User-Name attribute in APs messages to RADIUS servers when performing ***A:AA:AA:AA:AA:AA**)* MAC address authentication.

### Channel properties

Properties in this category specify the desired radio channel.

Property Description

band (2ghz-g 2ghz-n 2ghz-ax  2g | | | Frequency band and wireless standard that will be used by the AP. Defaults to newest supported standard. hz-be 5ghz-a 5ghz-ac 5ghz-an | | | | Note that band support is limited by radio capabilities. 5ghz-ax 5ghz-be  6ghz-ax 6ghz-| | | be)

deprioritize-unii-3-4 (no yes | ) Whether to assign lower priority to channels with a control frequency of 5720 or 5825-5885 MHz. These channels are unsupported by some client devices, making their automatic selection undesirable. Defaults to 'yes' in ETSI regulatory domains, elsewhere to 'no'.

frequency (list of numbers or For an interface in AP mode, specifies frequencies (in MHz) to consider when picking control channel center number ranges) frequency.

For an interface in station mode, specifies frequencies on which to scan for APs.

Leave unset (default) to consider all frequencies supported by the radio and permitted by the applicable regulatory profille.

The parameter can contain 1 or more comma-separated values of decimal numbers or, optionally, ranges of numbers denoted using the syntax RangeBeginning-RangeEnd:RangeStep

Examples of valid channel.frequency values:

2412 2412,2432,2472 5180-5240:20,5500-5580:20

preamble-puncturing (no | yes; Default: no ) Enables puncturing support on this interface for DFS/radar (802.11be only).

When set, the access point may disable ("puncture") only the affected 20 MHz part of a wide 80/160 MHz channel when radar signal presence is detected, instead of switching the whole channel.

For 80 MHz channels a single 20 MHz sub-channel may be punctured. For 160 MHz channels either one 20 MHz sub-channel or one 40 MHz block may be punctured.

The current puncturing state can be observed in '/interface/wifi/monitor' output for this interface, where punctured sub-channels are marked with the letter `o`.

reselect-interval (time interval; Defa Specifies the interval when the interface should run "rescan channel availability" and select the most appropriate ult: disabled) one to use. Specifying interval will allow the system to select this interval dynamically and randomly. This helps to avoid a situation when many APs at the same time scan the network, select the same channel, and prefer to use it at the same time. reselect-interval uses a background scan.

The reselect process will choose the most suitable channel considering the number of networks in the channel, channel usage, and overlap with networks in adjacent channels. It can be used with a list of frequencies defined, or with frequency not set-using all supported frequencies.

Example:

01:00..01:30 → Would set the rescan of channels to run every 1 hour + random time up to 30 minutes. The first time, it could run a rescan after "1 hour and 15 minute", later, it could be "1 hour and 1 second", then, it could be "1 hour, 29 minutes and 59 seconds" ...at random, a rescan will happen between every 1 hour to 1 hour 30 minutes.

reselect-time (time interval; Default: Specifies the clock time when the interface should run "rescan channel availability" and select the most disabled) appropriate one to use. Specifying the clock time will allow the system to select this time dynamically and randomly. This helps to avoid a situation when many APs at the same time scan the network, select the same channel, and prefer to use it at the same time. reselect-time uses a background scan.

The reselect process will choose the most suitable channel considering the number of networks in the channel, channel usage, and overlap with networks in adjacent channels. It can be used with a list of frequencies defined, or with frequency not set-using all supported frequencies.

Example:

01:00..01:30 → Would set the rescan of channels to run every night, once, randomly, between 01:00 AM to 01:30 AM, system clock time. 14:00..14:30 → Would set the rescan of channels to run every day (after midday), once, randomly between 14:00:00 to 14:30:00 (or 2 PM to 2:30 PM), system clock time.

secondary-frequency (list of integers For split 80+80MHz channels, specifies permitted center frequencies for the secodnary 80MHz segment. | 'disabled') For 320MHz channels, specifiies permitted 320MHz channel centers.

When unset (default), does not limit channel selection.

E.g. 'width=20/40/80+80mhz frequency=5180' would allow combining channel 42 with any other supported 80MHz channel. 'width=20/40/80+80mhz frequency=5180 secondary-frequency=5530' would only allow combining channels 42 and 106. 'width=20/40/80/160/320mhz frequency=6115' would allow use of either channel 31 or 63. 'width=20/40/80/160/320mhz frequency=6115 secondary-frequency=6265' allows use of only channel 63. Refer here for lists of valid 5GHz and 6GHz channels.
skip-dfs-channels  (10min-cac all | | Whether to avoid using channels, on which channel availability check (listening for presence of radar signals) is disabled; default: disabled) required.

10min-cac-interface will avoid using channels, on which 10 minute long CAC is required all-interface will avoid using all channels, on which CAC is required disabled  - interface may select any supported channel, regardless of CAC requirements

width ( 20mhz 20/40mhz 20 | | Width of radio channel. Defaults to widest channel supported by the radio hardware. /40mhz-Ce 20/40mhz-eC 20/40 | | /80mhz 20/40/80+80mhz 20/40 | | /80/160mhz | 20/40/80/160/320mhz)

### Configuration properties

This section includes properties relating to the operation of the interface and the associated radio.

Property Description

antenna-gain (in Overrides the default antenna gain. The master interface of each radio sets the antenna gain for every interface which uses the same teger 0..30) radio.

This setting cannot override the antenna gain to be lower than the minimum antenna gain of a radio. No default value.

beacon-interval ( Interval between beacon frames of an AP. time interval 100ms..1s; The 802.11 standard defines beacon interval in terms of time units (1 TU = 1.024 ms). The actual interval between default: 100ms) beacons will be 1 TU for every 1 ms configured.

Every AP running on the same radio (i.e. a master AP and all its 'virtual'/'slave' APs) must use the same beacon interval.

chains (list of Radio chains to use for receiving signals. Defaults to all chains available to the corresponding radio hardware. integer 0..7 )

country (name of a country; default: Latvia)

distance ()

dtim-period (inte ger 1..255; default: 1)

hide-ssid (no | yes; default: no)

hw-protection- mode (cts-to- self | none | rts- cts)

installation (indo or outdoor defa |; ult:indoor)

manager (caps man capsman- | or-local local; | default: local)

max-clients (inte ger 1..1000; default: 1000)

Determines, which regulatory domain restrictions are applied to an interface.

It is important to set this value correctly to comply with local regulations and ensure interoperability with other devices.

In a controlled environment or if you have a special permission to use it in your region, you can select country=Superch annel (with this country profile, router's Tx output power will not be restricted by the software, and the router will output as much power as its hardware chip allows, unless manual tx-power is configured to lower it). Does not work for wifi-qcom- ac drivers.

Maximum link distance in kilometers, needs to be set for long-range outdoor links. The value should reflect the distance to the AP or station that is furthest from the device. Unconfigured value allows usage of 2 km links.

distance is not used by the wifi-qcom-ac package. Setting distance above the actual needed value can have detrimental effects on throughput and latency.

DTIM is a part of the beacon frame that informs power saving (sleeping) stations about incoming multicast and broadcast traffic.

The setting configures a period at which to transmit multicast or broadcast traffic, when there are client devices in power save mode connected to the AP. Expressed as a multiple of the beacon interval (e.g. with default values dtim-period=1 and beacon- interval=100ms, it is sent every 1 x 100 ms = 100 ms).

Higher values enable client devices to save more energy, but increase network latency. Lower values enable clients to wake up more often, using more energy.

yes-AP does not include its SSID in beacon frames, and does not reply to probe requests that have broadcast SSID. no-AP includes its SSID in the beacon frames, and replies to probe requests that have broadcast SSID.

To reduce frame collisions, you can use:

cts-to-self  - Interface sends CTS frame to own address before transmitting an MPDU (to notify nearby devices to hold off talking over each other); none  - Interface does not use any hardware protection mechanism; rts-cts-Interface sends an RTS frame before each MPDU (RTS is followed by a CTS from a receiver and the communication happens after that-both RTS and CTS frames can hold off other devices);

Default (unset): interface sends RTS frames before re-transmitted MPDUs.

Devices installed outdoors will avoid use of indoor-only radio channels.

capsman-the interface will act as CAP only, this option should not be passed via provisioning rules to the CAP

capsman-or-local-the interface will get configuration via CAPsMAN or use its own, if /interface/wifi/cap is not enabled.

local-interface won't contact CAPsMAN in order to get configuration.

Maximum number of associated clients.

mode (ap stati | Interface operation mode on) ap (default) - interface operates as an access point station-interface acts as a client device, scanning for access points advertising the configured SSID station-bridge-interface acts as a client device and enables support for a 4-address frame format, so that the interface can be used as a bridge port station-pseudobridge-the interface keeps track of outgoing IP connections and performs MAC address translation similarly to how IP masquerading works

The 'wifi' station-bridge mode,  is incompatible with APs running the older 'wireless' package and vice versa.

multicast-With the multicast-enhance feature enabled, an AP will convert every multicast-addressed IP or IPv6 packet into multiple unicast- enhance (enabl addressed frames for each connected station. ed  disabled; | This may improve link throughput and reliability since, unlike multicast frames, unicasts are acknowledged by stations and transmitted default: disabled) using a higher data rate.

qos-classifier (d Specify which WMM ruleset to follow. APs and clients classify packets based on the priority assigned to them (as per WMM scp-high-3-bits | specification) → 1,2 - background; 0,3 - best effort; 4,5 - video; 6,7 - voice. "Better" access category has a higher probability of getting priority; default: access to medium (e.g. voice frames will have a shorter "back off" time after medium becomes "idle", ensuring that they are more priority) likely to be send out sooner than "worse" category frames).

dscp-high-3-bits-interface will transmit data packets using a WMM priority equal to the value of the 3 most significant bits of the IP DSCP field priority-interface will transmit data packets using a WMM priority equal to that set by IP firewall or bridge filter

802.11ac wireless chipsets do not support the dscp-high-3-bits classifier mode. For 802.11ac interfaces, please see DSCP from priority.
ssid (string; The name of the wireless network, aka the (E)SSID. default: no)

station-roaming Wifi interface running in station or station-bridge mode will periodically scan for AP candidates to roam to, the weaker the signal to AP (no | yes; is, the more often the scan will be performed. If an AP with a better signal is found, the station will roam to it. FT is supported, and Default: no) station will respond to BSS Transion Request if steering.wnm is enabled.

tx-chains (list of Radio chains to use for transmitting signals. Defaults to all chains available to the corresponding radio hardware. integer 0..7)

tx-power (intege A limit on the transmit power (in dBm) of the interface. Can not be used to set power above limits imposed by the regulatory profile. r 0..40) Unset by default.

### Datapath properties

Parameters relating to forwarding packets to and from wireless client devices.

Property Description

bridge (bridge interface) Bridge interface to add interface to, as a bridge port. Virtual ('slave') interfaces are by default added to the same bridge, if any, as the corresponding master interface. Master interfaces are not by default added to any bridge.

bridge-cost (integer; Bridge port cost to use when adding as bridge port. default: 10)

bridge-horizon (none integ | Bridge horizon to use when adding as bridge port. er; default: none)

client-isolation  (no yes; | Determines whether client devices connecting to this interface are (by default) isolated from others or not. default: no) This policy can be overridden on a per-client basis using access list rules, so a an AP can have a mixture of isolated and non-isolated clients. Traffic from an isolated client will not be forwarded to other clients and unicast traffic from a non-isolated client will not be forwarded to an isolated one.

interface-list (interface list; List to which add the interface as a member. default: no)

traffic-processing (on-cap | on-capsman | on-capsman-This setting is only available starting with 7.21beta2 version. secure)

on-cap, will make it so that the CAP itself is responsible for handling all WiFi traffic (same as any standalone AP would); on-capsman, will make it so that the CAP's WiFi traffic is forwarded to a pseudo-tunnel to the CAPSMAN and the CAPsMAN becomes responsible for CAP's traffic handling; on-capsman-secure, will make it so that the CAP's WiFi traffic is forwarded to an encrypted pseudo-tunnel to the CAPSMAN and the CAPsMAN becomes responsible for CAP's traffic handling.

When using traffic-processing=on-capsman setting, be aware, that since all the CAP's WiFi traffic now gets handled by the CAPsMAN (gets pushed into the CAPsMAN), it will increase CAPSMAN's resource consumption (CPU and RAM usage).

vlan-id (none | integer 1.. Default VLAN ID to assign to client devices connecting to this interface (only relevant to interfaces in AP mode). 4095; default: none) When a client is assigned a VLAN ID, traffic coming from the client is automatically tagged with the ID and only packets tagged with with this ID are forwarded to the client.

802.11ac chipsets do not support this type of VLAN tagging, but they can be configured as VLAN access ports in bridge settings.
### Security Properties

Parameters relating to authentication.

Property Description

authentication-types (list of wpa-psk, Authentication types to enable on the interface. wpa2-psk, wpa2-psk-sha2, wpa-eap, wpa2-eap, wpa3-psk, owe, wpa3-eap, The default value is an empty list (no authentication, an open network). wpa3-eap-192) Configuring a passphrase adds to the default list the wpa2-psk authentication method (if the interface is an AP) or both wpa-psk and wpa2-psk (if the interface is a station).

Configuring an eap-username and an eap-password adds to the default list wpa-eap and wpa2-eap authentication methods.

beacon-protection (disabled  enabled |) Whether to enable beacon integrity protection. Support depends on 'beacon-protection' radio capability.

Enabled by default for 802.11be interfaces.

connect-group ( string ) APs within the same connect group do not allow more than 1 client device with the same MAC address. This is to prevent malicious authorized users from intercepting traffic intended to other users ('MacStealer' attack) or performing a denial of service attack by spoofing the MAC address of a victim.

Handling of new connections with duplicate MAC addresses depends on the connect-priority of AP interfaces involved.

By default, all APs are assigned the same connect-group.

connect-priority (accept-priority/hold-These parameters determine, how a connection is handled if the MAC address of the client device is the priority (integers)) same as that of another active connection to another AP. If (accept-priority of AP2) < (hold-priority of AP1), a connection to AP2 wil cause the client to be dropped from AP1. If (accept-priority of AP2) = (hold-priority of AP1), a connection to AP2 will be allowed only if the MAC address can no longer be reached via AP1. If (accept-priority of AP2) > (hold-priority of AP1), a connection to AP2 will not be accepted.

If omitted, hold-priority is the same as accept-priority. By default, APs, which perform user authentication, have higher priority (lower integer value), than open APs.

dh-groups (list of 19, 20, 21) Identifiers of elliptic curve cryptography groups to use in SAE (WPA3) authentication.

disable-pmkid (no yes; default: | no) For interfaces in AP mode, disables inclusion of a PMKID in EAPOL frames. Disabling PMKID can cause compatibility issues with client devices that make use of it.

yes-Do not include PMKID in EAPOL frames. no  - include PMKID in EAPOL frames.

eap-accounting (no yes; default: | no) Send accounting information to RADIUS server for EAP-authenticated peers.

Properties related to EAP, are only relevant to interfaces in station mode. APs delegate (passthrough) EAP authentication to the RADIUS server.

eap-anonymous-identity (string; default: no Optional anonymous identity for EAP outer authentication. ne)

eap-certificate-mode (dont-verify-certificate Policy for handling the TLS certificate of the RADIUS server. | no-certificates verify-certificate verify- | | certificate-with-crl; default: dont-verify- verify-certificate-require server to have a valid certificate. Check that it is signed by a trusted certificate) certificate authority. dont-verify-certificate-Do not perform any checks on the certificate. no-certificates-Attempt to establish the TLS tunnel by performing anonymous Diffie-Hellman key exchange. To be used if the RADIUS server has no certificate at all. verify-certificate-with-crl-Same as verify-certificate, but also checks if the certificate is valid by checking the Certificate Revocation List.

eap-methods (list of peap, tls, ttls) EAP methods to consider for authentication. Defaults to all supported methods.

eap-password (string; default: none) sensit Password to use, when the chosen EAP method requires one. ive

eap-tls-certificate (certificate; none)default: Name or id of a certificate in the device's certificate store to use, when the chosen EAP authentication method requires one.

eap-username (string; none)default: Username to use when the chosen EAP method requires one.

Take care when configuring encryption ciphers.

All client devices MUST support the group encryption cipher used by the AP to connect, and some client devices (notably, Intel® 8260) will also fail to connect if the list of unicast ciphers includes any they don't support.

encryption (list of  ccmp, ccmp-256, gcmp, A list of ciphers to support for encrypting unicast traffic. gcmp-256, tkip; default: ccmp) Defaults to ccmp.

For a client device to successfully roam between 2 APs, the APs need to be managed by the same instance of RouterOS. For information on how to centrally manage multiple APs, see CAPsMAN

ft (no | yes: default: no)

ft-mobility-domain (integer 0..65535; default: 44484 (0xADC4))

ft-nas-identifier (string of 2..96 hex characters)

ft-over-ds (no yes; default: | no)

ft-preserve-vlanid (no  yes | )

ft-r0-key-lifetime (time interval 1s.. 6w3d12h15m; Default: 600000s (~7 days))

ft-reassociation-deadline (time interval 0.. 70s; default: 20s)

group-encryption (ccmp ccmp-256 gcmp | | | gcmp-256 tkip; default: | ccmp)

group-key-update (time interval; default: 24 hours)

management-encryption (cmac cmac-256 | | gmac gmac-256; default: | cmac)

management-protection (allowed disabled | | required)

multi-passphrase-group (string)

owe-transition-interface (interface auto |)

Whether to enable 802.11r fast BSS transitions ( roaming).

The fast BSS transition mobility domain ID.

Fast BSS transition PMK-R0 key holder identifier. Default: MAC address of the interface.

Whether to enable fast BSS transitions over DS (distributed system).

no-when a client connects to this AP via 802.11r fast BSS transition, it is assigned a VLAN ID according to the access and/or interface settings yes (default) - when a client connects to this AP via 802.11r fast BSS transition, it retains the VLAN ID, which it was assigned during initial authentication

The default behavior is essential when relying on a RADIUS server to assign VLAN IDs to users, since a RADIUS server is only used for initial authentication.

Lifetime of the fast BSS transition PMK-R0 encryption key.

Fast BSS transition reassociation deadline.

Cipher to use for encrypting multicast traffic.

The interval at which the group temporal key (key for encrypting broadcast traffic) is renewed.

Cipher to use for encrypting protected management frames.

Whether to use 802.11w management frame protection. Incompatible with management frame protection in standard wireless package.

The default value depends on the value of the selected authentication type. WPA2 allows the use of management protection, WPA3 requires it.

Name of /interface/wifi/security/multi-passphrase/ group that will be used. Only a single group can be defined under the security profile.

Name of an interface whose MAC address and SSID to advertise as the matching AP when running in OWE transition mode.

Setting the value to 'auto' will make RouterOS try to automatically match open and OWE APs on the same radio.

Required for setting up open APs that offer OWE, but also work with older devices that don't support the standard. See configuration example above.

The passphrase to use for PSK authentication types. Defaults to an empty string - "".

WPA-PSK and WPA2-PSK authentication requires a minimum of 8 chars, while WPA3-PSK does not have a minimum passphrase length.

Due to SAE (WPA3) associations being CPU resource intensive, overwhelming an AP with bogus authentication requests makes for a feasible denial-of-service attack.

This parameter provides a way to mitigate such attacks by specifying a threshold of in-progress SAE authentications, at which the AP will start requesting that client devices include a cookie bound to their MAC address in their authentication requests. It will then only process authentication requests that contain valid cookies.

Rate of failed SAE (WPA3) associations per minute, at which the AP will stop processing new association requests.

passphrase (string of up to 63 characters) sensitive

sae-anti-clogging-threshold ('disabled' int | eger; default: 5)

sae-max-failure-rate ('disabled' integer; | default: 40)

sae-pwe (both hash-to-element hunting- | | Methods to support for deriving SAE password element. and-pecking; default: both)

wps (disabled push-button; default: | push- button) push-button - AP will accept WPS authentication for 2 minutes after 'wps-push-button' command is called. Physical WPS button functionality not yet implemented. disabled-AP will not accept WPS authentication

### Security multi-passphrase properties

/interface/wifi/security/multi-passphrase/

multi-passphrase allows the use of PPSK-private pre-shared keys. Added in 7.17beta1.

It can be used by creating an access list entry and setting multi-passphrase-group name, or by assigning the group to a security profile that the interface uses.

The total limit of supported passphrases is 10000, the limit is shared between all interfaces. When the interface has an associated multi-passphrase group, upon being enabled it will start caching all passphrases from the specified group, while caching is taking place, the authentication will be slower. Once caching is completed there will be no perceptible added delay due to the use of multi-passphrase group.

If an access-list is used to apply multi-passphrase-group, the caching will start upon the first match for the group, and will continue until a match for the passphrase is found.

If there are thousands of entries for possible passphrases under a single group-it might take a few minutes for caching to complete, depending on device configuration and model.

multi-passphrase is not supported for the WPA3-PSK authentication type.

group (string) assigning the group to a security profile or an access list, will enable use of all passphrases defined under it

passphrase (string of The passphrase to use for PSK authentication types. Multiple users can use the same passphrase. up to 63 characters) s ensitive Not compatible with WPA3-PSK.

vlan-id (integer 0.. vlan-id that will be assigned to clients using this passphrase 4095; Default: ) Only supported on wifi-qcom interfaces, if wifi-qcom-ac AP has a client that uses a passphrase that has vlan-id associated with it, the client will not be able to join.

|expires (date and|||The expiration date and time for passphrase specified in this entry, doesn't affect the whole group. Once the date is reached,|
|---|---|---|---|
|time; "YYYY-MM-DD|||existing clients using this passphrase will be disconnected, and new clients will not be able to connect using it. If not set,|
|HH:SS"|||passphrase can be used indefinetly.|
|isolation (yes no|||;|Determines whether the client device using this passphrase is isolated from other clients on AP.|
|Default: no)|||Traffic from an isolated client will not be forwarded to other clients and unicast traffic from a non-isolated client will not be forwarded to an isolated one.|
|disabled (yes no Default: no)|||;||

### Steering properties

Unsolicited 802.11v BSS transition management request functionality is supported stating with 7.21.

Properties in this category govern mechanisms for advertising potential roaming candidates to client devices.

2g-probe-If delay ( no  ye | s Default: no) 1. This property is set to yes on a 2.4GHz AP and

2. said AP is in a steering neighbor group with at least one 5GHz AP then
the 2.4GHz AP will forego responding to the first 3 probe requests from each client in a 60 second interval which have a signal-to-noise ratio of > 35 dB.

neighbor-When sending neighbor reports and BSS transition management requests, an AP will list all other APs within its neighbor group as group (string) potential roaming candidates.

By default, a dynamic neighbor group is created for each set of APs with the same SSID and authentication settings. APs operating in the 5GHz band are indicated to be preferable to ones operating in the 2.4GHz band.

A dynamic neighbor group will not be created if EAP is used, it needs to be defined manually.

rrm (no yes; | Enables sending of 802.11k neighbor reports. Default: yes) The client may request for the "neighbor report" from the AP, when the device wants to "explore/map" its surroundings (the client device can store the report, and it can use it to roam at once or later).

transition-Sets an RSSI threshold for sending unsolicited 802.11v BSS transition management requests. If the client device sits "below" the threshold (inte configured threshold for the duration of transition-threshold-time, it gets marked as a "transition candidate". ger; Default: -80)

transition-Define a time, in seconds, for how long the client device can sit "below" the configured transition-threshold value, to be marked threshold-as "transition candidate". time (time interval; Default: 10)

transition-Defines an interval in seconds, using which, the AP will send unsolicited 802.11v BSS transition management requests to the client request-device, if it is a "transition candidate". period (time interval; E.g., using the default value (30s), a request will be sent to the client every 30 seconds for transition-request-count number of Default: 30) total requests.

transition-Defines how many unsolicited 802.11v BSS transition management requests should be sent out to the client marked as a "transition request-count candidate". x1 request is sent out immediately after the client gets "transition candidate" status ("-1" count), and the remaining "count" (count, will be sent every transition-request-period. unlimited; Default: )3 E.g., using the default value (3), the 1st request gets sent when a client gets "transition candidate" status, the second request gets sent after transition-request-period seconds and the third (last one), after another transition-request-period.

Set to unlimited if you want to send requests with out a count limit.

transition-Defines the time, for how long the client device can be a "transition candidate" before it gets forcefully deauthenticated. It can be a time time (time interval in seconds (to deauthenticate the client after the time, which starts running/counting as soon as the device becomes a interval, "transition candidate", expires), it can be immediate (to instantly deauthenticate the client after it becomes a "transition candidate") or immediate | unlimited (to never force the client and to continue sending transition requests for the transition-request-count amount, unlimited; every transition-request-period seconds). Default: unlimi ted) Note that with **transition-time=immediate**, transition-request-period and transition-request-count become useless, as the client will get deauthenticated instantly after transition-threshold-time.

wnm (no yes | Enables sending of solicited 802.11v BSS transition management requests.; Default: yes) A client may request for a "roaming suggestion" packet that contains "neighbor list", to help the device switch APs. The client device may accept the suggestion and roam at once, or it can ignore the suggestion and keep its current connection.

Please understand that the client can ignore BSS transition management requests. BBS transition request is a "suggestion" for the client to look for other-better signal APs. After receiving the transition request, it is 100% up to the client to decide whether it wants to switch APs or whether it wants to stay connected to the current AP.

Solicited 802.11v BSS transition management request behaviour:

A solicited 802.11v BSS transition management packet is sent to the client, per the client's own request. The client device "asks" the AP to provide a "roaming suggestion" (with a "neighbor list") and the AP responds with a transition request (containing the "neighbor list").

Unsolicited 802.11v BSS transition management request behaviour:

An unsolicited 802.11v request is sent to the client, without waiting for the client to request it. The request gets sent, even if the client was not asking for it.

If the client's signal gets below transition-threshold (default value: -80 dBm) for longer than transition-threshold-time (default value: 10 s), then the client gets marked as a "transition candidate". If the client's signal gets above the transition-threshold, then the client's "transition candidate" status gets removed.

If the client is a "transition candidate", then it will start receiving unsolicited 802.11v BSS transition management request packets (packets "suggesting" to move to other nearby APs). The first such packet will be sent immediately after the client's status changes to the "transition candidate", and the follow-up packets will be sent every transition-request-period (default value: 30 s). The transition-request- count (default value: 3) number of transition requests will be sent out in total, after which, the AP will stop suggesting the transition (unless tra nsition-request-count=unlimited is configured, which makes the AP send out requests non-stop, one request every transition- request-period). After the transition-request-count number is run out, the client will get the next transition request either after the client requests it itself, or after the client gets unmarked and marked as a "transition candidate" again.

The value in transition-time defines for how long the client device can stay as a "transition candidate", before it gets forcefully disconnected. Possible transition-time values: unlimited (to continue sending transition requests using transition-request-period for the amount of transition-request-count and to never forcefully deauthenticate the client), configurable time in seconds (to continue sending transition requests using the transition-request-period interval and transition-request-count number, and then to disconnect the client after the configured transition-time has run out), and immediate (to send a transition request to the client, when it becomes a "transition candidate", and to instantly disconnect it).

### Miscellaneous properties

Property Description

arp (disabled enabled loca | | Address Resolution Protocol mode: l-proxy-arp  | proxy-arp repl | y-only; default: enabled) disabled-the interface will not use ARP enabled-the interface will use ARP local-proxy-arp-the router performs proxy ARP on the interface and sends replies to the same interface proxy-arp-the router performs proxy ARP on the interface and sends replies to other interfaces reply-only-the interface will only reply to requests originated from matching IP address/MAC address combinations which are entered as static entries in the ARP table. No dynamic entries will be automatically stored in the ARP table. Therefore for communications to be successful, a valid static entry must already exist.

arp-timeout (time interval 'a | Determines how long a dynamically added ARP table entry is considered valid since the last packet was received from uto'; default: 30s) the respective IP address. Value auto equals to the value of arp-timeout in /ip settings, which defaults to 30s.

disable-running-check (no y | es; default: no) yes-interface's running property will be true whenever the interface is not disabled no - interface's running property will only be true when it has established a link to another device

disabled (no | yes; default: y es)

mac-address (MAC) MAC address (BSSID) to use for an interface.

Hardware interfaces default to the MAC address of the associated radio interface.

Default MAC addresses for virtual interfaces are generated by

1. Taking the MAC address of the associated master interface
2. Setting the second-least-significant bit of the first octet to 1, resulting in a locally administered MAC address
3. If needed, increment the last octet of the address to ensure it doesn't overlap with the address of another interface on the device
mtu (integer [32..2290]; Layer 3 Maximum transmission unit. Default: 1500)

l2mtu (integer [32..2290]; Layer 2 Maximum transmission unit. Default: 2290)

master-interface (interface; Multiple interface configurations can be run simultaneously on every wireless radio. default: none) Only one of them determines the radio's state (whether it is enabled, what frequency it's using, etc). This  'master' interface, is bound to a radio with the corresponding radio-mac.

To create additional ('virtual') interface configurations on a radio, they need to be bound to the corresponding master interface.

name (string) A name for the interface. Defaults to wifiN, where N is the lowest integer that has not yet been used for naming an interface.

### Read-only properties

Property Description

bound (boolean True for master interfaces that are currently available for WiFi manager. ) (B) True for a virtual interface (configurations linked to a master interface) when both the interface itself and its master interface are not disabled and the master interface has a bound flag.

cap (string) Show information about CAP device if this router is a CAPsMAN and interface does not belong to device itself, but CAPsMAN controlled CAP device.

default-name ( The default name for an interface. string)

inactive (boole False for interfaces in AP mode when they've selected a channel for operation (i.e. configuration has been successfully applied). an) (I) False for interfaces in station mode when they've connected to an AP (i.e. configuration has been successfully applied, and an AP with matching settings has been found).

True otherwise.

master (boolean True for physical interfaces on the router itself or detected CAP if running as CAPsMAN. ) (M) False for virtual interfaces.

radio-mac (MAC The MAC address of the associated radio. )

running (boole True, when an interface has established a link to another device. an) (R) If disable-running-check is set to 'yes', true whenever the interface is not disabled.

### Access List

Filtering parameters

Parameter Description

interface (interface interface-list | | Match if connection takes place on the specified interface or interface belonging to a specified list. any; default: any)

mac-address (MAC address; Match if the client device has the specified MAC address. default: none)

mac-address-mask (MAC address) Modifies the mac-address parameter to match if it is equal to the result of performing bit-wise AND operation on the client MAC address and the given address mask.

Default: FF:FF:FF:FF:FF:FF (i.e. client's MAC address must match value of mac-address exactly)

signal-range (min..max) Match if the strength of the received signal from the client device is within the given range. Allowed values: '-120.. 120'

ssid-regexp (regex) Match if the given regular expression matches the SSID.

time (start-end,days) Match during the specified time of day and (optionally) days of week. Allow values: 0s-1d

multi-passphrase-group (string) Name of /interface/wifi/security/multi-passphrase/ group that will be used. Only single group can be set under one access list entry.

Action parameters

Parameter Description

|allow-signal-out-of-range (time period ||||The length of time which a connected peer's signal strength is allowed to be outside the range required by the|
|---|---|---|---|
|always; default: 0s)|||signal-range parameter, before it is disconnected. If the value is set to 'always', peer signal strength is only checked during association.|
|action (accept reject query-radius; default: accept)|| |||Whether to authorize a connection accept-connection is allowed reject-connection is not allowed query-radius -  connection is allowed if MAC address authentication of the client's MAC address succeeds|
|client-isolation (no yes; default:|||none)|Whether to isolate the client from others connected to the same AP.|
|passphrase (string; tive||none) default: sensi|Override the default passphrase with given value.|
|radius-accounting (no yes; default: ne)|||no|Override the default RADIUS accounting policy with given value.|
|vlan-id ( none integer 1..4095; default: none)||||Assign the given VLAN ID to matched clients.|

### Frequency scan

Information about RF conditions on available channels can be obtained by running the frequency-scan command.

Command parameters

Parameter Description

duration (time interval; none)default: Length of time to perform the scan for before exiting. Useful for non-interactive use.

|default: 1s) number (string; rounds (integer; save-file (string;|freeze-frame-interval (time interval; frequency (list of frequencies/ranges) none)default:|none)default: none)default:||Time interval at which to update command output. Frequencies to perform the scan on. See channel.frequency parameter syntax above for more detail. Defaults to all supported frequencies. Either the name or internal id of the interface to perform the scan with. Required. Number of times to go through list of scannable frequencies before exiting. Useful for non-interactive use. Name of file to save output to.|
|---|---|---|---|---|
|||||Output parameters|
|Parameter||Description|||
|channel (integer) networks (integer) load (integer) nf (integer) max-signal (integer) min-signal (integer) primary (boolean) (P) secondary (boolean) (S) Flat-snoop|||Noise floor (in dBm) of the channel.|Frequency (in MHz) of the channel scanned. Number of access points detected on the channel. Percentage of time the channel was busy during the scan. Maximum signal strength (in dBm) of APs detected in the channel. Minimum signal strength (in dBm) of APs detected in the channel. Channel is in use as the primary (control) channel by an AP. Channel is in use as a secondary (extension) channel by an AP. The '/interface wifi flat-snoop' is a tool for surveying APs and stations. Monitors frequency usage, and displays which devices occupy each frequency. Provides more detailed infromation regarding nearby APs than scan, and offers easy overview of frequency usage by station/AP count. Output parameters|
|Parameter||||Description|
|duration (time interval; Scan command|filter-type (bsss frequency stas | | freeze-frame-interval (time interval; default: 1s)|none)default:)|The scan command takes all the same parameters as the frequency-scan command.|Length of time to perform the scan before exiting. Useful for non-interactive use. bsss-list of active APs and their parameters. frequency-list of station and AP count per scanned frequency stas-a detailed list of stations on each scanned frequency If filter-type is unspecified all types will be returned. Time interval at which to update command output. The '/interface wifi scan' command will scan for access points and print out information about any APs it detects. Output parameters|
|Parameter|Description||||

active (boolean) (A) This signifies that beacons from the AP have been received in the last 30 seconds.

address (MAC) The MAC address (BSSID) of the AP.

channel (string) The control channel frequency used by the AP, its supported wireless standards and control/extension channel layout.

security (string) Authentication methods supported by the AP.

signal (integer) The signal strength of the AP's beacons (in dBm).

ssid (string) The extended service set identifier of the AP.

sta-count (integer) The number of client devices associated with the AP. Only available if the AP includes this information in its beacons.

Sniffer

Command parameters

Parameter Description

duration (time interval; default: no Automatically interrupt the sniffer after the specified time has passed. ne)

filter (string) A string that specifies a filter to apply to captured frames. Only frames matched by the filter expression will be displayed, saved or streamed.

This works similarly to filter strings in libpcap, for example.

The filter can match

Address fields (addr1, addr2, addr3) Wireless frame type and subtype, including shortcuts such as 'beacon' (type == 0 && subtype == 8) Flags (to-ds, from-ds, retry, power, protected)

A string can include the following operators:

== (exact match) != (does not equal) && (logical AND) || (logical OR) () (for grouping filter expressions)

number (interface) Interface to use for sniffing.

pcap-file (string) Save captured frames to a file with the given name. No default value (captured frames are not saved to a file by default).

pcap-size-limit (integer; default: n File size limit (in bytes) when storing captured frames locally. one) When this limit has been reached, no new frames are added to the capture file.

stream-address (IP address; defa Stream captured packets via the TZSP protocol to the given address. No default value (captured packets are not none)ult: streamed anywhere by default).

stream-rate (integer) Limit the rate (in packets per second) at which captured frames are streamed via TZSP.

WPS

interface/wifi/wps-client wifi

Command parameters

Parameter Description

duration (time interval) Length of time after which the command will time out if no AP is found. Unlimited by default.

interval (time interval; default: 1s) Time interval at which to update command output. Default: 1s.

|mac-address (MAC;||none)default:|Only attempt connecting to AP with the specified MAC (BSSID).|
|---|---|---|---|
|number (string;|none)default:||Name or internal id of the interface with which to attempt a connection.|
|ssid (string;|none)default:||Only attempt to connect to APs with the specified SSID.|

Information about the capabilities of each radio can be gained by running the `/interface/wifi/radio print detail` command.

Radios

Property

2g-channels (list of integers)

5g-channels (list of integers)

6g-channels (list of integers)

bands (list of strings)

ciphers (list of strings)

countries (list of strings)

hw-caps (list of strings)

hw-type (string)

max-interfaces (integer)

max-peers (integer)

max-station-interfaces (integer)

max-vlans (integer)

min-antenna-gain (integer)

ml-group (MAC address)

phy-id (string)

radio-mac (MAC)

rx-chains (list of integers)

tx-chains (list of integers)

### Remote CAP

Property

identity (list of integers)

board-name (string)

serial (string)

version (string)

base-mac (MAC address)

Description

Frequencies supported in the 2.4GHz band.

Frequencies supported in the 5GHz band.

Frequencies supported in the 6GHz band.

Supported frequency bands, wireless standards, and channel widths.

Supported encryption ciphers.

Regulatory domains supported by the interface.

Additional supported features (e.g. sniffer, qos-classifier-dscp).

Radio hardware model number.

Maximum number of logical interfaces.

Maximum number of associated peers (connected stations).

Maximum number of logical interfaces in station mode.

Maximum number of different per-user VLANs.

Minimum antenna gain permitted for the interface.

Radios with a common ML (multi-link) group can be configured to take advantage of multi-link operation.

A unique identifier.

MAC address of the radio interface. Can be used to match radios to interface configurations.

IDs for radio chains available for receiving radio signals.

IDs for radio chains available for transmitting radio signals.

Description

IP address of CAP or MAC address used to connect to CAPsMAN

Configured system identity of CAP

Describes the model name

The serial number of CAP

RouterOS version of CAP

Base-MAC provided by CAP in the form: '[XX:XX:XX:XX:XX:XX]'

Information about the remote CAPs can be seen by running the `/interface/wifi/capsman/remote-cap print detail` command.

address(IP address/MAC address%interface)

common-name (string) Common name of the CAP

connected-time (time) Time interval passed since CAP connected to CAPsMAN

uptime (time) Time interval passed since boot-up

### Registration table

The registration table contains read-only information about associated wireless devices.

Parameter Description

authorized (boolean) (A) True when the peer has successfully authenticated.

auth-type (string) Authentication type used for the particular client.

band(string) Band on which particular router is communication with the AP.

bytes (list of integers) Number of bytes in packets transmitted to a peer and received from it.

interface (string) Name of the interface, which was used to associate with the peer.

last-activity (time) last interface data tx/rx activity

mac-address (MAC) The MAC address of the peer.

packets (list of integers) Number of packets transmitted to a peer and received from it.

tx-bits-per-second (integer) Rate of transmitted data to peer per second.

rx-bits-per-second (integer) Rate of received data from peer per second.

rx-rate (string) Bitrate of received transmissions from peer.

signal (integer) Strength of signal received from the peer (in dBm).

ssid (string) The SSID on which client is connected.

tx-rate (string) Bitrate used for transmitting to the peer.

uptime (time interval) Time since association.

vlan-id (integer) VLAN which is assigned by AP or RADIUS for particular peer traffic.

### CAPsMAN Global Configuration

Menu: /interface/wifi/capsman

Property Description

ca-certificate (auto | certificate Device CA certificate, CAPsMAN server requires a certificate, certificate on CAP is optional. name )

certificate (auto | certificate Device certificate name | none; Default: none)

enabled (no yes | ) Disable or enable CAPsMAN functionality

package-path (string) Folder location for the RouterOS packages. For example, use "/upgrade" to specify the upgrade folder from the files section. If an empty string is set, CAPsMAN can use built-in RouterOS packages, note that in this case only CAPs with the same architecture as CAPsMAN will be upgraded.

require-peer-certificate (yes | no; Require all connecting CAPs to have a valid certificate Default: no)

upgrade-policy (none | require-Upgrade policy options same-version | suggest-same- upgrade; Default: none) none-do not perform upgrade require-same-version-CAPsMAN suggests to upgrade the CAP RouterOS version and, if it fails it will not provision the CAP. (Manual provision is still possible) suggest-same-version-CAPsMAN suggests to upgrade the CAP RouterOS version and if it fails it will still be provisioned

interfaces (all | interface name | Interfaces on which CAPsMAN will listen for layer 2 CAP connections none; Default: all)

### CAPsMAN Provisioning

Provisioning rules for matching radios are configured in /interface/wifi/provisioning/ menu:

Property Description

action (create-disabled | Action to take if rule matches are specified by the following settings: create-enabled | create- dynamic-enabled | none; create-disabled-create disabled static interfaces for radio. I.e., the interfaces will be bound to the radio, but the radio Default: none) will not be operational until the interface is manually enabled; create-enabled-create enabled static interfaces. I.e., the interfaces will be bound to the radio and the radio will be operational; create-dynamic-enabled-create enabled dynamic interfaces. I.e., the interfaces will be bound to the radio, and the radio will be operational; none-do nothing, leaves radio in the non-provisioned state;

The basic difference between enabled and dynamic-enabled, is that dynamic interfaces can't be manually edited to override settings and can't be referenced in firewall or other menus, since they will be recreated. In both cases any /interface /wifi/configuration changes will be pushed to CAP automatically.

comment (string) Short description of the Provisioning rule

common-name-regexp (st Regular expression to match radios by common name. Each CAP's common name identifier can be found under "/interface ring) /wifi/radio" as value "REMOTE-CAP-NAME"

supported-bands (2ghz-Match radios by supported wireless modes. This parameter accepts one or more bands as a comma-separated list (for ax | 2ghz-g | 2ghz-n | example, supported-bands=5ghz-ac,5ghz-ax). When multiple bands are specified, the device must support all listed bands 5ghz-a | 5ghz-ac | 5ghz-for the match to succeed and for the defined configuration to be applied. ax | 5ghz-n;)

identity-regexp (string;) Regular expression to match radios by router identity

address-ranges (IpAddre Match CAPs with IPs within the configured address range. Will only work for CAPs that joined CAPsMAN using IP, not MAC ssRange[, address. IpAddressRanges] max 100x;)

master-configuration (stri If action specifies to create interfaces, then a new master interface with its configuration set to this configuration profile will ng) be created

name-format (string) Base string to use when constructing names of provisioned interfaces. Each new interface will be created by taking the base string and appending a number to the end of it, a number will only be appended if the string is not unique.

If included in the string, the character sequence %I will be replaced by the system identity of the cAP, %C will be replaced with the cAP's TLS certificate's Common Name, %R, or %r for lowercase, will be replaced with the CAP's radio MAC

Default: "cap-wifi"

slave-name-format (string) Base string to use when constructing names of virtual interfaces. Each new interface will be created by taking the base string and appending a number to the end of it, a number will only be appended if the string is not unique.

If included in the string, the chraracter sequence %v will be replaced with "virtual", the chraracter sequence %m will be replaced with the name of master interface,if included in the string, the character sequence %I will be replaced by the system identity of the cAP, %C will be replaced with the cAP's TLS certificate's Common Name, %R, or %r for lowercase, will be replaced with the CAP's radio MAC

Default: "master-interface-name-virtual"

radio-mac (MAC address) MAC address of radio to be matched. No default value.

slave-configurations (string If action specifies to create interfaces, then a new slave interface for each configuration profile in this list is created. the ;)

disabled (yes | no ;) Specifies if the provision rule is disabled.

### CAP configuration

Menu: /interface/wifi/cap

Property Description

caps-man-addresses list of IP addresses ( List of Manager comma-separated IP addresses or host names that CAP will attempt to contact during or host names; Default: _capsman._tcp.lan) discovery

caps-man-names () An ordered list of CAPs Manager names that the CAP will connect to, if empty-CAP does not check Manager name

discovery-interfaces (list of interfaces;) List of interfaces over which CAP should attempt to discover Manager

lock-to-caps-man (no | yes; Default: no) Sets, if CAP should lock to the first CAPsMAN it connects to

slaves-static () Creates Static Virtual Interfaces, allows the possibility to assign IP configuration to those interfaces. MAC address is used to remember each static-interface when applying the configuration from the CAPsMAN.

caps-man-certificate-common-names () List of Manager certificate CommonNames that CAP will connect to, if empty-CAP does not check Manager certificate CommonName

certificate () Certificate to use for authenticating

enabled (yes | no; Default: no) Disable or enable the CAP feature

current-caps-man-address () Shows currently used CAPsMAN address (available since 7.15)

current-caps-man-identity () Shows currently used CAPsMAN identity (available since 7.15)

slaves-datapath ()
