---
type: Reference
title: "Use string as a function"
description: "This script checks if the download on an interface is more than 512kbps if true then the queue is added to limit the speed to 256kbps."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Use string as a function

:global printA [:parse ":local A; :put \$A;"]; $printA

## Check bandwidth and add limitations

This script checks if the download on an interface is more than 512kbps if true then the queue is added to limit the speed to 256kbps.

:foreach i in=[/interface find] do={ /interface monitor-traffic $i once do={ :if ($"received-bits-per-second" > 0 ) do={ :local tmpIP [/ip address get [/ip address find interface=$i] address]; # :log warning $tmpIP; :for j from=( [:len $tmpIP] - 1) to=0 do={ :if ( [:pick $tmpIP $j] = "/") do={ /queue simple add name=$i max-limit=256000/256000 dst-address=[:pick $tmpIP 0 $j]; } } } } }

## Block access to specific websites

This script is useful if you want to block certain websites but you don't want to use a web proxy.

This example looks at entries "Rapidshare" and "youtube" in the DNS cache and adds IPs to the address list named "restricted". Before you begin, you must set up a router to catch all DNS requests:

/ip firewall nat add action=redirect chain=dstnat comment=DNS dst-port=53 protocol=tcp to-ports=53 add action=redirect chain=dstnat dst-port=53 protocol=udp to-ports=53

and add firewall

/ip firewall filter add chain=forward dst-address-list=restricted action=drop

Now we can write a script and schedule it to run, let's say, every 30 seconds.

Script Code:

:foreach i in=[/ip dns cache find] do={ :local bNew "true"; :local cacheName [/ip dns cache all get $i name]; # :put $cacheName;

:if (([:find $cacheName "rapidshare"] >= 0) || ([:find $cacheName "youtube"] >= 0)) do={

:local tmpAddress [/ip dns cache get $i address]; # :put $tmpAddress;

# if address list is empty do not check :if ( [/ip firewall address-list find list="restricted"] = "") do={ :log info ("added entry: $[/ip dns cache get $i name] IP $tmpAddress"); /ip firewall address-list add address=$tmpAddress list=restricted comment=$cacheName; } else={ :foreach j in=[/ip firewall address-list find list="restricted"] do={ :if ( [/ip firewall address-list get $j address] = $tmpAddress ) do={ :set bNew "false"; } } :if ( $bNew = "true" ) do={ :log info ("added entry: $[/ip dns cache get $i name] IP $tmpAddress"); /ip firewall address-list add address=$tmpAddress list=restricted comment=$cacheName; } } } }

## Parse file to add ppp secrets

This script requires that entries inside the file are in the following format:

username,password,local_address,remote_address,profile,service

For example:

janis,123,1.1.1.1,2.2.2.1,ppp_profile,myService juris,456,1.1.1.1,2.2.2.2,ppp_profile,myService aija,678,1.1.1.1,2.2.2.3,ppp_profile,myService

:global content [/file get [/file find name=test.txt] contents]; :global contentLen [ :len $content];

:global lineEnd 0; :global line ""; :global lastEnd 0;

:do { :set lineEnd [:find $content "\r\n" $lastEnd]; :set line [:pick $content $lastEnd $lineEnd]; :set lastEnd ( $lineEnd + 2 );

:local tmpArray [:toarray $line]; :if ( [:pick $tmpArray 0] != "" ) do={ :put $tmpArray; /ppp secret add name=[:pick $tmpArray 0] password=[:pick $tmpArray 1] \ local-address=[:pick $tmpArray 2] remote-address=[:pick $tmpArray 3] \ profile=[:pick $tmpArray 4] service=[:pick $tmpArray 5]; } } while ($lineEnd < $contentLen)

## Detect new log entry

This script is checking if a new log entry is added to a particular buffer.

In this example we will use PPPoE logs:

/system logging action add name="pppoe" /system logging add action=pppoe topics=pppoe,info,!ppp,!debug

Log buffer will look similar to this one:

[admin@mainGW] > /log print where buffer=pppoe 13:11:08 pppoe,info PPPoE connection established from 00:0C:42:04:4C:EE

Now we can write a script to detect if a new entry is added.

:global lastTime;

:global currentBuf [ :toarray [ /log find buffer=pppoe]]; :global currentLineCount [ :len $currentBuf]; :global currentTime [ :totime [/log get [ :pick $currentBuf ($currentLineCount -1)] time]];

:global message "";

:if ( $lastTime = "" ) do={ :set lastTime $currentTime; :set message [/log get [ :pick $currentBuf ($currentLineCount-1)] message];

} else={ :if ( $lastTime < $currentTime ) do={ :set lastTime $currentTime; :set message [/log get [ :pick $currentBuf ($currentLineCount-1)] message]; } }

After a new entry is detected, it is saved in the "message" variable, which you can use later to parse log messages, for example, to get the PPPoE client's mac addresses.

## Allow use of ntp.org pool service for NTP

This script resolves the hostnames of two NTP servers, compares the result with the current NTP settings, and changes the addresses if they're different. This script is required as RouterOS does not allow hostnames to be used in the NTP configuration. Two scripts are used. The first defines some system variables which are used in other scripts and the second does the grunt work:
