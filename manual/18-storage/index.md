# Storage

* [Storage](storage.md) - This page documents RouterOS storage features including disk encryption, RAID configurations, Btrfs/XFS filesystems, network protocols like iSCSI and NFS, media sharing via DLNA, file synchronization with rsync, and

## index

* [index](index.md) - Btrfs is a stable copy-on-write file system with features like bitrot protection, subvolumes, and snapshots. It is available with the Storage package and supports RAID configurations, subvolume management, and
* [Btrfs maintenance](btrfs-maintenance.md) - This page covers Btrfs maintenance tasks including periodic scrubbing to detect and correct data corruption in RAID arrays, balancing to optimize storage space usage, and creating snapshots for data recovery. It
* [raid](raid.md) - This page provides step-by-step instructions for setting up a Btrfs RAID1 array using two disks in RouterOS, covering disk preparation, formatting, adding devices, balancing data, and ensuring consistent RAID profiles
* [Btrfs subvolumes and snapshots](btrfs-subvolumes-and-snapshots.md) - This page guides users through creating Btrfs subvolumes and snapshots in RouterOS, explaining how to organize data, format disks, set up subvolumes like Documents and Photos, and create snapshots for efficient
* [DLNA Media Server](dlna-media-server.md) - The DLNA media server shares video, music and picture files from a disk folder with TVs, phones and players on one interface. It covers limiting a server to one device, the servers that disk sharing creates, and how
* [Encrypted storage (dm-crypt)](encrypted-storage-dm-crypt.md) - Encrypted storage (dm-crypt) enables transparent disk encryption for block devices in RouterOS, configured with type=crypted and an encryption key. Examples show creating encrypted file systems on USB drives or on
* [iSCSI](iscsi.md) - iSCSI enables IP-based storage access with RouterOS supporting both target and initiator modes, featuring properties like iscsi-address, IQN identifiers, and configurable ports for both client and server roles
* [NFS](nfs.md) - NFS enables network directory sharing in RouterOS using NFS v4, requiring the Storage package. It uses port TCP/2049 and is configured via the nfs-sharing, nfs-address and nfs-share arguments of /disk
* [NVMe over TCP](nvme-over-tcp.md) - NVMe over TCP enables network-attached NVMe storage access for both initiators and targets, with configurable IP addresses, ports, and host-based access control. Examples show mounting a disk from a RouterOS client

## RAID

* [RAID](raid-2.md) - RAID technology in RouterOS enables data storage across multiple drives with improved performance and protection, supporting RAID levels 0,1,4,5,6, linear, and nested configurations. Includes configuration examples
* [Setting a hot spare disk](setting-a-hot-spare-disk.md) - This page explains how to configure a hot spare disk for a RAID array in RouterOS, enabling automatic rebuild on disk failure by assigning a spare disk to the RAID setup
* [Moving your RAID array to a different device](moving-your-raid-array-to-a-different-device.md) - This page explains how to move a RAID 5 array from an old device to a new one by creating the RAID on the new device, ejecting disks from the old device, and transferring them to the new device where RouterOS
* [Ramdisk](ramdisk.md) - A ramdisk is a block device in RAM. Format it before use, or use it as a RAID member. It needs the rose-storage package and is empty after every reboot
* [Rsync](rsync.md) - Rsync in RouterOS allows efficient file synchronization between systems, with configurable local/remote paths and modes for upload/download. Dynamic IPsec entries are created when a password is set, ensuring secure
* [Self-encrypting drives (SED)](self-encrypting-drives-sed.md) - RouterOS supports Self-Encrypting Drives (SED) using the TCG-Opal standard, requiring the Storage package. Supported drives show o (inactive) / O (active) flags in /disk/print, and encryption can be enabled with
* [SMB](smb.md) - RouterOS includes a built-in SMB server for file sharing over SMB/CIFS protocols, supporting SMB2.1, 3.0, and 3.1.1. Users can configure server settings, shares, and user permissions through /ip/smb, /ip/smb/shares,
* [SSHFS](sshfs.md) - SSHFS allows mounting a folder from a remote SSH server as a local disk in RouterOS, using the sshfs type of /disk. The mount is configured with the remote address, user credentials, and path, and appears in /file
* [Tmpfs](tmpfs.md) - A tmpfs is a folder in RAM for temporary files such as packet captures and downloads. Its size is capped, and its contents are lost on reboot
