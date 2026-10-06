---
type: Reference
title: "Old device /disk eject nvme1 /disk eject nvme2 /disk eject nvme3 /disk eject nvme4"
description: "Finally, you can remove the disks from the \"old\" device and insert them in the assigned slots in the \"new\" one. RouterOS will automatically detect a RAID superblock and mount the array without any additional input."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Old device /disk eject nvme1 /disk eject nvme2 /disk eject nvme3 /disk eject nvme4

Finally, you can remove the disks from the "old" device and insert them in the assigned slots in the "new" one. RouterOS will automatically detect a RAID superblock and mount the array without any additional input.

## RSYNC

rsync (Remote Sync) is a powerful file synchronization and file transfer program used in Unix-based systems. It allows for efficient transfer and synchronization of files and directories between different systems or within the same system. If you make changes in a file only changes to files are transferred, reducing data transfer volume. RouterOS RSYNC implementation uses ipsec for data transfer (if password is set). When configured you will see dynamic ipsec entries.

Rsync settings can be found in file/sync menu

Port TCP/8291 is used for the control connection (if not open in the status (file sync print) you will be stuck at making control connection to 192.1

68.88.2) Port UDP/500 and protocol 50 (ipsec-esp) is used to create a secure connection and start the transfer (if not open in the status (file sync print) you will be stuck at initializing transfer)
IPSec dynamic entry example:

# PEER TUNNEL SRC-ADDRESS DST-ADDRESS PROTOCOL ACTION LEVEL PH2-COUNT ;;; file-sync-10.155.145.11 1 D file-sync-10.155.145.11 no 10.155.145.17/32 10.155.145.11/32 tcp encrypt require 1

/ip/ipsec/peer> print 0 D name="file-sync-10.155.145.11" address=10.155.145.11/32 local-address=10.155.145.17 profile=default exchange-mode=main send-initial-contact=yes /ip/ipsec/identity> print 0 D ;;; file-sync-10.155.145.11 peer=file-sync-10.155.145.11 auth-method=pre-shared-key secret="secret" generate-policy=no

Properties

Property Description

local-path File/folder path. Used for mode Upload to set the path of the file/folder to upload to the device

mode Sets if you want to download/upload the file (direction of the sync)

password Target device password

remote-address Target devices IP

remote-path File/folder path. Used with mode download to set the path of the target device to be downloaded

user Target device password

Configuration example

Basic configuration is really easy, on the host device you need to add the file you want to sync to another device, the ip, user/password and the mode.

/file sync add local-path=/ipv6route.txt.rsc mode=upload remote-address=192.168.88.2 remote-path=RAID/

If configured correctly, you will see on the host device:

0 192.168.88.2 upload /ipv6route.txt.rsc RAID/ in sync

And on the client device:
