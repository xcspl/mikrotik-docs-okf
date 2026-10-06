---
type: Reference
title: "Watchdog"
description: "Software watchdog timer (mostly caused by hardware malfunction) device can recover itself with a reboot; Ping watchdog can monitor connectivity to a specific IP address and trigger the reboot function."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Watchdog

Summary Properties Quick Example

## Summary

Sub-menu: /system watchdog

This menu allows the configuring system to reboot, when a specific IP address does not respond, or when it detects, that the software has locked up. The detection is done in two ways:

Software watchdog timer (mostly caused by hardware malfunction) device can recover itself with a reboot; Ping watchdog can monitor connectivity to a specific IP address and trigger the reboot function.

Note: These are two different Watchdog features and both have their own settings. By default software Watchdog is enabled and ping

Watchdog is disabled. You can enable ping Watchdog by specifying an IP address and you can disable the software Watchdog by unsetting the Watchdog Timer option.

Note: Watchdog reboot is not a system failure. Such reboot also will not generate autosupout file. Watchdog reboot is "/system reboot"

automatically triggered by operating system when some service is not responding as fast as it should. Reasons for that can vary between damaged hardware, slow software implementation for some service, DDoS attack, bad configuration and others.

## Properties

Property Description

auto-send-supout (yes After the support output file is automatically generated, it can be sent by email. | no; Default: no)

automatic-supout (yes When software failure happens, a file named "autosupout.rif" is generated automatically. The previous "autosupout.rif" file is | no; Default: yes) renamed to "autosupout.old.rif".

no-ping-delay (time; Specifies how long will it wait before trying to reach the watch-address. Default: 5m)

ping-timeout (time; Specifies the time interval in which the device will be pinged 6 times (after "no-ping-delay"). Default: 60s)

send-email-from (string The e-mail address to send the support output file from. If not set, the value set in /tool e-mail is used.; Default: )

send-email-to (string; The e-mail address to send the support output file to. Default: )

send-smtp-server (string SMTP server address to send the support output file through. If not set, the value set in /tool e-mail is used.; Default: )

watch-address (IP; The system will reboot, in case 6 sequential pings to the given IP address will fail. If set to none this feature is disabled. By Default: ) default, the router will reboot every 6 minutes if the watch-address is set and not reachable.

watchdog-timer (yes | Whether to reboot if a system is unresponsive for a minute. no; Default: yes)

## Quick Example

To make system generate a support output file and sent it automatically to support@example.com through the 192.0.2.1in case of a software crash:

[admin@MikroTik] system/watchdog/ set auto-send-supout=yes \ \... send-to-email=support@example.com send-smtp-server=192.0.2.1 [admin@MikroTik] system watchdog> print watch-address: none watchdog-timer: yes no-ping-delay: 5m automatic-supout: yes auto-send-supout: yes send-smtp-server: 192.0.2.1 send-email-to: support@example.com
