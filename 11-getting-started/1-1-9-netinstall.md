---
type: Reference
title: "Netinstall"
description: "Netinstall is a tool for installing and reinstalling MikroTik devices running RouterOS."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Netinstall

Introduction Device installation workflow using Netinstall: Device configuration scripts: Netinstall for Windows Netinstall for Linux Quick start guide for Windows Quick start guide for Linux Etherboot Reset button RouterOS Serial console

## Introduction

Netinstall is a tool for installing and reinstalling MikroTik devices running RouterOS.

Always reinstall device using Netinstall if you suspect that your device is not working properly.

The tool is available for Windows with a graphical interface and for Linux command line tool.

Be careful. Netinstall re-formats the system's drive, all configuration and user files will be lost.

Netinstall does not erase the RouterOS license key, nor does it reset RouterBOOT related settings, for example, CPU frequency is not changed during reinstalling the device.

### Device installation workflow using Netinstall:

prepare and start Netinstall host on same L2 network segment where re-installable device will be connected, preferable dedicated NIC and hub /switch to avoid IP/DHCP/BOOTP conflict caused by other devices on same network boot device from Netinstall by holding Reset button till device is detected by Netinstall. As alternative device RouterBOOT can be configured for network boot, during which device will boot to Netinstall Install device using specified packages and configuration scripts During next boot device applies configuration parameters specified in Netinstall

### Device configuration scripts:

Configure script-installs on device custom default configuration script which replaces with RouterOS supplied default configuration script. The script can access factory set passwords with read-only variables $defconfPassword and $defconfWifiPassword starting from RouterOS 7.10beta8.

Mode script-puts on device one‑time custom script to run on the device’s first boot after installation. This script can be used to configure device‑mode and protected‑routerboot  and other settings during device initial configuration.

Configure and Mode scripts have a maximum execution timeout of 120 seconds.

Configure script will be kept during RouterOS updates and used after further configuration resets till device will be reinstalled with new script or removed if no script provided.

Mode script feature requires RouterOS and Netinstall version 7.22 or newer.

Configure and Mode scripts are regular/import file, accepts valid MikroTik RouterOS CLI commands.

For more reference see:

RouterOS configuration management RotuerOS packages RouterBOOT configuration

MikroTik downloads

## Netinstall for Windows

The available actions and parameters are as follows:

Controls Description /Actions

Netbooting Allows to Enable, Disable and configure  IP addressing for Netinstall build-in in BOOTP and TFPT server required for netbooting MikroTik device using Netinstall client

Shutdown Performs shutdown of selected MiktoTik device booted to Netinstall

Reboot Performs reboot of selected MiktoTik device booted to Netinstall

Install Performs MiktoTik device Netinstall using selected options

Cancel Cancel current in progress installation

Routers Device selection for Netinstall. /Drives For device to appear in list device must be started to Netinstall mode

Packages Allows to specify location where RouterOS packages files are located and create package sets  for next installations

Netinstall Description parameters

Auto reboot Set action what is performed after device installation is successfully completed

Software ID Displays current device Software ID

Key Allows to specify and install new license key during installation.

By default Netinstall will keep detected license key from device.

Keep old Instruct Netinstall to read and restore device core configuration (/export; /users) after device installation. configuration This options does not keep user files, containers etc.

Keep branding Instruct Netinstall to keep device branding package if it present on device.

Factory installed branding packages can not be discarded and always will be kept.

Apply default If set,  after device installation and reboot device will apply default configuration script. config /system/default-configuration/script/print

Configure script Allows during device installation to install on device custom default configuration script which replaces with RouterOS supplied default configuration script.

/system/default-configuration/custom-script/print

This script will be kept during RouterOS updates and used after further configuration resets till device will be reinstalled with new script or removed if no script provided.

Mode script Specifies a one‑time custom script to run on the device’s first boot after installation.

Use this script  to configure device‑mode and protected‑routerboot and other settings during device deployment.

Mode script executes before any custom or default configuration scripts. Upon completion, script is automatically removed from the device. If the script modifies the device-mode, the device will be reboot immediately after execution.

This feature requires RouterOS and Netinstall version 7.22 or newer.

IP address Netinstall will autocreate Configure script with specified parameters for initial device configuration using IPv4 connectivity or serial Gateway console. Baudrate Parameter available only when device is Installed to empty configuration, eg no other configuration option options specified.

