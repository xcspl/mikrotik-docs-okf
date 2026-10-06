---
type: Reference
title: "ROSE-storage"
description: "ROSE (RouterOS Enterprise) package adds data center functionality to RouterOS-for supporting disk monitoring, improved formatting with BTRFS and XFS file systems, RAIDs, rsync, iSCSI, NVMe over TCP, NFS. This functionali."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# ROSE-storage

While regular drives are supported, for reliability purposes, we highly recommend using drives that have Power Loss Protection (PLP)

ROSE (RouterOS Enterprise) package adds data center functionality to RouterOS-for supporting disk monitoring, improved formatting with BTRFS and XFS file systems, RAIDs, rsync, iSCSI, NVMe over TCP, NFS. This functionality currently is supported on arm, arm64, x86 and tile platforms.

Storage Type Crypted Properties Example: Simple crypted file system Example: Crypted RAID1 array with integrity check iSCSI Properties Configuration example NFS Properties Configuration example NVME over TCP Properties Example: Mount a disk Linux Client Example: Mount a file as a block device Example: Mount a RAID array Ramdisk Properties Configuration example SMB Properties Configuration example Tmpfs Properties Configuration example RAID Properties Configuration example (RAID6): Example: RAID check RAID 0 RAID 1 RAID 4 RAID 5 RAID 6 RAID Linear Nested RAID Configuration example Setting a hot spare disk Moving your RAID array to a different device RSYNC Properties Configuration example Self-Encryption Drives

## Storage Type

Crypted

|Properties|provide encryption of block devices.|Drive or device used together with type=crypted to make "dm_crypt" encrypted storage. dm-crypt is a transparent disk encryption subsystem designed to|
|---|---|---|
|Property|slot (string; Default:) encryption-key (string; Default:) crypted-backend (string; Default:) Example: Simple crypted file system To create a crypted file-system: After it's created format the file system and it's ready to go.|Description Name of the  file system key used to decrypt Drive or partition to encrypt add crypted-backend=usb1 encryption-key=<secret_key> slot=crypted-usb1 type=crypted disk format crypted-usb1 file-system=ext4 Example: Crypted RAID1 array with integrity check Create a RAID1 array and create a crypted-file system on top of it:|
|/disk and-integrity /disk iSCSI initiator modes. Properties|set nvme3 raid-master=raid1 raid-role=0 set nvme4 raid-master=raid1 raid-role=1 Format the crypted file-system to Btrfs: format crypted-raid1 file-system=btrfs|add raid-device-count=2 raid-type=1 slot=raid1 type=raid add crypted-backend=raid1 encryption-key=<secret_key> slot=crypted-raid1 type=crypted crypt-mode=encryption- iSCSI allows accessing storage over an IP-based network. On initiator iSCSI device will appear as block device. RouterOS supports both target and|
|Property|Description||
|iscsi-address iscsi-export iscsi-iqn iscsi-port||IP address of the iSCSI target. (Host device IP) Disables/enables iSCSI on the host device unique identifier used to name iSCSI target. network port used by the iSCSI target to listen for incoming connections from initiators. The default port for iSCSI traffic is 3260.|

|iscsi-server-iqn iscsi-server-port Host|unique identifier used by the iSCSI server. By default the format for the IQN is iqn.2000-02.com.mikrotik:slot (starting 7.21beta2) network port used by the iSCSI server. (starting 7.21beta2) Configuration example|
|---|---|
|/disk Client|set pcie1-nvme1 iscsi-export=yes|
|/disk|add type=iscsi iscsi-address=192.168.1.1 iscsi-iqn=iqn.2000-02.com.mikrotik:pcie1-nvme1|
|NFS NFS allows sharing local directories over network. RouterOS currently supports NFS v4 only mode. Properties|NFS uses port TCP/2049. If the port is not available in disk print detail you will see the state stuck at  nfs-state="mounting"|
|Property|Description|
|nfs-address nfs-share nfs-sharing Host|IP address of the NFS target. (host device IP) Specify the folder to mount (client parameter) Disable/enable NFS on the host device Configuration example|
|/disk Client|set pcie1-nvme1 nfs-sharing=yes|
|/disk Linux client|add type=nfs nfs-address=192.168.1.1 mkdir /mnt/files mount -t nfs 192.168.1.1:/ /mnt/files|
|Properties|NVME over TCP nvme-tcp allows accessing storage over network as NVMe block device on initiator side. On target side this device can be hdd/ssd/nvme or even raid array.|

