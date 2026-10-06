---
type: Reference
title: "Define a variable so we know if anything's changed. :local changea 0; :local changeb 0;"
description: "RouterOS manual, section Scripting — Define a variable so we know if anything's changed. :local changea 0; :local changeb 0;."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Define a variable so we know if anything's changed. :local changea 0; :local changeb 0;

# Debug output :put ("Old: ". $ntpcura. " New: ". $ntpipa); :put ("Old: ". $ntpcurb. " New: ". $ntpipb);

# Change primary if required :if ($ntpipa != $ntpcura) do={ :put "Changing primary NTP"; /system ntp client set primary-ntp="$ntpipa"; :set changea 1; }

# Change secondary if required :if ($ntpipb != $ntpcurb) do={ :put "Changing secondary NTP"; /system ntp client set secondary-ntp="$ntpipb"; :set changeb 1; }

# If we've made a change, send an e-mail to say so. :if (($changea = 1) || ($changeb = 1)) do={ :put "Sending e-mail."; /tool e-mail send \ to=$SYSsendemail \ subject=($SYSname. " NTP change") \ from=$SYSmyemail \ server=$SYSemailserver \ body=("Your NTP servers have just been changed:\n\nPrimary:\nOld: ". $ntpcura. "\nNew: " \. $ntpipa. "\n\nSecondary\nOld: ". $ntpcurb. "\nNew: ". $ntpipb); }

Scheduler entry:

/system scheduler add \ comment="Check and set NTP servers" \ disabled=no \ interval=12h \ name=CheckNTPServers \ on-event=setntppool \ policy=read,write,test \ start-date=jan/01/1970 \ start-time=16:00:00

## Other scripts

Dynamic_DNS_Update_Script_for_EveryDNS Dynamic_DNS_Update_Script_for_ChangeIP.com UPS Script
