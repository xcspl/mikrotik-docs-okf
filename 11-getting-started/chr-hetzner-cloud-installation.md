---
type: Reference
title: "CHR: Hetzner Cloud Installation"
description: "Note: Replace the URL with the link to the latest CHR version available on the MikroTik download page."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# CHR: Hetzner Cloud Installation

Hetzner Cloud is a cloud computing platform that allows users to run virtual machines (VMs) in the cloud. It offers scalable infrastructure and a range of pre-configured Linux distributions. However, for those needing advanced networking features, Hetzner Cloud is also a great platform for deploying RouterO S CHR (Cloud Hosted Router). CHR is a MikroTik product that provides a fully functional RouterOS installation in a virtual environment, ideal for cloud-based routing, VPN services, and other network management tasks. By running RouterOS CHR on Hetzner Cloud, users can leverage powerful networking tools with the flexibility and scalability of a cloud environment.

1. Create a Hetzner Cloud Server Begin by creating a new server on Hetzner Cloud. Any of the available server options will work.
2. Activate Rescue System In the Hetzner Cloud admin interface, activate the Enable Rescue system by selecting "ENABLE RESCUE & POWER CYCLE" Choose 'linux64' as the Rescue OS. The system will display a username and password. Use these credentials to log into the rescue system via SSH.
3. Install CHR (Cloud Hosted Router) Once logged into the rescue system, download the CHR RAW disk image and write it over the system disk of the cloud server using the following command: curl -L [https://download.mikrotik.com/routeros/7.15.3/chr-7.15.3.img.zip](https://download.mikrotik.com/routeros/7.15.3/chr-7.15.3.img.zip) | funzip | dd of=/dev/sda bs=1M
Note: Replace the URL with the link to the latest CHR version available on the MikroTik download page.

Reboot the Server

After the installation is complete, reboot the server by issuing the reboot command.

It is crucial to secure your RouterOS installation immediately!

Make sure to keep your RouterOS updated and follow best security practices to maintain the safety and performance of your server.
