---
type: Reference
title: "Serial Console"
description: "The Serial Console and Serial Terminal are tools, used to communicate with devices and other systems that are interconnected via the serial port. The serial terminal may be used to monitor and configure many devices-incl."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Serial Console

Overview Serial Console Connections Null Modem Without Handshake Null Modem With Loopback Handshake Null Modem With Partial Handshake Null Modem With Full Handshake Null Modem Compatibility RJ45 Type Serial Port RB M33G Additional Serial Header CCR Serial Header Serial Terminal Usage Special Login

## Overview

The Serial Console and Serial Terminal are tools, used to communicate with devices and other systems that are interconnected via the serial port. The serial terminal may be used to monitor and configure many devices-including modems, network devices (including MikroTik routers), and any device that can be connected to a serial (asynchronous) port.

The Serial Console feature is for configuring direct-access configuration facilities (monitor/keyboard and serial port) that are mostly used for initial or recovery configuration. A special null-modem cable is needed to connect two hosts (like two PCs, or two routers; not modems). Note that a terminal emulation program (e.g., HyperTerminal on Windows or minicom on Linux) is required to access the serial console from another computer. Default settings of the router's serial port are 115200 bits/s (for x86 default is 9600 bits/s), 8 data bits, 1 stop bit, no parity, hardware (RTS/CTS) flow control.

Several customers have described situations where the Serial Terminal (managing side) feature would be useful:

on a mountaintop, where a MikroTik wireless installation sits next to equipment (including switches and Cisco routers) that can not be managed in- band (by telnet through an IP network) monitoring weather-reporting equipment through a serial port connection to a high-speed microwave modem that needed to be monitored and managed by a serial connection

With the serial-terminal feature of the MikroTik, up to 132 (and, maybe, even more) devices can be monitored and controlled.

## Serial Console Connections

Serial communications between devices are done with RS232, it is one of the oldest and most widely spread communication methods in the computer world. It was used for communication with the modems or other peripheral devices DTE/DCE. In the modern world, the main use of serial communication is DTE/DTE communication (Data Terminal Equipment) e.g. using a null-modem cable. There are several types of null modem cables and some of them may not work with RouterBoards at all.

### Null Modem Without Handshake

This cable does not utilize handshake pins at all:

|Side1 (DB9f)|Side2 (DB9f)|Function|
|---|---|---|
|2|3|Rx ← Tx|
|3|2|Tx → Rx|
|5 It allows data-only traffic on the cross-connected Rx/Tx lines. Hardware flow control is not possible with this type of cable. The only way to perform flow control is with software flow control using the XOFF and XON characters.|5|GND|

### Null Modem With Loopback Handshake

|signal lines. available:||The problem with the first cable is when connected to a device on which hardware flow control is enabled software may hang when checking modem Null modem cable with loop back handshake fixes the problem, its main purpose is to fool well-defined software into thinking there is handshaking|
|---|---|---|
|Side1 (DB9f)|Side2 (DB9f)|Function|
|2 3 5 1+4+6 - 7+8 - Null Modem With Partial Handshake|3 2 5 - 1+4+6 - 7+8 This type of cable is not recommended for use with RouterOS.|Rx ← Tx Tx → Rx GND DTR → CD + DSR DTR → CD + DSR RTS → CTS RTS → CTS Hardware flow control is not possible with this cable. Also if remote software does not send its own ready signal to DTR output communication will hang. This cable can be used when flow control enabled without being incompatible with the original way flow control was used with DTE/DCE communication.|
|Side1 (DB9f)|Side2 (DB9f)|Function|
|1 2 3 4 5 6 7+8 Null Modem With Full Handshake|7+8 3 2 6 5 4 1 Used with special software and should not be used with RouterOS.|RTS2 → CTS2 + CD1 Rx ← Tx Tx → Rx DTR → DSR GND DSR ← DTR RTS1 → CTS1 + CD2|
|Side1 (DB9f)|Side2 (DB9f)|Function|
|2 3 4 5 6 7 8|3 2 6 5 4 8 7|Rx ← Tx Tx → Rx DTR → DSR GND DSR ← DTR RTS → CTS CTS ← RTS|

