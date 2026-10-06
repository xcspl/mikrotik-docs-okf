# Internet of Things

* [Internet of Things](internet-of-things.md) - Internet of Things documentation provides RouterOS features for connecting devices to sensors, gateways, and IoT platforms including Bluetooth, GPIO, LoRa, MQTT, and Wiliot

## Bluetooth

* [Bluetooth](bluetooth.md) - This page documents MikroTik RouterOS's Bluetooth IoT functionality, covering Bluetooth channel structure, advertising packet formats, and configuration via the /iot/bluetooth submenu. It explains PDU types, antenna

## Bluetooth / MikroTik Beacon Manager

* [MikroTik Beacon Manager](mikrotik-beacon-manager.md) - MikroTik Beacon Manager app for configuring TG-BT5 series Bluetooth tags, with guides for Android and iOS and tag advertisement formats
* [MikroTik Beacon Manager for Android devices](mikrotik-beacon-manager-for-android-devices.md) - MikroTik Beacon Manager application is designed for Bluetooth tag (TG-BT5-XX) configuration. Since the tags are Bluetooth-based devices, you have to enable Bluetooth on the phone before proceeding with the configuration
* [MikroTik Beacon Manager for iOS devices](mikrotik-beacon-manager-for-ios-devices.md) - MikroTik Beacon Manager application is designed for Bluetooth tag (TG-BT5-XX) configuration. Since the tags are Bluetooth-based devices, you have to enable Bluetooth on the phone before proceeding with the configuration
* [MikroTik Bluetooth TG-BT5-XX tag changelog](mikrotik-bluetooth-tg-bt5-xx-tag-changelog.md) - MikroTik Bluetooth TG-BT5-XX tag changelog: documentation and related topics
* [MikroTik Tag advertisement formats](mikrotik-tag-advertisement-formats.md) - TG-BT5-XX tags can operate in 4 different modes:

## Bluetooth / User Guides

* [Bluetooth tag-tracking using MQTT and ThingsBoard](bluetooth-tag-tracking-using-mqtt-and-thingsboard.md) - This page documents Bluetooth tag-tracking using MikroTik RouterOS with MQTT and ThingsBoard, detailing how Bluetooth advertising packets are captured by KNOT devices, processed into MQTT messages, and visualized in
* [Email notification on the MikroTik BLE tag's accelerometer triggers](email-notification-on-the-mikrotik-ble-tags-accelerometer-triggers.md) - In this guide, we will show a quick step-by-step on how you can set up your KNOT to send an e-mail notification, whenever it detects a 'triggered' condition reported by the TG-BT5-IN or TG-BT5-OUT tag
* [HTTPS post and Azure configuration](https-post-and-azure-configuration.md) - This article will demonstrate how to configure both Azure and RouterOS to publish the data using the HTTPS protocol. RouterOS, in this scenario, is going to act as a gateway and publish the data that is broadcasted
* [IFTTT app notifications on BLE tag appearance in KNOT's range](ifttt-app-notifications-on-ble-tag-appearance-in-knots-range.md) - Our Bluetooth tags and the KNOT can be used in different scenarios for IoT asset tracking
* [MQTT and Azure configuration](mqtt-and-azure-configuration.md) - Publish MikroTik MQTT data to Microsoft Azure IoT, covering Azure account setup, device credentials, and MQTT broker configuration
* [MQTT/HTTPS and AWS configuration](mqtthttps-and-aws-configuration.md) - Forward MikroTik Bluetooth tag data to Amazon AWS using MQTT over HTTPS, covering AWS account setup, certificates, and broker configuration
* [Sending temperature readings from the TG-BT5-OUT tag to ThingsBoard](sending-temperature-readings-from-the-tg-bt5-out-tag-to-thingsboard.md) - Our TG-BT5-OUT Bluetooth tag model has a temperature sensor built in. This means that it can be used to measure the surrounding temperature

## GPIO

* [GPIO](gpio.md) - GPIO allows configuring digital and analog input/output pins on MikroTik routers for tasks like voltage measurement, dry contact sensing, and relay control. Settings are managed via CLI under /iot/gpio with submenus
* [Using the GPIO as pulse input from a meter device](using-the-gpio-as-pulse-input-from-a-meter-device.md) - Use a MikroTik device's GPIO as a pulse input to read water, energy, or other meters, with a RouterOS script that counts the pulses

## Lora

* [Lora](lora.md) - This page introduces MikroTik RouterOS LoRa and LoRaWAN configuration, covering gateway setup, general properties, server integration, and non-LoRaWAN payload forwarding with MQTT/HTTP. It details supported hardware,
* [General Properties](general-properties.md) - This page documents the configuration settings for setting up a LoRaWAN gateway on MikroTik RouterOS, including antenna gain, channel plans, server connections, and traffic forwarding rules. It explains how to enable

## Lora / User Guides

* [User Guides](user-guides.md) - This section provides user guides for MikroTik LoRa devices and gateways, including step-by-step installation instructions, AWS LoRaWAN and The Things Stack configuration examples, and the TG-LR sensor tag setup guide
* [AWS LoRaWAN configuration](aws-lorawan-configuration.md) - This page guides users through configuring AWS LoRaWAN integration on MikroTik RouterOS, covering gateway registration in AWS IoT Core, certificate generation and importation, and server setup for LNS connectivity
* [ChirpStack](chirpstack.md) - This page guides MikroTik RouterOS users through registering LoRaWAN gateways with ChiprStack open-source server
* [Step by step installation](step-by-step-installation.md) - This page provides a step-by-step guide for installing and configuring LoRa mini-PCIe cards on MikroTik RouterOS, including hardware installation, GUI setup, package management, and initial network server configuration
* [TG-LR setup guide](tg-lr-setup-guide.md) - This page is the setup guide for MikroTik TG-LR82 and TG-LR92 LoRaWAN sensor tags, covering activation, network join, telemetry and sensor configuration, magnet switch commands, command encoding for downlinks, data
* [The Things Stack](the-things-stack.md) - This page guides MikroTik RouterOS users through registering LoRaWAN gateways with The Things Stack, covering UDP and LNS/CUPS protocols. It explains how to find Gateway EUI values, configure server settings,
* [Modbus](modbus.md) - You can find more information about this protocol by following this link

## MQTT

* [MQTT](mqtt.md) - This page documents MQTT integration in MikroTik RouterOS, covering publisher/subscriber workflows for IoT platforms like Kaa and ThingsBoard. It explains MQTT protocol basics, RouterOS capabilities as an MQTT
* [Kaa IoT setup](kaa-iot-setup.md) - This page introduces Kaa IoT setup for MikroTik RouterOS, covering MQTT and HTTP protocol support, system resource monitoring via scripting, and Kaa IoT portal configuration steps including application/device
* [MQTT and ThingsBoard configuration](mqtt-and-thingsboard-configuration.md) - This page guides MikroTik RouterOS users through configuring MQTT data publishing to ThingsBoard, covering device setup, authentication scenarios (access tokens, basic credentials, SSL/TLS), and certificate
* [Wiliot](wiliot.md) - Wiliot is an IoT company offering battery-free Bluetooth tags that broadcast telemetry data, requiring MikroTik RouterOS devices with Bluetooth support for gateway and bridge modes. The documentation guides users
