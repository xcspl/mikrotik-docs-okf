---
type: Reference
title: "DLNA Media server"
description: "DLNA is a set of protocols that enables networked devices to share digital media, including videos, photos, and music. Central to the operation of DLNA is the UPnP (Universal Plug and Play) architecture, which facilitate."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# DLNA Media server

DLNA is a set of protocols that enables networked devices to share digital media, including videos, photos, and music. Central to the operation of DLNA is the UPnP (Universal Plug and Play) architecture, which facilitates the discovery and control of network devices.

DLNA and UPnP work in tandem to provide a seamless media sharing experience. UPnP supports device discovery and control on the network through protocols like the Simple Service Discovery Protocol (SSDP) and others such as SOAP (Simple Object Access Protocol) for control messages and XML for device and service descriptions. In the context of DLNA, UPnP serves as the foundation, allowing various devices like TVs, computers, and mobile devices to connect and share media content efficiently.

In RouterOS, enable the media server and share movies or music with your household media devices, such as TVs or player apps in your PC, such as the popular VLC.

Media (DLNA) is not supported on SMIPS devices

## Server settings

Property Description

allowed-hostname To restrict access to specific hostnames.

allowed-ip To limit access to specified IP addresses

friendly-name The name that will be displayed for the DLNA server on the network.

interface Specifies the network interface that the DLNA server will use

path The file path where the media content is stored and will be served from.

disabled Specifies if entry is disabled

## Configuration examples

Creating a DLNA server

/ip media add friendly-name=Mikrotik interface=bridge1 path=usb1

Creating multiple DLNA servers with limitations. Usage example-Limit children's TV access only to child-friendly media, located in folder "usb1/kids"

/ip media add friendly-name=adults interface=bridge1 path=usb1/adults allowed-hostname=ADULTS_TV /ip media add friendly-name=kids interface=bridge1 path=usb1/kids allowed-hostname=KIDS_TV

SMB

Summary

Sub-menu: /ip smb Packages required: system

SMB server provides file sharing access to configured folders of the router.

RouterOS only supports SMB2.1 SMB3.0, SMB3.1.1. SMB1 is not supported due to security vulnerabilities.

SMB is not supported on SMIPS devices

### Server settings

Property Description

comment (string; Default: Mi Set comment for the server krotikSMB)

domain (string; Default: MS Name of Windows Workgroup HOME)

enabled (  yes | no | auto Def The default value is 'auto.' This means that the SMB server will automatically be enabled when the first non-disabled ault: auto) SMB share is configured under '/ip smb share'

interface (string; Default: all) List of interfaces on which SMB service will be running. all-SMB will be available on all interfaces.

Starting from version 7.14, the 'allow-guest' option has been replaced by a default guest user located in 'ip/smb/users'. This default guest user can now be disabled or enabled in this section.

### Share settings

Sub-menu: /ip smb shares

Allows configuring share names and directories that will be accessible by SMB.

If the directory provided in the configuration does not exist it will be created automatically.

Property Description

comment (string; Set a comment for the share Default: default share)

disabled (yes | no; If disabled, the share will not be accessible. Default: no)

valid-users (list of strings Specifies which users are allowed to access the Samba share. If it is left empty, all users will be able to access the share,; | Default:) once user or users are defined here, only they will be able to access the share

invalid-users (list of strin Used to specify users who are explicitly denied access to the Samba share. gs; | Default: )

require-encryption (yes | Enforces the use of encryption for all connections to a particular Samba share. It is recommended to change this to "Yes" to no; Default: no) ensure better stability with macOS clients.

name (string; Default: ) Name of the SMB share