|Null Modem Compatibility Summary tables below will allow you to choose the proper cable for your application.|||||
|---|---|---|---|---|
||No handshake|Loopback handshake|Partial handshake|Full handshake|
|RouterBoards with limited port functionality|Y|Y|N*|N|
|RouterBoards with full functionality|Y|Y|Y|N|
|* - may work only when hardware flow control is disabled|||||
||No handshake|Loopback handshake|Partial handshake|Full handshake|
|Software flow control only|Y|Y*|Y**|Y**|
|Low-speed DTE/DCE compatible hardware flow control|N|Y|Y*|N|
|High-speed DTE/DCE compatible hardware flow control|N|Y|Y**|N|
|High speed communication using special software|N|N|Y*|Y|
|* - will work as an alternative ** - will work but not recommended RJ45 Type Serial Port serial port. RJ45 to DB9 Cable Pinout:|This type of port is used on RouterBOARD 2011, 3011, 4011, CCR1072, CCR1036 r2, CCR2xxx and CRS series devices, sometimes called "Cisco style"||||

Signal Console Port (DTE) RJ-45 Rolled Cable Adapter DB-9 Pin Adapter DB-25 Pin Signal RJ-45 RJ-45 Pin

||RJ-45|RJ-45 Pin||||
|---|---|---|---|---|---|
|RTS|1|8|8|5|CTS|
|DTR|2|7|6|6|DSR|
|TxD|3|6|2|3|RxD|
|Ground|4|5|5|7|Ground|
|Ground|5|4|5|7|Ground|
|RxD|6|3|3|2|TxD|
|DSR|7|2|4|20|DTR|
|CTS|8|1|7|4|RTS|

### RB M33G Additional Serial Header

For RBM33G additional serial header can be attached on GPIO pins U3_RXD, GND, U3_TXD, and 3V3

### CCR Serial Header

The Cloud Core Router series devices have a serial header on the PCB board, called J402 or 100

Here is the pin-out of that connector:

## Serial Terminal Usage

RouterOS allows to communicate with devices and other systems that are connected to the router via the serial port using a /system serial- terminal  command. All keyboard input will be forwarded to the serial port and all data from the port is output to the connected device.

First, you have to have a free serial port, if the device has only one serial port (like all RouterBoards, WRAP/ALIX boards, etc.) you will have to disable the system console on this serial port to be able to use it as Serial Terminal for connection to other equipment (switches, modems, etc):

/system console disable 0

Be sure to just disable the console rather than removing it, as RouterOS will recreate the console after the next reboot when you really remove it.

Note that there are some caveats you should be aware of! Take your time understanding those limits to avoid strange things to happen when connecting a device to a serial port on a RouterBoard:

By re-configuring port Serial0 on a RouterBoard as seen above, you will lose your serial console access to RouterOS. This means, that if you cannot access your RouterBoard over the network anymore, you might even have to reset the whole configuration of it to gain access again. When rebooting a RouterBoard the boot loader (RouterBOOT) will always use the serial console (Serial0 on RouterBoards) to send out some startup messages and offer access to the RouterBOOT menu.

Having text coming out of the serial port to the connected device might confuse your attached device. Furthermore, in the standard config, you can enter the RouterBOOT menu by pressing ANY key. So if your serial device sends any character to the serial port of your RouterBoard during boot time, the RouterBoard will enter the RouterBOOT menu and will NOT boot RouterOS unless you manually intervene!

You can reconfigure RouterBOOT to enter the RouterBOOT menu only when a DEL character is received-use this to reduce the chance to get a router that's stuck when rebooting!

Or if newer versions are used "Silent boot" feature can be used to suppress any output on the serial interface, including removal of booting sounds.

Next, you will have to configure your serial port according to the serial port settings of the connected device. Using the following command you will set your serial port to 19200 Baud 8N1. What settings you need to use depends on the device you connect:

/port set serial0 baud-rate=19200 data-bits=8 parity=none stop-bits=1

You can also try to let RouterOS guess the needed baud rate by setting

/port set serial0 baud-rate=auto

Now's the time to connect your device if not already done. Usually, you will have to use a null modem cable (the same thing as a cross-over-cable for Ethernet). Now we're ready to go:

/system serial-terminal serial0

This will give you access to the device you connected to port Serial0. Ctrl-A is the prefix key, which means that you will enter a small "menu". If you need to send the Ctrl-A character to a remote device, press Ctrl-A twice.