|Property||Description|
|---|---|---|
|nvme-tcp-export nvme-tcp-name itive nvme-tcp-port host-name network (Client).|nvme-tcp-address nvme-tcp-host-name nvme-tcp-password sens nvme-tcp-server-allow- nvme-tcp-server- password sensitive nvme-tcp-server-port Example: Mount a disk 1. Use the following commands on Host : 2. Use the following commands on Client :|IP address of the NVME over TCP target. (host device IP) Disable/enable NVME over TCP on the host device This property specifies the hostname of the NVMe over TCP initiator. It can be used for identification and authentication purposes This property specifies the name of the NVMe over TCP target or the connection name for reference purposes (needs to be the same as host slot name) his property is used to specify the password for authenticating the NVMe over TCP connection, ensuring secure access. This property specifies the network port used by the NVMe over TCP target to listen for incoming connections from initiators. The default port for NVMe over TCP traffic is 4420. This property specifies whether the NVMe over TCP server allows connections from specific hostnames, providing a mechanism for host-based access control. This property specifies the password for the NVMe over TCP server, used for authenticating initiators connecting to the target. This property specifies the network port used by the NVMe over TCP server to accept connections from initiators. In this example, one RouterOS device is used as a storage server (Host) and another RouterOS device requires a storage device to be mounted over the /disk set disk1 nvme-tcp-export=yes nvme-tcp-port=4420 /disk add type=nvme-tcp nvme-tcp-address=192.168.1.1 nvme-tcp-name=disk1|
|Linux Client|1. Load kernel module modprobe nvme_tcp|3. Your Client  will now see a disk that is actually mounted over network using NVMe-Over-TCP Use these commands to setup NVM-Over-TCP on a Linux Client. 2. Discover existing NVMe-Over-TCP mounts: nvme discover -t tcp -a 192.168.1.1 -s 4420|

#OUTPUT: Discovery Log Number of Records 1, Generation counter 2 =====Discovery Log Entry 0====== trtype: tcp adrfam: ipv4 subtype: nvme subsystem treq: not specified, sq flow control disable supported portid: 4420 trsvcid: 4420 subnqn: disk1 traddr: 10.155.166.7 sectype: none

3. Connect to the NVMe-Over-TCP mount: nvme connect -t tcp -a 192.168.1.1 -s 4420 -n disk1
4. Block devices now should be available: ls /dev/nvme* #OUTPUT: /dev/nvme0 /dev/nvme0n1 /dev/nvme-fabrics
5. You can now use the mounted block device as any other block device on your Linux Client.
In case you want to disconnect the mounted block device:

nvme disconnect -d /dev/nvme0

Example: Mount a file as a block device

In this example, one RouterOS device is used as a storage server ( Host ) and another RouterOS device requires a storage device to be mounted over the network ( Client ).

Such a setup is useful when you don't want to delegate the whole disk to a Client, but rather give a fraction of the disk size to the Client. Mounting a file rather a disk is going to have a lower performance than mounting a disk (or partition) using NVMe-Over-TCP.

1.  Use the following commands on Host  to create a file that is going to be used as a block device: /disk add type=file file-path=disk1/BIGFILE.img file-size=10G slot=blockdevice1 /disk set blockdevice1 nvme-tcp-export=yes
2. Use the following commands on Client to mount the file as a block device: /disk nvme-discover 192.168.1.1 /disk add nvme-tcp-address=192.168.1.1 nvme-tcp-name=blockdevice1 type=nvme-tcp /disk format blockdevice1 file-system=ext4
3. Your Client will now see a new disk called blockdevice1 even though on the Server the storage device is actually a file. In case you want to mount the block device on a Linux Client, then check the LinuxClient section.

