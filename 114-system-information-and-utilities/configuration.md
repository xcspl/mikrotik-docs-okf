---
type: Reference
title: "Configuration"
description: "dst-active (yes or no; read-only property): This property has the value yes while daylight saving time of the current time zone is active. gmt-offset ( + - HH:MM-offset in hours and minutes; read-only property): This is ."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Configuration

### Active time zone information

dst-active (yes or no>; read-only property): This property has the value yes while daylight saving time of the current time zone is active. gmt-offset ([ |] + - HH:MM-offset in hours and minutes; read-only property): This is the current value of GMT offset used by the system, after applying base time zone offset and active daylight saving time offset.

### Manual time zone configuration

These settings are available in /system clock manual console path and in the "Manual Time Zone" tab of the "System > Clock" WinBox window. These settings have an effect only when time-zone-name=manual. It is only possible to manually configure single daylight saving time period.

time-zone, dst-delta ([ |] + - HH:MM - time offset in hours and minutes, leading plus sign is optional; default value: +00:00) : While DST is not active use GMT offset time-zone. While DST is active use GMT offset time-zone + dst-delta. dst-start, dst-end (mmm/DD/YYYY HH:MM: SS - date and time, either date or time can be omitted in the set command; default value: jan/01/1970 00:00:00): Local time when DST starts and ends.