|directory (string; Default:) User setup Sub-menu: /ip smb user|Directory on router assigned to SMB share. If left empty value of the name argument will be used from the root folder. Set up users that can access SMB shares of the router.|
|---|---|
|Property|Description|
|comment (string; Default:) disabled (yes | no; Default: no) name (string; Default:) password (string; Default:) sensitive read-only (yes | no; Default: yes) Example create user: add shared folder: enable SMB service:|Set a description for the user Defines whether the user is enabled or disabled Login name of the SMB service user Password for SMB user to connect to SMB service Sets if the user has only read-only rights when accessing shares or full access rights. To make RouterOS folder available through SMB service follow these steps: /ip/smb/users/add read-only=no name=mtuser password=mtpasswd /ip/smb/shares/add directory=backup name=backup|
|/ip/smb/set enabled=yes Now check for results: Check general service settings: /ip/smb/print enabled: yes domain: MSHOME comment: MikrotikSMB interfaces: all SMB user settings:|#this step is optional, as the default is "enabled=auto"|
|/ip smb/users/print Columns: NAME, PASSWORD # NAME PASSWORD 0 X*r guest 1 mtuser mtpasswd And finally SMB shares settings:|Flags: X-DISABLED; * - DEFAULT; r-READ-ONLY|

/ip/smb/shares/print Flags: X-DISABLED; * - DEFAULT Columns: NAME, DIRECTORY, REQUIRE-ENCRYPTION # NAME DIRECTORY REQUIRE-ENCRYPTION ;;; default share 0 X* pub /pub no 1 backup backup no

Now, additional configuration changes can be done, like disabling the default user and share, etc.

UPS

Summary

Sub-menu: /system ups Standards: APC Smart Protocol

The UPS monitor feature works with APC UPS units that support “smart” signalling over serial RS232 or USB connection. The UPS monitor service is not included in the default set of packages so it needs to be downloaded and installed manually with ups.npk package. This feature enables the network administrator to monitor the UPS and set the router to ‘gracefully’ handle any power outage with no corruption or damage to the router. The basic purpose of this feature is to ensure that the router will come back online after an extended power failure. To do this, the router will monitor the UPS and set itself to hibernate mode when the utility power is down and the UPS battery has less than 10% of its battery power left. The router will then continue to monitor the UPS (while in hibernate mode) and then restart itself when the utility power returns. If the UPS battery is drained and the router loses all power, the router will power back to full operation when the ‘utility’ power returns.

The UPS monitor feature on the MikroTik RouterOS supports

hibernate and safe reboot on power and battery failure UPS battery test and run time calibration test monitoring of all "smart" mode status information supported by UPS logging of power changes

### Connecting the UPS unit

The serial APC UPS (BackUPS Pro or SmartUPS) requires a special serial cable (unless connected with USB). If no cable came with the UPS, a cable may be ordered from APC or one can be made "in-house". Use the following diagram:

Router Side (DB9f) Signal Direction UPS Side (DB9m)

2 Receive IN 2 3 Send OUT 1 5 Ground 4 7 CTS IN 6

If using a RouterBOARD device, make sure to set your "RouterBOOT setup key" to Delete instead of the default Any key. This is to avoid accidental opening of the setup menu if the UPS unit sends some data to the serial port during RouterBOARD startup. This can be done in the RouterBOOT options during boot time or via the RouterBoard Settings in Winbox : Select key which will enter setup on boot:

* 1 - any key 2 - <Delete> key only your choice:
### General Properties

Property Description

alarm-setting (delayed | immediate | low-UPS sound alarm setting: battery | none; Default: immediate) delayed-alarm is delayed to the on-battery event immediate-alarm immediately after the on-battery event low-battery-alarm only when the battery is low none-do not alarm

check-capabilities (yes | no; Default: yes) Whether to check UPS capabilities before reading information. Disabling it can fix compatibility issues with some UPS models. (Applies to RouterOS version 6, implemented since v6.17)

min-runtime (time; Default: never) Minimal run time remaining. After a 'utility' failure, the router will monitor the runtime-left value. When the value reaches the min-runtime value, the router will go to hibernate mode.

never-the router will go to hibernate mode when the "battery low" signal is sent indicating that the battery power is below 10% 0s-the router will continue to work as long as the battery is supplying sufficient voltage

offline-time (time; Default: 0s) How long to work on batteries. The router waits that amount of time and then goes into hibernate mode until the UPS reports that the 'utility' power is back

0s-the router will go into hibernate mode according to the min-runtime setting. In this case, the router will wait until the UPS reports that the battery power is below 10%

port (string; Default: ) Communication port of the router.

