# Getting Started

* [Getting Started](getting-started.md) - Getting Started provides essential instructions for initial RouterOS setup including connection methods, admin interface access, and basic security tasks to bring a MikroTik router into service
* [First Time Configuration](first-time-configuration.md) - This page provides a step-by-step guide for first-time MikroTik RouterOS configuration, covering prerequisites, connection setup, and key concepts like DHCP, NAT, and firewall. It includes both WinBox graphical and
* [Manual Network Setup (No Default Configuration)](manual-network-setup-no-default-configuration.md) - How to manually set up a MikroTik router that has no default configuration: reset to a clean state, create a bridge, assign a LAN IP address, and configure a DHCP server using CLI or WinBox/WebFig
* [Securing your router](securing-your-router.md) - This page provides security recommendations for MikroTik RouterOS, including upgrading RouterOS versions, changing default usernames and passwords, securing access with firewall rules and VPNs, disabling unnecessary

## Networking Fundamentals

* [Networking Fundamentals](networking-fundamentals.md) - This page introduces networking fundamentals in MikroTik RouterOS, covering the OSI and TCP/IP models, their layers, protocols, and Ethernet communication details including MAC addresses and frame forwarding types
* [IPv6 Addresses](ipv6-addresses.md) - This page introduces IPv6 addressing in MikroTik RouterOS, covering its benefits over IPv4, address types and syntax, simplified representation with zero compression, prefix notation, and the absence of broadcast
* [IPv6 Neighbor Discovery](ipv6-neighbor-discovery.md) - RouterOS supports IPv6 Neighbor Discovery and stateless address autoconfiguration by using RADVD, adhering to RFC 4861 and 4862. It enables hosts to automatically configure IPv6 addresses through Router

## Installation and Upgrade

* [Installation and Upgrade](installation-and-upgrade.md) - This section provides guidance on installing and upgrading RouterOS using Netinstall, covering procedures for initial setup or system recovery

## Installation and Upgrade / Install / CHR: Installation

* [CHR: Installation](chr-installation.md) - This page provides an overview of installing and configuring Cloud Hosted Router (CHR) on virtual environments, covering system requirements, RAM calculations, disk image formats, download instructions, VM setup, and
* [CHR: AWS Installation](chr-aws-installation.md) - This page guides users through deploying MikroTik CHR on Amazon Web Services (AWS) by importing a raw disk image as an AMI and launching an EC2 instance
* [CHR: VMWare ESXi Installation](chr-vmware-esxi-installation.md) - This page documents the installation and configuration of MikroTik CHR on VMware ESXi, covering supported network interfaces (vmxnet3, E1000) and disk controllers (IDE, VMware Paravirtual SCSI), along with
* [CHR: Hetzner Cloud Installation](chr-hetzner-cloud-installation.md) - This page provides an overview for deploying MikroTik RouterOS Cloud Hosted Router (CHR) on Hetzner Cloud, detailing the installation process including server creation, rescue system activation, CHR image deployment
* [CHR: Hyper-V Installation](chr-hyper-v-installation.md) - This page documents the installation of MikroTik RouterOS CHR on Microsoft Hyper-V, detailing supported network adapters (synthetic and legacy) and disk controllers (IDE for system disks, SCSI for secondary ones),
* [CHR: Proxmox VE Installation](chr-proxmox-ve-installation.md) - This page provides an overview and detailed installation steps for deploying MikroTik Cloud Hosted Router (CHR) on Proxmox VE virtual environments, covering VM creation, image handling, and configuration methods
* [CHR: Troubleshooting](chr-troubleshooting.md) - This page covers troubleshooting for MikroTik RouterOS CHR, addressing IGMP snooping issues on Linux bridges, VLAN-related data flow problems between guests and the outside world, VLAN tagging requirements in
* [CHR: VirtualBox Installation](chr-virtualbox-installation.md) - This page provides a step-by-step guide for installing MikroTik RouterOS Cloud Hosted Router (CHR) in VirtualBox, covering VM creation, configuration, and initial setup with login instructions
* [CHR: Vultr Installation](chr-vultr-installation.md) - This page guides users through deploying MikroTik CHR on Vultr by first setting up a SystemRescue server, then writing the CHR image to disk using wget and dd commands, and finally connecting via SSH to configure the

## Installation and Upgrade / Install

* [x86 Installation](x86-installation.md) - This page provides a step-by-step guide for installing RouterOS on x86 hardware using USB or Netinstall, covering Windows/Linux/macOS methods, BIOS settings adjustments, and boot priority configurations for

## Installation and Upgrade

* [Upgrade](upgrade.md) - This page documents RouterOS upgrade procedures for MikroTik devices, covering automatic updates with release chains (Long term, Stable, Testing, Development), manual upgrades through WinBox/WebFig/FTP, and

