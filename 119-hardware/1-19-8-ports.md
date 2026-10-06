---
type: Reference
title: "Ports"
description: "There are many ways how to use ports on the routers. Most obvious one is to use serial port for initial RouterOS configuration after installation (by default serial0 is used by serial-terminal)."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Ports

Summary General Properties Remote Access Properties

## Summary

There are many ways how to use ports on the routers. Most obvious one is to use serial port for initial RouterOS configuration after installation (by default serial0 is used by serial-terminal).

Serial and USB ports can also be used to:

connect 3G modems; connect to another device through a serial cable access device connected to serial cable remotely.

## General

Sub-menu: /port

Menu lists all available serial and USB ports on the router and allows to configure port parameters, like baud-rate, flow-control, etc.

Below you can see default port configuration on LtAP.

[admin@LtAP] > /port/print Columns: DEVICE, NAME, CHANNELS, USED-BY, BAUD-RATE # DEVICE NAME CHANNELS USED-BY BAUD-RATE 0 serial0 1 Serial Console(#0) auto 1 gps 1 GPS(#0) 115200

List of the ports are maintained automatically by the RouterOS.

## Properties

Property Description

baud-rate (integer | auto; Baud rate (speed) used by the port. If set to auto, then RouterOS tries to detect baud rate automatically. Default: auto)

data-bits (7 | 8; Default: ) The number of data bits in each character.

7 - true ASCII 8 - any data (matches the size of a byte)

dtr (on | off; Default: ) Whether to enable RS-232 DTR signal circuit used by flow control.

flow-control (hardware | none | method of flow control to pause and resume the transmission of data. xon-xoff; Default: )

name (string; Default: ) Name of the port.

parity (even | none | odd; Error detection method. If enabled, extra bit is sent to detect the communication errors. In most cases parity is set to n Default: ) one and errors are handled by the communication protocol.

|rts (on | off; Default:) Read-only properties|stop-bits (1 | 2; Default:)||Whether to enable RS-232 RTS signal circuit used by flow control. Stop bits sent after each character. Electronic devices usually uses 1 stop bit.|
|---|---|---|---|
|Property|Description|||
|channels (integer) inactive (yes | no) line-state () used-by (string) Properties|Remote Access Sub-menu: /port remote-access Enabling remote access on RouterOS is very easy:|Number of channels supported by the port.|Shows current port state, inactive=yes-device with port previous was connected, but currently is not present Shows who  is currently are using port and channel (#).  For example, by default Serial0 is used by serial-console. If you want to access serial device that can only talk to COM ports and is located somewhere else behind router, then you can use remote-access. As defined in RFC 2217 RouterOS can transfer data from/to a serial device over TCP connection. /port remote-access add port=serial0 protocol=rfc2217 tcp-port=9999 By default serial0 is used by serial-terminal. Without releasing the port, it cannot be used by remote-access or other services|
|Property|||Description|
|0.0.0.0/0) port (string; Default:) Read-only properties|allowed-addresses (IP address range; Default: channel (integer [0..4294967295]; Default:) disabled (yes | no; Default: no) local-address (IP address; Default:) log-file (string; Default:) "" protocol (raw | rfc2217; Default: rfc2217) tcp-port (integer [1..65535]; Default:)|0|Range of IP addresses allowed to access port remotely. 0 Port channel that will be used. If port has only one channel then channel number should always be. 0 IP address used as source address. Name of the file, where communication will be logged. By default logging is disabled. Name of the port from Port list. RFC 2217 defines a protocol to transfer data from/to a serial device over TCP. If set to raw, then data is sent to serial as is. TCP port on which to listen for incoming connections.|
|Property||Description||
|active (yes | no) busy (yes | no) inactive (yes | no)|||Whether remote access is active and ready to accept connection. Whether port is currently busy.|

logging-active (yes | no) Whether logging to file is currently running

remote-address (IP address) IP address of remote location that is currently connected.