If you want to exit the connection to the serial device type Ctrl-A, then Q. This will return you to your RouterOS console.

Do not connect to devices at an incorrect speed and avoid dumping binary data.

## Special Login

Special login can be used to access another device (like a switch, for example) that is connected through a serial cable by opening a telnet/ssh session that will get you directly on this device (without having to login to RouterOS first).

For demonstration we will use two RouterBoards and one PC.

Routers R1 and R2 are connected with serial cable and PC is connected to R1 via ethernet. Lets say we want to access router R2 via serial cable from our PC. To do this you have to set up serial interface proxy on R1. It can be done by feature called special-login.

By default console is bound to serial port.

First task is to unbind console from serial simply by disabling entry in /system console menu:

[admin@MikroTik] /system console> print Flags: X-disabled, U-used, F-free # PORT TERM 0 X serial0 vt102

Next step is to add new user, in this case serial, and bind it to the serial port

[admin@MikroTik] > /user add name=serial group=full [admin@MikroTik] > /special-login add user=serial port=serial0 disabled=no [admin@MikroTik] > /special-login print Flags: X-disabled # USER PORT 0 serial serial0

Now we are ready to access R2 from our PC.

maris@bumba:/$ ssh serial@10.1.101.146

[Ctrl-A is the prefix key] R2 4.0beta4 R2 Login:

[admin@R2] >

To exit special login mode press Ctrl+A and Q

[admin@MikroTik] > [Q-quit connection] [B-send break] [A-send Ctrl-A prefix] [R-autoconfigure rate]

Connection to 10.1.101.146 closed.

After router reboot and serial cable attached router may stuck at Bootloader main menu

To fix this problem you need to allow access bootloader main menu from <any> key to <delete>:

enter bootloader menu press 'k' for boot key options press '2' to change key to <delete> What do you want to configure? d-boot delay k-boot key s-serial console n-silent boot o-boot device u-cpu mode f-cpu frequency r-reset booter configuration e-format nand g-upgrade firmware i-board info p-boot protocol b-booter options t-call debug code l-erase license x-exit setup your choice: k-boot key Select key which will enter setup on boot:

* 1 - any key 2 - <Delete> key only your choice: 2

SSH

SSH Server Properties Enabling PKI authentication SSH key pair generation SSH Client Simple log-in to remote host Log-in from certain IP address of the router Log-in using SSH key Executing remote commands SSH exec Retrieve information

## SSH Server

RouterOS has built in SSH (SSH v2) server that is enabled by default and is listening for incoming connections on port TCP/22. It is possible to change the port and disable the server under Services menu.

Properties

Sub-menu: /ip ssh

Property Description

password-authentication (yes-if-no-key Whether to allow password login at the same time when public key authorization is configured for a user. | yes | no; Default: yes-if-no-key)

ciphers (3des-cbc | aes-cbc | aes-ctr | Allow to configure SSH ciphers.; aes-gcm | auto | null Default: auto)

forwarding-enabled (both | local | no | Allows to control which SSH forwarding method to allow: remote; Default: no) no-SSH forwarding is disabled; local-Allow SSH clients to originate connections from the server(router), this setting controls also dynamic forwarding; remote-Allow SSH clients to listen on the server(router) and forward incoming connections; both-Allow both local and remote forwarding methods.

host-key-size (1024 | 1536 | 2048 | RSA key size when host key is being regenerated. 4096 | 8192; Default: 2048)

host-key-type (ed25519 rsa |; Default: Select host key type rsa)

publickey-authentication-options  (none Sets public key authentication options. | touch-required | verify-required; Default: none) The touch-required option causes public key authentication using a FIDO authenticator algorithm to always require the signature to attest that a physically present user explicitly confirmed the authentication (usually by touching the authenticator).

The verify-required option requires a FIDO key signature attest that the user was verified, e.g. via a PIN.

strong-crypto (yes | no; Default: no) Use stronger encryption, HMAC algorithms, use bigger DH primes and disallow weaker ones:

use 256 and 192 bit encryption instead of 128 bits; disable null encryption; use sha256 for hashing instead of sha1; disable md5; use 2048bit prime for Diffie-Hellman exchange instead of 1024bit.

Commands

Property Description