## Installation and Upgrade / Netinstall

* [Netinstall](netinstall.md) - This page introduces Netinstall, the MikroTik utility for installing and reinstalling RouterOS, helps choose between the Windows, Linux, and Netinstall package methods, and describes the common device installation
* [Netinstall for Windows](netinstall-for-windows.md) - This page explains how to install or reinstall RouterOS on MikroTik devices using the Netinstall utility on Windows, covering prerequisites, network preparation with a static IP, booting the device in Etherboot mode,
* [Netinstall for Linux](netinstall-for-linux.md) - This page documents netinstall-cli, the Linux command-line version of the MikroTik Netinstall utility, covering all command-line options for single and multiple device reinstallation, scripting and configuration
* [Netinstall package](netinstall-package.md) - This page documents the RouterOS Netinstall package, which allows reinstalling RouterOS on MikroTik devices remotely from another router running RouterOS 7.24beta1 or newer, covering prerequisites, the

## Installation and Upgrade

* [Packages](packages.md) - RouterOS organizes features into packages with .npk extensions, including the core routeros bundle and optional extras like Containers or The Dude. Wireless devices require specific packages depending on hardware,
* [RouterBOOT](routerboot.md) - RouterBOOT manages RouterOS startup on MikroTik hardware, featuring a main and backup loader with force-backup-booter option. The reset button has multiple functions including configuration reset, CAPs mode

## Configuration Management

* [Configuration Management](configuration-management.md) - This page explains configuration management in MikroTik RouterOS, detailing how to undo and redo actions using the /system/history interface or CLI commands, with examples for firewall rule modifications
* [Backup](backup.md) - The RouterOS backup feature enables saving and restoring router configurations, including MAC addresses, with options for encrypted or unencrypted storage. It supports saving backups to files and loading them back
* [Default Configuration Passwords](default-configuration-passwords.md) - Find the default login credentials for MikroTik RouterOS devices fresh from the factory or after a full reset
* [Default configurations](default-configurations.md) - This page describes default configurations for various MikroTik RouterOS devices, including CPE routers, LTE CPE AP routers, and other interface types. It outlines specific settings for each configuration type, such
* [List of menus with sensitive parameters](list-of-menus-with-sensitive-parameters.md) - This page lists MikroTik RouterOS menus where sensitive parameters such as passwords, keys, and secrets are configured, with links to detailed documentation for each
* [RouterOS configuration reset](routeros-configuration-reset.md) - This page provides comprehensive instructions for resetting MikroTik RouterOS configurations, covering both physical button methods and GUI/CLI commands. It details LED indicators for each reset action, backup loader

## RouterOS Licensing

* [RouterOS License Keys](routeros-license-keys.md) - RouterOS licensing is explained with details on Software ID and System ID for MikroTik hardware, CHR, and x86 systems. Separate guides cover licensing specifics for each platform along with installation instructions

## RouterOS Licensing / Cloud Hosted Router, CHR

* [Cloud Hosted Router, CHR](cloud-hosted-router-chr.md) - Cloud Hosted Router (CHR) is a virtualized RouterOS edition for x8664 environments, offering core routing, firewall, VPN, and management features with guides for installation and licensing
* [CHR: Licensing](chr-licensing.md) - CHR offers four license levels—Free, P1 (Perpetual-1), P10 (Perpetual-10), and P-Unlimited—with trial periods available for paid options. Licenses are perpetual, tied to the CHR system ID, and require periodic

## RouterOS Licensing

* [MikroTik Hardware Licensing](mikrotik-hardware-licensing.md) - MikroTik hardware routers running RouterOS come with pre-installed licenses that determine features like tunnel limits and user sessions. License levels range from trial mode to unlimited functionality, with pricing
* [x86 Licensing](x86-licensing.md) - This page explains x86 system licensing for MikroTik RouterOS, covering license key acquisition, Software ID requirements, system prerequisites, and license level details including features and pricing for trial,

## Software Specifications

* [Software Specifications](software-specifications.md) - This page outlines RouterOS software specifications covering hardware compatibility, installation methods, configuration tools, backup/restore capabilities, firewall features, routing protocols, and MPLS support for
* [Feature support based on architecture](feature-support-based-on-architecture.md) - This page outlines feature support differences across MikroTik RouterOS architectures, listing which features are unsupported or exclusively available for each platform like ARM, MIPS, and PPC. It also references
* [Upgrading to v7](upgrading-to-v7.md) - This page outlines the steps and considerations for upgrading MikroTik RouterOS to version 7, detailing compatibility with features like BGP, OSPF, MPLS, and user manager settings. It highlights mandatory parameters
* [Supout.rif](supoutrif.md) - A supout.rif file is a diagnostic snapshot of the router for MikroTik support. Create it from the CLI, WinBox or WebFig, download it and open it with the Supout.rif viewer