## Netinstall for Linux

The Netinstall Linux version netinstall-cli is a command line tool, which offers nearly the same parameters as the Windows counterpart.

The tool requires root privileges and must be run as root or use sudo.

Command line:

*netinstall-cli* [-r] [-e] [-b] [-m [-o]] [-f] [-k <keyfile>] [-s <userscript>] [-sm <modescript>] [--mac <mac address>] {-i <interface> | -a <client-ip>} [PACKAGES]

Available actions and parameters are as follows:

Parameter Meaning

-r Reinstall device and apply default configuration script.

-e Reinstall device without applying default configuration script-leave device with empty config

-b Option to discard the currently installed branding package from the device, otherwise it will kept

-m Enables multiple device reinstallation.

Available options:

No "-m", no "-o" chosen – Only one successful installation will proceed, and Netinstall will close afterward.

"-m" only – Enables multiple device reinstallation. The same device will be reinstalled as many times as BOOTP requests are sent.

"-o" only – Functions the same as when neither "-m" nor "-o" is chosen: only one successful installation will proceed, and Netinstall will close afterward.

Both "-m" and "-o" – Enables multiple device reinstallation. The same device will be reinstalled only once per Netinstall run.

-o When using the netinstall tool with the "-o" option, devices can only be installed once per netinstall run. This means that during the netinstall process, the tool will keep track of the MAC addresses of devices that were successfully installed. If a device with the same MAC address tries to reinstall during the same run, the tool will ignore it and not  respond to its BOOTP requests.

-f Ignore size constraints. Netinstall-cli checks the storage size on the router. If the total size of the selected packages exceeds the device's available storage, an error will be displayed: "Ignoring XX:XX:XX:XX:XX:XX, not enough space (override with -f)"

-c Allow to run multiple Netinstall instances on the same computer.

-v Verbose mode

-k <keyfile> Provides the device with a license key in .KEY format (optional).

-s Specifies Configure script to be installed on device, this replaces replaces with RouterOS supplied default configuration script. <userscript> /system/default-configuration/custom-script/print

This script will be kept during RouterOS updates and used after further configuration resets till device will be reinstalled with new script or removed if no script provided.

-sm Specifies a one‑time custom script to run on the device’s first boot after installation. <modescript> Use this script  to configure device‑mode and protected‑routerboot and other settings during device deployment.

Mode script executes before any custom or default configuration scripts. Upon completion, script is automatically removed from the device. If the script modifies the device-mode, the device will be reboot immediately after execution.

This feature requires RouterOS and Netinstall version 7.22 or newer.

--mac <mac Specifies MAC address which will be allowed to be installed. When a MAC address is provided, all other BOOTP requests are address> disregarded.

-i Allows you to specify an interface (optional). <interface>

-a <IP Uses a specific IP address that the Netinstall server will assign to the device. Mandatory, but can be auto-assigned if interface parameter address> used.

PACKAGE Specify a list of RouterOS.NPK format packages that Netinstall will try to install on the device (mandatory). The system package must be listed first.

If the "-r" or "e-" parameter is not specified, netinstall-cli will reinstall RouterOS  and will keep the current configuration by downloading current configuration database from the router, reinstalling the router (including disk formatting), and uploading the configuration back to it, the same as  Netinstall "Keep old configuration" option. However, it's important to note that this process solely applies to the configuration itself and does not impact the files, including databases like the User Manager database, Dude database, and others.

## Quick start guide for Windows

Download the Stable or Testing version of the Netinstall from the utility downloads page; Download the RouterOS Main package from the downloads page;

You need to select a RouterOS version, preferably one marked as Stable. (ARM, Additionally, choose the appropriate architecture MIPS, SMIPS, TILE, etc.). If unsure, you can download the RouterOS package for all architectures, and Netinstall will determine the correct one for your device.

Disable all computer network interfaces (WiFi, Ethernet, LTE, or any other type of connection) except for the one to be used for installation. Netinstall will only function with one active interface on your computer. It's strongly recommended to deactivate any other network interfaces to ensure Netinstall selects the correct one. Configure a static IP address for your Ethernet interface, open Start, and select Settings:

