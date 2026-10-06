---
type: Reference
title: "Step by step installation"
description: "This page provides a step-by-step guide for installing and configuring LoRa mini-PCIe cards on MikroTik RouterOS, including hardware installation, GUI setup, package management, and initial network server configuration"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, internet-of-things]
resource: https://manual.mikrotik.com/docs/internet-of-things/lora/user-guides/step-by-step-installation.md
sources:
  - resource: https://manual.mikrotik.com/docs/internet-of-things/lora/user-guides/step-by-step-installation.md
---

# Step by step installation

### LoRa card installation

LtAP LTE kit will be used as an example in this section.

Open your router's case. For LtAP specifically, once you have removed all the screws, carefully move the upper case to the left side, as the LTE antennas are attached to the inner side of it:

![1.png](https://manual.mikrotik.com/docs/internet-of-things/lora/user-guides/img/step-by-step-installation-01.webp)

Insert R11e-LoRa card into the mini-PCIe slot and apply two screws to the threaded inserts:

![](https://manual.mikrotik.com/docs/internet-of-things/lora/user-guides/img/step-by-step-installation-02.webp)

Attach antenna to the card (UFL connector). In this case UFL → SMA cable is also used, as the LtAP's case has a specific slot for it.

![](https://manual.mikrotik.com/docs/internet-of-things/lora/user-guides/img/step-by-step-installation-03.webp)

Once the previous steps are done, you can close the router's case and move on to configuration.

### Configuration

#### GUI setup

Connect to your router via Winbox or WebFig.

Winbox can be downloaded from the [link](https://mikrotik.com/download/winbox).

Run it:

![](https://manual.mikrotik.com/docs/internet-of-things/lora/user-guides/img/step-by-step-installation-04.webp)

It is highly recommended to upgrade your RouterOS version to the latest available. Installing the version will perform a reboot:

![](https://manual.mikrotik.com/docs/internet-of-things/lora/user-guides/img/step-by-step-installation-05.webp)

If your device does not have the **IoT>LoRa** menu, download "**Extra packages**" specifically for your router's architecture and rOS version. You can see the type of your router's architecture at the top of the Winbox window or in System →  Resources → Architecture Name.
[https://mikrotik.com/download](https://mikrotik.com/download)
![](https://manual.mikrotik.com/docs/internet-of-things/lora/user-guides/img/step-by-step-installation-06.webp)

Once the package is downloaded and extracted, upload the **IoT** package to your router. It can be done via drag & drop as well. It should appear in the files folder after the upload is complete. Reboot your router (System → Reboot) to install the package:
![](https://manual.mikrotik.com/docs/internet-of-things/lora/user-guides/img/step-by-step-installation-07.webp)

After the reboot, the package should be visible in the Package list:
![](https://manual.mikrotik.com/docs/internet-of-things/lora/user-guides/img/step-by-step-installation-08.webp)

Check if the LoRa gateway has initialized under **IoT>LoRa>Devices**. If it is an LtAP model, make sure to set USB Type to Mini-PCIe:
![](https://manual.mikrotik.com/docs/internet-of-things/lora/user-guides/img/step-by-step-installation-09.webp)

Once the gateway has shown up (under **IoT>LoRa>Devices**), select it, choose Network Servers from the default ones or add your own (under **IoT>LoRa>Servers**) and enable it:
![](https://manual.mikrotik.com/docs/internet-of-things/lora/user-guides/img/step-by-step-installation-10.webp)

Navigate to the Traffic tab to monitor the surrounding nodes sending requests:
![](https://manual.mikrotik.com/docs/internet-of-things/lora/user-guides/img/step-by-step-installation-11.webp)

This concludes basic installation and configuration of LoRa mini-PCIe cards. For additional settings check: [General Properties](https://manual.mikrotik.com/docs/internet-of-things/lora/general-properties.md)
