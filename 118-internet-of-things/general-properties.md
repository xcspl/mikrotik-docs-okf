---
type: Reference
title: "General Properties"
description: "Every RouterBOARD with a miniPCI-e slot which supports LTE modems can also be used as a LoRaWAN gateway by installing R11e-LoRa8 or R11e- LoRa9 card. Both UDP and LNS (starting with v7.12rc1 testing version) protocols ar."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# General Properties

Properties Channels Join EUI Network ID Servers Traffic Debugging

Every RouterBOARD with a miniPCI-e slot which supports LTE modems can also be used as a LoRaWAN gateway by installing R11e-LoRa8 or R11e- LoRa9 card. Both UDP and LNS (starting with v7.12rc1 testing version) protocols are supported.

In order to work with Lora, IoT package should be installed. You can find the package for your device architecture in extra packages archive on the download page.

Starting with v7.11 (stable), LoRa functionality is moved into the IoT package that is available on the download page under extra packages. A separate Lora package is still available for download.

When using IoT package, LoRa functionality will move to a /iot lora sub-menu. When using LoRa package, LoRa functionality will be possible via /lora sub-menu.

LoRa package is not obligatory anymore and is left only for compatibility reasons.

note:  RouterOS does not support 3rd party LoRaWAN gateway cards.

## Properties

This menu is used to apply settings to the LoRa interface.

Sub-menu: /iot lora

Property Description

antenna-gain (integer [-128..127]; Antenna gain in dBi. This value should be equal to setup-antenna-gain minus cable-loss. Using 6.5 dBi Default: )0 antenna, 6.5 is the value to be configured (not taking into account cable loss).

server. The gateway will calculate its actual output power by Output power of the gateway is dictated by the subtracting antenna-gain setting from server_value (value received in the downlink message).

channel-plan (as-923 | au-915 | Frequency plans for various regions. custom | eu-868 | in-865 | kr-920 | ru-864 | ru-864-mid | us-915-1 | us-915-2; Default: eu-868)

disabled (yes | no; Default: yes) Whether LoRaWAN gateway is disabled.

forward (ccrc-validtaion | dev-Defines what kind of packets should be forwarded to Network server: addr-validtaion | proprietary-traffic; Default: crc-validtaion) crc-validtaion-Forward valid packets with correct CRC. dev-addr-validtaion-Checks if DevAddr of the packet corresponds to the NetID and if not, drops the packet. The following sequence happens: 1) Dev. Addr value gets "obtained" from the received LoRa packet; 2) Dev. Addr is "compared" against "valid" Net IDs list; 3) If there is no Net ID for the Dev. Addr, the packet is not forwarded; 4) If Net ID is valid, Dev. Addr range is valid, the packet is forwarded. proprietary-traffic-Checks the content of the LoRa packet and if the "type" of the frame is "proprietary", the packet is not forwarded.

gateway-id (string) Gateway ID or Gateway EUI, is used when registering the gateway with the server.

lbt-enabled (yes | no; Default: no) Whether gateway should use LBT (Listen Before Talk) protocol.

listen-time (integer [0us.. Time in microseconds to track RSSI before TX (used when lbt-enabled=yes). 4294967295us]; Default: 5000us)

name (string; Default: ) Name of LoRaWAN gateway.

network (private | public; Default: Whether sync word should (network=private) or should not (network=public) be used. public)

rssi-threshold (integer [-32,768 .. RSSI value to determine whether forwarder may use specific channel to talk. If RSSI value is below rssi-threshold, 32,767]; Default: -65dB) channel could be used (used when lbt-enabled=yes).

servers (list of string; Default: ) Name of the server from the /iot lora servers section.

src-address (IP; Default: ) Specifies uplink packet source address if necessary (address should match an address configured on the RB).

spoof-gps (string; Default: ) Set custom GPS location:

Latitude [-90..90] Longitude [-180..180] Altitude( ) [-2147483648..2147483647] m

Once the server is selected and LoRa interface is enabled using /iot lora enable [find] command, the device will start operating as a LoRaWAN gateway. It will start forwarding LoRa payloads from the /iot lora traffic tab to the configured server.

## Channels

This section is used to alter channel/frequency related settings.

Sub-menu: /iot lora channels

Property Description

bandwidth (7.8_kHz | 15.6_kHz | 31.2_kHz | 62.5_kHz | Bandwidth of specific channel, predefined when any of channel-plan preset is used, but 125_kHz | 250_kHz | 500_kHz; Default: 125_kHz) could be manually changed when channel-plan is set to custom.

disabled (yes | no; Default: no) Disable or enable the channel.

freq-off (integer [-400000..400000]; Default:  ) Channel frequency offset against radio central frequency, it makes possible to adjust channel frequencies so that channels does not overlap.

radio (radio0 | radio1; Default: ) Defines which radio uses selected channel.

spread-factor (SF7 | SF8 | SF9 | SF10 | SF11 | SF12; Defines the Spread Factor for a channel with type=LoRa. Lower Spread Factor means Default: ) higher data rate.

To view current channels, issue the command /iot lora cannels print:

/iot lora channels print Columns: NAME, TYPE, RADIO, FREQ-OFF, BANDWIDTH, FREQ, SPREAD-FACTOR, DATARATE # NAME TYPE RADIO FREQ-OFF BANDWIDTH FREQ SPREAD-FACTOR DATARATE 0 gateway-0 MSF radio1 -400000 125_kHz 868.1 1 gateway-0 MSF radio1 -200000 125_kHz 868.3 2 gateway-0 MSF radio1 0 125_kHz 868.5 3 gateway-0 MSF radio0 -400000 125_kHz 867.1 4 gateway-0 MSF radio0 -200000 125_kHz 867.3 5 gateway-0 MSF radio0 0 125_kHz 867.5 6 gateway-0 MSF radio0 200000 125_kHz 867.7 7 gateway-0 MSF radio0 400000 125_kHz 867.9 8 gateway-0 LoRa radio1 -200000 250_kHz 868.3 SF7 9 gateway-0 FSK radio1 300000 125_kHz 868.8 50000

Channels are created using freq-off and radio's center-freq frequencies. To view radios center frequencies use the command /iot lora radios print.

To understand how each channel's frequency is calculated, check the example below:
