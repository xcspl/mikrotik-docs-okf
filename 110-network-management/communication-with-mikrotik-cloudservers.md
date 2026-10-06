---
type: Reference
title: "Communication with MikroTik Cloud/Servers"
description: "RouterOS manual, section Network Management — Communication with MikroTik Cloud/Servers."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Communication with MikroTik Cloud/Servers

This table lists information about all connections that can occur from RouterOS to MikroTik servers, as well as instructions on how to disable such

|connections.||||
|---|---|---|---|
|Sub-menu|Domain name|by default|Ensuring communication is disabled/inactive|
|system clock time-|cloud2.|Yes|system/clock/set time-zone-autodetect=no (more info)|
|zone-autodetect|mikrotik.com|||
|system backup cloud|cloud2. mikrotik.com|No|Communication is only invoked by upload-file, download-file, remove-file commands. (more info)|
|ip cloud update-time|cloud2. mikrotik.com|Yes|ip cloud/set update-time=no (more info)|
|ip cloud ddns-enabled|cloud2. mikrotik.com|No|ip cloud/set ddns-enabled=auto (more info)|
|ip cloud back-to-home-|cloud2.|No|ip cloud/set back-to-home-vpn=revoked-and-disabled (more info)|
|vpn|mikrotik.com|||
|ip cloud back-to-home-|cloud2.|No|Communication is only invoked by enabling or disabling file sharing in "ip cloud back-to-home-file". (mor|
|file|mikrotik.com||e info)|
|system license|licence. mikrotik.com|for CHRs)|In the case of CHRs, it is impossible to disable communication with the license server using a specific command or setting in RouterOS. (more info)|
|interface lte firmware-|upgrade.|No|Communication is only invoked by firmware-upgrade command. (more info)|
|upgrade|mikrotik.com|||
|interface detect-internet|cloud.mikrotik.|No|interface/detect-internet/set detect-interface-list=none (more info)|
||com|||
|system package update|upgrade. mikrotik.com|No|Communication is only initiated by the check-for-updates command and by downloading packages from the upgrade server. (more info)|
|system swos upgrade|upgrade. mikrotik.com|No|Communication is only invoked by upgrade command. (more info)|

Enabled/Active

Yes (relevant only