Example: Mount a RAID array

In this example, one RouterOS device is used as a storage server ( Host ) and another RouterOS device requires a storage device to be mounted over the network ( Client ), but also provides data redundancy.

1. Setup a RAID on the Host, for example: /disk add raid-device-count=8 raid-type=6 slot=RAID6_array type=raid /disk set disk1 raid-master=RAID6_array raid-role=0 /disk set disk2 raid-master=RAID6_array raid-role=1 /disk set disk3 raid-master=RAID6_array raid-role=2 /disk set disk4 raid-master=RAID6_array raid-role=3 /disk set disk5 raid-master=RAID6_array raid-role=4 /disk set disk6 raid-master=RAID6_array raid-role=5 /disk set disk7 raid-master=RAID6_array raid-role=6 /disk set disk8 raid-master=RAID6_array raid-role=7 /disk set RAID6_array nvme-tcp-export=yes
2. Use the following commands on Client :
3. Your Client will now see a single disk, but it is actually a highly redundant RAID array. In case you want to mount the block device on a Linux Client, then check the LinuxClient section. Do not mount multiple disks from different RouterOS devices on a Linux Client and put them into a software RAID configuration (for example, mdadm). While this type of configuration does provide some redundancy, you can expect abnormal latency issues or even timeouts. It is recommended to create RAID array on your RouterOS and export the RAID array as a block device to your Linux Client.
Ramdisk

RAMdisk-allows using part of RAM as attached device (block device). If compared to tmpfs-this allows using RAM as part of raid, or any other configuration where device instead of folder is required.

RAMdisk will be cleared on reboot or power loss

Properties

Property Description

ramdisk-size Size of the block device you want to create

Configuration example

/disk add type=ramdisk ramdisk-size=500M

To start using the created ramdisk, you must first format it.

/disk format ramdisk1