Netinstall can run also on a local network, in such case you could skip setting a static IP address, but it is highly recommended that you set a static IP address if you are not familiar with Netinstall.

Open Network & Internet and select Change adapter options

on your Ethernet interface and select Right-click Properties

Select Internet Protocol Version 4 (TCP/IPv4) and click Properties

Check Use the following IP address and fill out the fields as shown in the image below

Open your Downloads folder (or wherever you saved the downloaded files) and extract the Netinstall *.zip file to a convenient place

Make sure that the Ethernet interface is running and launch Netinstall.exe. If you followed the guide precisely, then you should not have any Internet connection on your computer, Windows 10 wants to verify all apps that it runs, but will not be able to do it since lack of an Internet connection, for this reason, a warning might pop up, you should click Run.

Netinstall requires administrator rights, there should be a window asking for permissions to run Netinstall, you must accept these permissions in order for Netinstall to work properly.

Allow access for Netinstall in Public networks and configure Net booting settings and fill out the required fields as shown in the image below

The Client IP address must be unique! Don't use an existing IP address in your network, this also means that you should not use the computer's IP address as well. Use a completely different IP address from the same subnet.

Connect your device to your computer using an ethernet cable directly (without any other devices in-between), plug the Ethernet cable into your device's Etherboot port (see the next "Warning" in this article before connecting your Netinstall network). MikroTik devices are able to use Netinstall from their first port (Ether1), or from the port marked with "BOOT".

Some computers have a network interface (especially USB Ethernet adapters) that tend to create an extra link flap, which is enough for Netinstall to fail to detect a device that is in Etherboot mode. In such a case you can use a switch between your device and your computer or a router in bridge mode to prevent this issue. If you use RouterOS powered router in bridge mode, then make sure that you disable any DHCP clients on the router bridge interface and disable Detect Internet feature.

Netinstall uses bootp packets, which are using the same port numbers as DHCP packets. If you're using a switch between your PC and the device to be Netinstalled, ensure that the ports in the bridge are not blocked by other network devices.

If you have dhcp-snooping enabled, make sure to enable "trusted" on the bridge ports facing the Netinstall PC.

Power up your device and put it into etherboot mode

There are multiple ways how to put your device into Etherboot mode. Make sure you read the Etherboot manual before trying to put the device into this mode. Methods vary between different MikroTik devices.

Wait for the device to show up in Netinstall, then select it and click Browse. Navigate to your Downloads folder (or wherever you saved your RouterOS packages) and press OK.

Select your desired RouterOS packages and press Install. Wait for the installation to finish and press "Reboot" (Devices without serial console have to be rebooted manually).

If you have downloaded RouterOS packages for multiple architectures, Netinstall will only display the appropriate architecture packages for your device after you have selected it. Unsupported packages will not appear in this window once a device is selected.

If the installation does not start (progress bar is not moving or no status is shown), then you can try closing the Netinstall application and opening it up again or try to put the device into Etherboot mode again. If you are still unable to get Netinstall working, then you should try using it on a different computer since there might be an operating system's issue that is preventing Netinstall from working properly.

The "Keep old configuration" process involves downloading the configuration database from the router, reinstalling the router (including disk formatting), and uploading the configuration files back to it. However, it's important to note that this process solely applies to the configuration itself and does not impact the files, including databases like the User Manager database, Dude database, and others.

After using Netinstall the device will be reset to defaults (unless you specified not to apply default configuration). Some devices are not accessible through e ther1 port with the default configuration for security reasons. Read more about Default configuration.

Option "Keep branding" allows you to retain the device's already installed branding package without reinstalling it using Netinstall.

When using the Configure script option, it is suggested to introduce a delay before configuration execution.

You're all set! Configure your device and reconnect it to your network. Your device should now be functioning correctly!

## Quick start guide for Linux

