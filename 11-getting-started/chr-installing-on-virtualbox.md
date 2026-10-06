---
type: Reference
title: "CHR: installing on VirtualBox"
description: "1. Download VirtualBox: Install the latest version of VirtualBox from the official website."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# CHR: installing on VirtualBox

## CHR VirtualBox installation. Video instruction

1. Download VirtualBox: Install the latest version of VirtualBox from the official website.
2. Download CHR Image: Download and unpack the latest Stable or Testing version of the CHR (Cloud Hosted Router) VDI image from the MikroTik website.
Step 1: Create a New Virtual Machine

1. Launch the VirtualBox application.
2. Create a New VM: Click on New to create a new virtual machine.

Name and Operating System:

Name: Enter a name for your VM (e.g., MikroTik_CHR). Type: Select Linux. Version: Select Other Linux (64-bit).

Click Next.

### Step 2: Configure Memory Size

Memory Size: Allocate memory for the VM. It is recommended to allocate at least 256 MB of RAM (since RouterOS 7.15.1).

Processors: Select the desired quantity of CPUs. Click Next.

Step 3: Create a Virtual Hard Disk

1. Virtual Hard Disk: Select "Use an existing Hard Disk File" Add the downloaded VDI image file Click Choose.
Click Next.

Check the settings and click Finish.

### Step 4: Configure Virtual Machine Settings

Settings: Select your newly created VM and click on Settings.

System: Go to the System tab and uncheck Floppy, Optical in the Boot Order section. Processors: Go to the Processor tab. Select the desired quantity of CPUs. Network: Go to the Network tab.

Adapter 1: Enable the network adapter and attach it to Bridged Adapter or NAT (depending on your network setup).

### Step 5: Start the Virtual Machine

Start VM: Click Start to boot your new virtual machine.

Login: After the VM reboots, you will see the CHR login prompt. The default login credentials are: Username: admin Password: (blank)

Initial Configuration: Configure the CHR as per your network requirements using the MikroTik CLI or WebFig.

Congratulations! You have successfully installed MikroTik CHR on VirtualBox. You can now proceed with configuring your network settings and using the full features of MikroTik RouterOS.
