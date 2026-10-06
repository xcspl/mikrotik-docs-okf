---
type: Reference
title: "REMOTE-ADDRESS MODE LOCAL-PATH REMOTE-PATH STATUS 0 D 192.168.88.1 download RAID/ /ipv6route.txt.rsc in sync"
description: "RouterOS manual, section Hardware — REMOTE-ADDRESS MODE LOCAL-PATH REMOTE-PATH STATUS 0 D 192.168.88.1 download RAID/ /ipv6route.txt.rsc in sync."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# REMOTE-ADDRESS MODE LOCAL-PATH REMOTE-PATH STATUS 0 D 192.168.88.1 download RAID/ /ipv6route.txt.rsc in sync

## Self-Encryption Drives

For using SED-drives have to be Opal-compliant. Please consult drive manufacturers documentation to find out if particular drive supports this feature before buying drives. RouterOS adds o (supported inactive) or O (supported active) flags for supported drives:

/disk print Flags: B-BLOCK-DEVICE; M, F-FORMATTING; o-TCG-OPAL-SELF-ENCRYPTION-SUPPORTED Columns: SLOT, MODEL, SERIAL, INTERFACE, SIZE, FREE, FS, RAID-MASTER # SLOT MODEL SERIAL INTERFACE SIZE FREE FS RAID 0 BMo sata1 Samsung SSD 860 2.5in S3Z9NX0N414510L SATA 6.0 Gbps 1 000 204 886 016 983 351 111 680 ext4 none 1 BMo sata2 Samsung SSD 860 S5GENG0N307602J SATA 6.0 Gbps 1 000 204 886 016 983 351 128 064 ext4 none 2 BMO sata3 Samsung SSD 860 S5GENG0N307604H SATA 6.0 Gbps 1 000 204 886 016 983 351 128 064 ext4 none 3 BMO sata4 Samsung SSD 860 2.5in S4CSNX0N838150B SATA 6.0 Gbps 1 000 204 886 016 983 351 128 064 ext4 none

To set TCG-OPAL-SELF-ENCRYPTION:

|/disk disk set sata1 self-encryption-password=securepassword|
|---|
|/disk disk unset sata1 self-encryption-password|
|/disk disk set sata1 !self-encryption-password|

to unset:

or