export-host-key (key-file-Export public and private RSA/Ed25519 to files. Command takes two parameters: prefix) key-file-prefix - used prefix for generated files, for example, prefix 'my' will generate files 'my_rsa', 'my_rsa.pub' etc. passphrase-private key passphrase sensitive

Host keys are exported in PKCS#8 format.

import-host-key (private-Import and replace private RSA/Ed25519 key from specified file. Command takes two parameters: key-file) private-key-file - name of the private RSA/Ed25519 key file passphrase-private key passphrase sensitive

Private key is supported in PEM or PKCS#8 format.

regenerate-host-key () Generated new and replace current set of private keys (RSA/Ed25519) on the router. Be aware that previously imported keys might stop working.

Exporting the SSH host key requires "sensitive" user policy.

### Enabling PKI authentication

Example of importing public key for user admin

Get SSH key pair on the client device (the device you will connect from). Upload the public SSH key to the router and import it.

More information about supported SSH keys find here.

/user ssh-keys import public-key-file=id_rsa.pub user=admin

### SSH key pair generation

RouterOS does not support direct SSH key generation, which is available on Linux systems.

To obtain an SSH key pair (SSH key pair is automatically generated on the first SSH connection or when host key is exported), the device's SSH host key must be exported.

## SSH Client

Sub-menu: /system ssh

### Simple log-in to remote host

It is able to connect to remote host and initiate ssh session. IP address supports both IPv4 and IPv6.

/system ssh 192.168.88.1 /system ssh 2001:db8:add:1337::beef

In this case user name provided to remote host is one that has logged into the router. If other value is required, then user=<username> has to be used.

/system ssh 192.168.88.1 user=lala /system ssh 2001:db8:add:1337::beef user=lala

Log-in from certain IP address of the router

For testing or security reasons it may be required to log in to other host using certain source address of the connection. In this case src-address=<ip address> argument has to be used. Note that IP address in this case supports both, IPv4 and IPv6.

/system ssh 192.168.88.1 src-address=192.168.89.2 /system ssh 2001:db8:add:1337::beef src-address=2001:db8:bad:1000::2

in this case, ssh client will try to bind to address specified and then initiate ssh connection to remote host.

### Log-in using SSH key

Example of importing RSA private key for user admin.

First, export currently generated SSH keys to a file:

/ip ssh export-host-key key-file-prefix=admin

Two files admin_rsa and admin_rsa.pub will be generated. The pub file needs to be trusted on the SSH server side (how to enable SSH PKI on RouterOS) The private key has to be added for the particular user.

/user ssh-keys private import user=admin private-key-file=admin_rsa

Only user with full rights on the router can change 'user' attribute value under /user ssh-keys private

After the public key is installed and trusted on the SSH server, a PKI SSH session can be created.

/system ssh 192.168.1.1

Watch how to:

Log in with an RSA key.

Log in with Ed25519.

### Executing remote commands

To execute remote command it has to be supplied at the end of log-in line

/system ssh 192.168.88.1 "/ip address print" /system ssh 192.168.88.1 command="/ip address print" /system ssh 2001:db8:add:1337::beef "/ip address print" /system ssh 2001:db8:add:1337::beef command="/ip address print"

If the server does not support pseudo-tty (ssh -T or ssh host command), like MikroTik ssh server, then it is not possible to send multiline commands via SSH

For example, sending command "/ip address \n add address=1.1.1.1/24" to MikroTik router will fail.

If you wish to execute remote commands via scripts or scheduler, use command ssh-exec.

## SSH exec

Sub-menu: /system ssh-exec

Command ssh-exec is a non-interactive ssh command, thus allowing to execute commands remotely on a device via scripts and scheduler.

### Retrieve information

The command will return two values:

exit-code: returns 0 if the command execution succeeded output: returns the output of remotely executed command

Example: Code below will retrieve interface status of ether1 from device 10.10.10.1 and output the result to "Log"

:local Status ([/system ssh-exec address=10.10.10.1 user=remote command=":put ([/interface ethernet monitor [find where name=ether1] once as-value]->\"status\")" as-value]->"output") :log info $Status

For security reasons you should not use plain text password with parameter "password" specified in the command line. To ensure safe execution of the command remotely, it is strongly recommended to use SSH PKI authentication for users on both sides.

The user group and script policy executing the command requires test permission

Watch how to execute commands through SSH.
