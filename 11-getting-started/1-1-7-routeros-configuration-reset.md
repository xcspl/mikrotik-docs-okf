---
type: Reference
title: "RouterOS configuration reset"
description: "Resetting the RouterOS configuration Hold this button until the LED light starts flashing, and release the button to reset RouterOS configuration to default."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# RouterOS configuration reset

## Quickstart

To reset RouterOS to factory defaults (this means losing configuration, but also resetting the password), do the following:

1. Turn off the device by unplugging it
2. Hold the reset button
3. While holding it, plug in the device power cable
4. Watch the LED lights of the device, one of the LEDs (usually the User / USR light) will start blinking
5. When this LED blinks, release the button to complete the reset
## Reset From RouterOS

If you still have access to your router and want to recover its default configuration, then you can:

Run the command "/system reset-configuration" from a command-line interface;

Do it from System -> Reset Configuration menu in the graphical user interface; the

## Using the Reset Button

MikroTik routers are fitted with a reset button which has several functions:

Loading the backup RouterBOOT loader Hold this button before applying power, and release it after three seconds since powering, to load the backup boot loader. This might be necessary if the device is not operating because of a failed RouterBOOT upgrade. When you have started the device with the backup loader, you can either set RouterOS to force backup loader in the RouterBOARD settings or have a chance to reinstall the failed RouterBOOT from a ".fwf" file (total of 3 seconds)

Resetting the RouterOS configuration Hold this button until the LED light starts flashing, and release the button to reset RouterOS configuration to default.

Enabling CAPs mode To connect this device to a wireless network managed by CAPsMAN, keep holding the button for 5 more seconds, LED turns solid, release now to turn on CAPs mode. It is also possible to enable CAPs mode via the command line, to do so run the command "/system reset-configuration caps-mode=yes";

Starting the RouterBOARD in Netinstall mode Or keep holding the button for 5 more seconds until the LED turns off, then release it to make the RouterBOARD look for Netinstall servers. You can also simply keep the button pressed until the device shows up in the Netinstall program on Windows.

You can also do the previous three functions without loading the backup loader, simply push the button immediately after you apply power. You might need the assistance of another person to push the button and also plug in the power supply at the same time!

## How to reset configuration

1) Unplug the device from power;
2) Press and hold the button right after applying power;
Note: hold the button until the LED will start flashing;

3) Release the button to clear the configuration; If you wait until the LED stops flashing, and only then release the button-this will instead launch Netinstall mode, to reinstall RouterOS.

## Jumper hole reset

Older RouterBOARD models are also fitted with a reset jumper hole. Some devices might need an opening of the enclosure, RB750/RB951/RB751 have the jumper hole under one of the rubber feet of the enclosure.

Close the jumper with a metal screwdriver, and boot the board until the configuration is cleared:

### Jumper reset for older models

The below image shows the location of the Reset Jumper on older RouterBOARDs like RB133C:

Don't forget to remove the jumper after the configuration has been reset, or it will be reset every time you reboot!

WPS

Some devices have WPS button, or reset button with WPS functionality to reach and control access for Wireless networks without logging into the device, so that client can connect without password. Specific models use WPS sync function to connect with each other. Detailed information on WPS and reset button functionality for each model are described in User Manuals

||Backup Summary want to save it. the backup file in a safe place. Saving a backup Sub-menu: /system backup save|We recommend restoring the backup on the same version of RouterOS.|The RouterOS backup feature allows cloning a router configuration in binary format, which can then be re-applied on the same device. The system's backup file also contains the device's MAC addresses, which are restored when the backup file is loaded. If The Dude or User-manager or installed on the router, then the system backup will not contain configuration from these services, therefore, additional care should be taken to save configuration from these services. Use the provided tool mechanisms to save/export configuration if you System backups contain sensitive information about your device and its configuration, always consider encrypting the backup file and keeping|
|---|---|---|---|
||Property dont-encrypt (yes | no; Default: no) encryption (aes-sha256 | rc4; name (string; Default: [identity]-[date]-[time].backup) password (string; Default:) se nsitive If Loading a backup Load units backup without password:|except if the dont-encrypted property is used or the current user's password is empty. The backup file will be available under /file menu, which can be downloaded using FTP or using Winbox.|Description Disable backup file encryption. Note that since RouterOS v6.43 without a provided password, the backup file is unencrypted. The encryption algorithm to use for encrypting the backup file. Note that is not considered a secure encryption Default: aes-sha256)  method and is only available for compatibility reasons with older RouterOS versions. The filename for the backup file. Password for the encrypted backup file. Note that since RouterOS v6.43 without a provided password, the backup file is unencrypted. password is not provided in RouterOS versions older than v6.43, then the backup file will be encrypted with the current user's password, a [admin@MikroTik] > system/backup/load name=auto-before-reset.backup password=""|
||Property name (string; Default:) password (string; Default:) sensitive||Description File name for the backup file. Password for the encrypted backup file.|

## Example

To save the router's configuration to file test and a password:

[admin@MikroTik] > /system backup save name=test password=<YOUR_PASSWORD> Configuration backup saved [admin@MikroTik] > /system backup

To see the files stored on the router:

[admin@MikroTik] > /file print # NAME TYPE SIZE CREATION-TIME 0 test.backup backup 12567 sep/08/2018 21:07:50 [admin@MikroTik] >

To load the saved backup file test:

[admin@MikroTik] > /system backup load name=test password: <YOUR_PASSWORD> Restore and reboot? [y/N]: y Restoring system configuration System configuration restored, rebooting now

## Cloud backup

Since RouterOS v6.44 it is possible to securely store your device's backup file on MikroTik's Cloud servers, read more about this feature on the IP/Cloud pa ge.
