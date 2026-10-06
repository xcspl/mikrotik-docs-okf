---
type: Reference
title: "Resolve the two ntp pool hostnames :local ntpipa [:resolve $SYSntpa]; :local ntpipb [:resolve $SYSntpb];"
description: "RouterOS manual, section Scripting — Resolve the two ntp pool hostnames :local ntpipa [:resolve $SYSntpa]; :local ntpipb [:resolve $SYSntpb];."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Resolve the two ntp pool hostnames :local ntpipa [:resolve $SYSntpa]; :local ntpipb [:resolve $SYSntpb];

# Get the current settings :local ntpcura [/system ntp client get primary-ntp]; :local ntpcurb [/system ntp client get secondary-ntp];