Download the tool from our download page (links not literal): wget [https://download.mikrotik.com/routeros/[VERSION](https://download.mikrotik.com/routeros/[VERSION)]/netinstall-[VERSION].tar.gz

Extract it: tar -xzf netinstall-[VERSION].tar.gz

Run the tool: sudo ./netinstall-cli [-parameters] [address/interface] routeros-arm64-[package VERSION].npk

The tool requires privileged access and must be run as root, use sudo.

Make sure you have set the IP on your computer's interface to static IP address:

admin@ubuntu:~$ sudo ifconfig <interface> 192.168.88.2/24

Then run the Netinstall version 6 (an example that resets the configuration upon reinstallation procedure):

admin@ubuntu:~$ sudo ./netinstall -r -a 192.168.88.3 routeros-mipsbe-6.48.1.npk Using server IP: 192.168.88.2 Starting PXE server Waiting for RouterBOARD... PXE client: 01:23:45:67:89:10 Sending image: mips Discovered RouterBOARD... Formatting... Sending package routeros-mipsbe-6.48.1.npk ... Ready for reboot... Sent reboot command

Or run the Netinstall version 7 (an example that applies an empty configuration and discards the branding during the reinstallation procedure):

admin@ubuntu:~$ sudo ./netinstall-cli -e -b -i enx1234567ee890 -a 192.168.88.3 routeros-7.14.2-arm.npk wireless-

7.14.2-arm.npk Version: 7.15beta9(2024-03-27 20:41:15) Will apply empty config Will remove branding Using Interface: enx1234567ee890 Wait for Link-UP on 'enx1234567ee890'. OK Using Client IP: 192.168.88.3 Using Server IP: 192.168.88.10 Starting PXE server Waiting for RouterBOARD... client: 74:4D:28:8E:86:74 Detected client architecture: arm Sending and starting Netinstall boot image ... Installed branding package detected Discovered RouterBOARD... 74:4D:28:8E:86:74 Formatting... Sending package routeros-7.14.2-arm.npk ... Sending package wireless-7.14.2-arm.npk ... Sending empty config ... Ready for reboot... Sent reboot command
## Etherboot

Etherboot mode is a special state for a MikroTik device that allows you to reinstall your device using Netinstall. There are two types of booters available for use: the regular booter and the backup booter. It's essential to verify both options.

To use the Regular booter press Ctrl+E to enter etherboot mode using the serial console or press the Reset button after a 1-2 second delay from when you power it on. To employ the backup booter, power OFF the device. Press the Reset button and power on your device (wait until the "USR" led is blinking then stable "On", and when the "USR" led is "Off" - release the Reset button) - the device is booting in bootp mode to reinstall RouterOS using Netinstall.

### Reset button

The Reset can be found on all MikroTik devices, this button can be used to put the device into Etherboot mode. An easy way to put a device into Etherboot mode using the Reset button is by powering off the device, hold the Reset button, power on the device while holding the Reset button and keep holding it until the device shows up in your Netinstalll window.

If you have set up a Protected bootloader, then the reset button's behavior is changed. Make sure you remember the settings you used to set up the Protected bootloader, otherwise you will not be able to use Eterboot mode and will not be able to reset your device.

RouterOS

If your device is able to boot up and you are able to log in, then you can easily put the device into Etherboot mode. To do so, just connect to your device and execute the following command:

/system routerboard settings set boot-device=try-ethernet-once-then-nand

After that either reboot the device or do a power cycle on the device. Next time the device will boot up, then it will first try going into Etherboot mode. Note that after the first boot up, the device will not try going into Etherboot mode and will boot directly from NAND or from the storage type the device is using.

### Serial console

Some devices come with a serial console that can be used to put the device into Etherboot mode. To do so, make sure you configure your computer's serial console. The required parameters for all MikroTik devices (except for RouterBOARD 230 series) are as following:

115200bit/s, 8 data bits, 1 stop bit, no parity, flow control=none by default.

For RouterBOARD 230 series devices the parameters are as following:

9600bit/s, 8 data bits, 1 stop bit, no parity, hardware (RTS/CTS) flow control by default.

Make sure you are using a proper null modem cable, you can find the proper pinout here. When the device is booting up, keep pressing CTRL+E on your keyboard until the device shows that it is trying bootp protocol:

RouterBOOT booter 7.14.2

CRS328-4C-20S-4S+

CPU frequency: 800 MHz Memory size: 512 MiB Storage size: 16 MiB

Press Ctrl+E to enter etherboot mode Press any key within 2 seconds to enter setup
trying bootp protocol.... OK
Got IP address: 192.168.88.3 resolved mac address 84:69:93:9E:E6:49
transfer started ............................... transfer ok, time=2.00s

At this point your device is in Etherboot mode, now the device should show up in your Netinstall window.
