---
type: Reference
title: "Clock"
description: "RouterOS uses data from the TZ database, Most of the time zones from this database are included, and have the same names. Because local time on the router is used mostly for timestamping and time-dependent configuration,."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Clock

## Introduction

RouterOS uses data from the TZ database, Most of the time zones from this database are included, and have the same names. Because local time on the router is used mostly for timestamping and time-dependent configuration, and not for historical date calculations, time zone information about past years is not included. Currently, only information starting from 2005 is included.

Following settings are available in the /system clock console path and in the "Time" tab of the "System > Clock" WinBox window.

Startup date and time is jan/02/1970 00:00:00 [+|-]gmt-offset.

## Properties

Property Description

time (HH:MM:SS); where HH - hour 00..24, MM - minutes 00..59, SS-seconds 00..59).

date (mmm/DD/YYYY); where mmm - month, one of jan, feb, mar, apr, may, jun, jul, aug, sep, oct, nov, dec, DD - date, 00..31, YYYY-year, 1970..

2037): date and time show current local time on the router. These values can be adjusted using the set command. Local time cannot, however, be exported, and is not stored with the rest of the configuration.
time-zone-name (manual, Name of the time zone. As most of the text values in RouterOS, this value is case sensitive. Special value manual applies m or name of time zone; anually configured GMT offset, which by default is 00:00 with no daylight saving time. default value: manual);

time-zone-autodetect (yes Feature available from v6.27. If enabled, the time zone will be set automatically. or no; default: yes);

Time-zone-autodetect by default is enabled on new RouterOS installation and after configuration reset. The time zone is detected depending on the router's public IP address and our Cloud servers database. Since RouterOS v6.43 your device will use cloud2.mikrotik.com to communicate with MikroTik's Cloud server. Older versions will use cloud.mikrotik.com to communicate with the MikroTik's Cloud server.

Be aware that the router's internal CPU clock is not a reliable time source for precise timing operations, as its frequency may vary due to power management, thermal conditions, and hardware differences, even between identical models. This variation is expected and does not affect normal router performance. For accurate timekeeping, it is recommended to use network-based time synchronisation, such as NTP (Network Time Protocol).