|SMB|vulnerabilities) Properties||SMB is a popular file-sharing protocol. ROSE package currently supports SMB2.1 SMB3.0, SMB3.1.1 dialects (SMB1 is not supported due to security|
|---|---|---|---|
||Property||Description|
|Client|smb-address smb-password sensitive smb-share smb-user|Configuration example|IP address of the SMB server SMB password Name of the share you want to connect to SMB user add smb-address=10.155.145.11 smb-share=share1 smb-user=user smb-password=password type=smb|
|Tmpfs|Properties|Server-side configuration can be found-SMB|TMPFS-allows using part of RAM as filesystem (can't be used as block device) Tmpfs will be cleared on reboot or power loss|
||Property||Description|
||tmpfs-max-size|Configuration example add type=tmpfs tmpfs-max-size=10G|Size of the block device you want to create|
||RAID Properties|both by combining them into logical units.|RAID (Redundant Array of Independent Disks) technology allows storing data on multiple drives-improving data transfer performance, data protection or In the case of a RAID disk failure, a rebuild begins automatically once the failed drive is replaced. RouterOS supports software RAID levels 0,1,4,5,6,linear and nested RAID.|
||Property||Description|

raid-type RAID type used (levels 0,1,4,5,6,linear and nested RAID.)

raid-chunk-size The size of the chunks or stripes used in the RAID array.

raid-device-count The number of devices (disks) included in the RAID array.

raid-master Created RAID master block device the disks are added to.

raid-max-component-size The maximum size of an individual component or disk in the RAID array.

raid-member-failed Sets the drive in a failed state in RAID array. Used if there is a need to change a non-failed drive

raid-role Defines the role of each device within the RAID array.

raid-scrub Verifies and repairs data integrity across the RAID array.

Configuration example (RAID6):

This is an example on how to configure RAID, it will be the same procedure in most of RAID types

Create the RAID block device (In this example, RAID 6)

add raid-device-count=20 raid-type=6 slot=raid1 type=raid

Add drives to this raid

set nvme1 raid-master=raid1 raid-role=0 set nvme2 raid-master=raid1 raid-role=1 set nvme3 raid-master=raid1 raid-role=2 set nvme4 raid-master=raid1 raid-role=3 set nvme5 raid-master=raid1 raid-role=4 set nvme6 raid-master=raid1 raid-role=5 set nvme7 raid-master=raid1 raid-role=6 set nvme8 raid-master=raid1 raid-role=7 set nvme9 raid-master=raid1 raid-role=8 set nvme10 raid-master=raid1 raid-role=9 set nvme11 raid-master=raid1 raid-role=10 set nvme12 raid-master=raid1 raid-role=11 set nvme13 raid-master=raid1 raid-role=12 set nvme14 raid-master=raid1 raid-role=13 set nvme15 raid-master=raid1 raid-role=14 set nvme16 raid-master=raid1 raid-role=15 set nvme17 raid-master=raid1 raid-role=16 set nvme18 raid-master=raid1 raid-role=17 set nvme19 raid-master=raid1 raid-role=18 set nvme20 raid-master=raid1 raid-role=19

Format the RAID block device

disk> format raid1 file-system=ext4

And the result should look similar to this

21 BM type=raid slot="raid1" slot-default="" parent=none uuid="f457bc79-7408-489b-8850-85923e900452" fs=ext4 model="RAID6 2-parity-disks" size=17 283 541 893 120 free=17 283 538 190 336 raid-type=6 raid-device-count=20 raid-max- component-size=none raid-chunk-size=1M raid-master=none raid-state="clean" nvme-tcp-export=no iscsi-export=no nfs-sharing=no smb-sharing=no media- sharing=no media-interface=none

Avoid using multiple partitions on a single physical disk in multiple RAID arrays. Using the the same physical disk in multiple RAID arrays can result in low performance.

Example: RAID check

It is extremely important to monitor your RAID array for failures. There are multiple ways to do it, but the simplest way is to create a script that sends an e- mail whenever a RAID member has failed. You can use the following script as an working example:

/system scheduler add interval=30s name=MRaidHealthCheckCall on-event=MraidHealthCheck policy=ftp,read,write,policy,test,sniff start-time=startup /system script add dont-require-permissions=no name=MraidHealthCheck owner=admin policy=ftp,read,write,policy,test,sniff source=":global CheckRAID;\ \n:local sysadmin; \ \n\ \n:set \$sysadmin \"<servername@domain.tld>\";\ \n\ \n:local temp [/disk print count-only where raid-member-failed];\ \n:if ( \$temp > 0 ) do={\ \n :if ( \$CheckRAID < 1 ) do={\ \n /log info message=\"ERROR: RAID has failed!\";\ \n /tool e-mail send to= \$sysadmin subject=([/system identity get name].\" RAID failed\") body=(\"Go check it! Value: \".\$temp);\ \n :set \$CheckRAID 7;\ \n :delay 5s;\ \n }\ \n } \ \n :if ( \$CheckRAID > 0 ) do={\ \n :set \$CheckRAID ( \$CheckRAID -1 );\ \n }\ \n"

You will also need to configure your RouterOS device's e-mail server settings:

/tool e-mail set from=<raidcheck@domain.tld> port=587 server=smtp.domain.com tls=starttls

Make sure you configure your e-mail server's settings under /tool e-mail and change the e-mail address in the script above with the values that matches your e-mail server's settings.

### RAID 0

All data is written evenly over all disks in this RAID, this configuration does not provide any fault tolerance but provides best performance.

### RAID 1

Same data is written in all drives (data is mirrored), this configuration provides best fault tolerance, but performance wise write speeds will be equal to slowest disk used in array.

### RAID 4

Block-level data is striped to a dedicated disk where parity bits are stored. Performance will be limited to a parity writing speed.

### RAID 5

Block-level data is striped evenly over the available disks. Can be recovered from 1 disk failure.

### RAID 6

Block-level data is striped evenly over the available disks. Can be recovered from 2 disk failures.

### RAID Linear

Data is appended over multiple disks combining them into single large disk. Provides no redundancy and is limited to single disk read/write speed.

### Nested RAID

Combination of multiple RAID configurations into other RAID. For example RAID 10 (RAID 1+0) combines disk mirroring (RAID 1) and disk striping (RAID

0)

Configuration example

In this example I'm using 10 SSD drives and configuring in RAID (RAID 1+0)

Create a RAID 0 block

add raid-device-count=3 raid-type=0 slot=raid10 type=raid

Create five RAID 1 blocks, each containing 2 devices and add them to set the master-raid the previously created RAID 0 block (name=raid10)

add raid-device-count=2 raid-master=raid10 raid-role=0 raid-type=1 slot=raid0 type=raid add raid-device-count=2 raid-master=raid10 raid-role=1 raid-type=1 slot=raid1 type=raid add raid-device-count=2 raid-master=raid10 raid-role=2 raid-type=1 slot=raid2 type=raid add raid-device-count=2 raid-master=raid10 raid-role=3 raid-type=1 slot=raid3 type=raid add raid-device-count=2 raid-master=raid10 raid-role=4 raid-type=1 slot=raid4 type=raid

Add drives to each RAID block

set nvme1 raid-master=raid0 raid-role=0 set nvme3 raid-master=raid1 raid-role=0 set nvme5 raid-master=raid2 raid-role=0 set nvme7 raid-master=raid3 raid-role=0 set nvme9 raid-master=raid4 raid-role=0

set nvme2 raid-master=raid0 raid-role=1 set nvme4 raid-master=raid1 raid-role=1 set nvme6 raid-master=raid2 raid-role=1 set nvme8 raid-master=raid3 raid-role=1 set nvme10 raid-master=raid4 raid-role=1

After this format, the raid10 block

format raid10 file-system=ext4

After formating you should see the free space and use the block

23 BM type=raid slot="raid10" slot-default="" parent=none uuid="ec3344f4-1662-49ab-b899-db1aaa217b0f" fs=ext4 model="RAID0 striped" size=9 601 967 652 864 free=9 597 901 369 344 raid-type=0 raid-device-count=5 raid-max-component-size=none raid- master=none raid-state="clean" nvme-tcp-export=no iscsi-export=no nfs-sharing=no smb-sharing=no media-sharing=no media-interface=none

Based on this configuration you can modify the RAID 10 configuration to fit as much storage devices as you require.

Similarly it is possible to create other nested RAID configurations, keeping the same principle as showcased in the example.

### Setting a hot spare disk

It's possible to assign a hot spare disk for your RAID array. In case of a disk failure-the rebuild immediately begins on the assigned spare disk.

Add the RAID array with the desired amount of arrays:

/disk add raid-device-count=4 raid-type=5 type=raid slot=raid5

Afterwards, add the disks to the RAID as well as the spare. In this case we will add NVMe5 as the spare.

/disk set raid-master=raid5 raid-role=0 nvme1 /disk set raid-master=raid5 raid-role=1 nvme2 /disk set raid-master=raid5 raid-role=2 nvme3 /disk set raid-master=raid5 raid-role=3 nvme4

/disk set raid-master=raid5 raid-role=spare nvme5

Moving your RAID array to a different device

It is possible to move your RAID array from one device to another.

In this example we are using a RAID 5 array on an RDS2216 consisting of 4 members.

First, on the "new" device, create a RAID and assign the member slots

# New device /disk add raid-device-count=4 raid-type=5 type=raid slot=raid5

Then, add the currently empty slots to the newly created RAID

# New device /disk set raid-master=raid5 raid-role=0 nvme1 /disk set raid-master=raid5 raid-role=1 nvme2 /disk set raid-master=raid5 raid-role=2 nvme3 /disk set raid-master=raid5 raid-role=3 nvme4

After the RAID has been created and the slots have been assigned to the RAID-on the "old" device, eject the disks you want to switch to the "new" device