Read-only properties:

Property Description

load (percent) The UPS's output load as a percentage of full rated load in Watts. The typical accuracy of this measurement is ±3% of the maximum of 105%

manufacture-date (string) UPS's date of manufacture in the format "mm/dd/yy" (month, day, year).

model (string) Less than 32 ASCII character string consisting of the UPS model name (the words on the front of the UPS itself)

nominal-battery-voltage ( UPS's nominal battery voltage rating (this is not the UPS's actual battery voltage) integer)

offline-after (time) When will the router go offline

serial (string) A string of at least 8 characters directly representing the UPS's serial number as set at the factory. Newer SmartUPS models have 12-character serial numbers

version (string) UPS version, consists of three fields: SKU number, firmware revision, country code. The country code may be one of the following:

I - 220/230/240 Vac D - 115/120 Vac A - 100 Vac M - 208 Vac J - 200 Vac

Note: In order to enable UPS monitor, the serial port should be available.

Example

To enable the UPS monitor for port serial1: [admin@MikroTik] system ups> add port=serial1 disabled=no [admin@MikroTik] system ups> print Flags: X-disabled, I-invalid 0 name="ups" port=serial1 offline-time=5m min-runtime=5m alarm-setting=immediate model="SMART-UPS 1000" version="60.11.I" serial="QS0030311640" manufacture-date="07/18/00" nominal-battery-voltage=24V [admin@MikroTik] system ups>

### Runtime Calibration

Command: /system ups rtc <id>

The rtc command causes the UPS to start a run time calibration until less than 25% of full battery capacity is reached. This command calibrates the returned run time value.

Note: The test begins only if the battery capacity is 100%.

Monitoring

Command: /system ups monitor <id>

Property Description

battery-charge () the UPS's remaining battery capacity as a percent of the fully charged condition

battery-voltage () the UPS's present battery voltage. The typical accuracy of this measurement is ±5% of the maximum value (depending on the UPS's nominal battery voltage)

frequency () when operating on-line, the UPS's internal operating frequency is synchronized to the line within variations of 3 Hz of the nominal 50 or 60 Hz. The typical accuracy of this measurement is ±1% of the full scale value of 63 Hz

line-voltage () the in-line utility power voltage

load () the UPS's output load as a percentage of full rated load in Watts. The typical accuracy of this measurement is ±3% of the maximum of 105%

low-battery (yes | only shown when the UPS reports this status no)

on-battery (yes | Whether UPS battery is supplying power no)

on-line (yes | no) whether power is being provided by the external utility (power company)

output-voltage () the UPS's output voltage

overloaded-output only shown when the UPS reports this status (yes | no)

replace-battery (ye only shown when the UPS reports this status s | no)

runtime-only shown when the UPS reports this status calibration-running (yes | no)

runtime-left (time) the UPS's estimated remaining run time in minutes. You can query the UPS when it is operating in the on-line, bypass, or on- battery modes of operation. The UPS's remaining run time reply is based on available battery capacity and output load

smart-boost-mode only shown when the UPS reports this status (yes | no)

smart-ssdd-mode () only shown when the UPS reports this status

transfer-cause (stri the reason for the most recent transfer to on-battery operation (only shown when the unit is on-battery) ng)

Example

When running on utility power:

[admin@MikroTik] system ups> monitor 0 on-line: yes on-battery: no RTC-running: no runtime-left: 20m battery-charge: 100% battery-voltage: 27V line-voltage: 226V output-voltage: 226V load: 45% temperature: 39C frequency: 50Hz replace-battery: no smart-boost: no smart-trim: no overload: no low-battery: no [admin@MikroTik] system ups>

When running on battery: [admin@MikroTik] system ups> monitor 0 on-line: no on-battery: yes transfer-cause: "Line voltage notch or spike" RTC-running: no runtime-left: 19m offline-after: 4m46s battery-charge: 94% battery-voltage: 24V line-voltage: 0V output-voltage: 228V load: 42% temperature: 39C frequency: 50Hz replace-battery: no smart-boost: no smart-trim: no overload: no low-battery: no [admin@MikroTik] system ups>
