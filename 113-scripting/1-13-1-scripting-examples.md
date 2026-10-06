---
type: Reference
title: "Scripting examples"
description: "This section contains some useful scripts and shows all available scripting features. Script examples used in this section were tested with the latest 3.x version."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Scripting examples

Introduction Create a file Append text to a file in a new line Check if IP on the interface has changed Strip netmask Resolve host-name Write simple queue stats in multiple files Generate backup and send it by e-mail Check bandwidth and add limitations Block access to specific websites Parse file to add ppp secrets Detect new log entry Allow use of ntp.org pool service for NTP Other scripts

## Introduction

This section contains some useful scripts and shows all available scripting features. Script examples used in this section were tested with the latest 3.x version.

## Create a file

it is not possible to create a file directly, however, there is a workaround:

/file print file=myFile /file set myFile.txt contents=""

## Append text to a file in a new line

There is no direct way to append text to a file, however you can store the old content and append to it in a new line:

:local oldText [/file get test.txt contents as-string] :local addText "test append" :local newText ($oldText."\n".$addText) /file set myFile.txt contents=$newText

## Check if IP on the interface has changed

Sometimes provider gives dynamic IP addresses. This script will compare if a dynamic IP address is changed.

:global currentIP;

:local newIP [/ip address get [find interface="ether1"] address];

:if ($newIP != $currentIP) do={ :put "ip address $currentIP changed to $newIP"; :set currentIP $newIP; }

## Strip netmask

This script is useful if you need an IP address without a netmask (for example to use it in a firewall), but "/ip address get [id] address" returns the IP address and netmask.

:global ipaddress 10.1.101.1/24

:for i from=( [:len $ipaddress] - 1) to=0 do={ :if ( [:pick $ipaddress $i] = "/") do={ :put [:pick $ipaddress 0 $i] } }

Another much more simple way:

:global ipaddress 10.1.101.1/24 :put [:pick $ipaddress 0 [:find $ipaddress "/"]]

## Resolve host-name

Many users are asking features to use DNS names instead of IP addresses for radius servers, firewall rules, etc.

So here is an example of how to resolve the RADIUS server's IP.

Let's say we have the radius server configured:

/radius add address=3.4.5.6 comment=myRad

And here is a script that will resolve the IP address, compare resolved IP with configured one, and replace it if not equal:

/system script add name="resolver" source= {

:local resolvedIP [:resolve "server.example.com"]; :local radiusID [/radius find comment="myRad"]; :local currentIP [/radius get $radiusID address];

:if ($resolvedIP != $currentIP) do={ /radius set $radiusID address=$resolvedIP; /log info "radius ip updated"; }

}

Add this script to the scheduler to run for example every 5 minutes

/system scheduler add name=resolveRadiusIP on-event="resolver" interval=5m

Write simple queue stats in multiple files

Let's consider queue namings are "some text.1" so we can search queues by the last number right after the dot.

:local entriesPerFile 10; :local currentQueue 0; :local queuesInFile 0; :local fileContent ""; #determine needed file count :local numQueues [/queue simple print count-only]; :local fileCount ($numQueues / $entriesPerFile); :if ( ($fileCount * $entriesPerFile) != $numQueues) do={ :set fileCount ($fileCount + 1); }

#remove old files /file remove [find name~"stats"];

:put "fileCount=$fileCount";

:for i from=1 to=$fileCount do={ #create file /file print file="stats$i.txt"; #clear content /file set [find name="stats$i.txt"] contents="";

:while ($queuesInFile < $entriesPerFile) do={ :if ($currentQueue < $numQueues) do={ :set currentQueue ($currentQueue +1); :put $currentQueue; /queue simple :local internalID [find name~"\\.$currentQueue\$"]; :put "internalID=$internalID"; :set fileContent ($fileContent. [get $internalID target-address]. \ " ". [get $internalID total-bytes]. "\r\n"); } :set queuesInFile ($queuesInFile +1);

} /file set "stats$i.txt" contents=$fileContent; :set fileContent ""; :set queuesInFile 0;

}

## Generate backup and send it by e-mail

This script generates a backup file and sends it to a specified e-mail address. The mail subject contains the router's name, current date, and time.

Note that the SMTP server must be configured before this script can be used. See /tool e-mail for configuration options.

/system backup save name=email_backup /tool e-mail send file=email_backup.backup to="me@test.com" body="See attached file" \ subject="$[/system identity get name] $[/system clock get time] $[/system clock get date] Backup"

The backup file contains sensitive information like passwords. So to get access to generated backup files, the script or scheduler must have a 'sensitive' policy.
