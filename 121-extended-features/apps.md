---
type: Reference
title: "Apps"
description: "The configuration parameters, however, can be edited before enabling an app, and the applied yaml file can always be viewed."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Apps

Summary

Sub-menu: /app Packages required: container

The App menu provides a catalog of applications that can be deployed in a couple of clicks. Each app can consist of one or multiple pre-configured containers and the necessary RouterOS configuration such as firewall rules and address translation will be applied automatically. This catalog is prepared and maintened by MikroTik, but the container images get sourced from multiple registries such as Docker Hub, GCR and Quay.

The configuration parameters, however, can be edited before enabling an app, and the applied yaml file can always be viewed.

Requirements

The App system inherits the same requirements as the Container package:

Architecture Support: arm64, and x86 architectures Container Package: Must be installed Device Mode: Container mode must be enabled (requires physical access and device reset) External Storage: Highly recommended for optimal performance Memory Requirements: Adequate RAM for container operations (16MB SPI flash devices may require external storage for images) Architecture Limitations: Devices with EN7562CT CPU (like hEX Refresh) are not supported

Security Considerations

As with the underlying Container system, the App menu inherits security implications:

Physical access required to initially enable container support Once enabled, containers can be managed remotely Compromised devices can use containers to install malicious software Device security is equivalent to the security of running containers Third-party container images may introduce security vulnerabilities

## Properties

|auto-update (yes | no; Default:  no)||Enables/disables auto-updating when new image version is available|
|---|---|---|
|check-certificate (yes | no; Default: yes)||Verify registry certificate before pulling container image|
|container-command-lines (string; Default: )||Specify app command lines to start with|
|devices (string; Default: )||Specify extra HW devices to app|
|environment (string; Default: )||List of environmental variables to be used with app|
|extra-mounts (string; Default: )||Specify extra mounts to add to app|
|firewall-redirects (string; Default: )||Specified in the specify port redirects from device to container|
|network (default lan internal;|| ||Allows to specify which network will be used-internal (behind NAT), lan (on your LAN network), default|
|Default: default )||(different per app, can be internal and lan)|
|pvid (integer; Default: 1)||Sets pvid of app veth interface in bridge|

required-hw-devices

required-mounts

use-https (yes | no; Default:  yes)

yaml (string; Default: )

Read-only properties

app-size

app-store-url (string)

cpu-usage

custom (yes | no)

data-size

default-credentials (string)

default-network (lan/internal)

description (string)

from-app-store (yes/no)

interface (string)

ip-address (IP)

memory-current

name (string)

project-page (string)

running

ui-url (string)

variables-to-be-used-in-environment

Setup Wizard

Step 1: Storage Selection

Modifiable only after adding the yaml. Specified device must be present for app to start

Compose:

devices:

- [host-hw-device]:[device-in-app]
Modifiable only after adding the yaml. Required mounts for the container to start

Compose:

volumes:

- [dir-on-host]:[dir-in-app]
Use HTTPS for app URL. Will not work on devices which do not support cloud services.

Compose .yml for app. See example

App size

URL of used app-store for the app

CPU usage

Shows if app is custom (made by user)

Stored app data size

Default credentials of app

App default used network

App description from the "descr" parameter in the YAML

Yes if app is from custom app store, no-if it is not

VETH Interface which is used by the app

VETH interface IP address

Current used memory by the app

App name from the "name" parameter in the YAML

App project page from the "page" parameter in the YAML

Yes-if app is running

Status of app

App generated URL to web interface (if it has one)

List of all present variables in the environment

status (acquire veth | configuring container(s) | downloading/extracting | starting)

The App menu includes a setup wizard (button "Setup" in the GUI, or command /app setup). This wizard automates all the networking, storage, and registry setup that would otherwise require multiple manual steps.

Choose the storage disk for application installation. The system automatically detects available formatted disks (nvme1, usb1, disk1, etc.). If no suitable disk appears, it must be formatted with ext4 or btrfs and mounted via /disk menu.

Requirements:

Minimum 100MB/s sequential read/write speed and 10K random IOPS recommended Use /disk/test command to verify storage performance External storage highly recommended for optimal performance

Step 2: Bridge Configuration

Select the LAN bridge interface for container networking. This enables automatic port forwarding and application autodiscovery on the local network. The wizard automatically configures:

Virtual ethernet (veth) interfaces Adding the veth interface to the configured bridge NAT rules for outbound connectivity

Step 3: IP Configuration

Specify the router IP address for application access. The system auto-detects the primary IP but allows manual override for complex network configurations. This IP will be used for:

Application UI-URL generation Automatic port forwarding rules WebFig integration links

Completion

After completing the setup wizard, the App system is ready for immediate use. Applications can be enabled directly through the interface and will automatically handle all underlying container configuration.

Configuration

App configuration is accessible through /app/settings and provides simplified setup compared to manual Container configuration

## Properties

app-store-urls (string; Default: ) URL to custom app store. URL must lead to a yaml array, where each app is an element in the array

auto-update (yes | no; Default:  no) Global setting to enable auto-update on all apps

disk (string; Default: ) Global setting for the disk that will be used

download-path (string; Default: ) Manually specify the path where all downloads will be stored

lan-bridge (string; Default: ) Manually specify the local area network bridge

media-path (string; Default: ) Manually specify the path where all media will be stored

registry-mirrors (string; Default: ) Specify one or multiple registry mirrors

router-ip (IP; Default: ) Manually specify the IP where the current device can be reached

show-in-webfig (yes | no; Default:  yes) Shows or hides links to enabled apps in the Webfig login page

Certain parameters are initially configured automatically. However, it is always possible to override them.

Auto-configured settings include:

assumed router-ip: Network IP address for RouterOS device assumed-lan-bridge: Network bridge interface for LAN connectivity assumed-media-path: Default media storage path (typically disk/media) assumed-download-path: Download directory path (typically disk/media/downloads)

Application Management

Applications are managed through the /app interface, providing status monitoring and lifecycle control similar to the underlying /container system:

/app> print Flags: X-DISABLED, R-RUNNING Columns: NAME, UI-URL, MEMORY-CURRENT, APP-SIZE, DATA-SIZE, CATEGORY, DESCRIPTION

Status Indicators and Metadata

Flags: X (DISABLED) - Can indicate two states: not downloaded/installed (APP-SIZE and DATA-SIZE will be empty), or downloaded but disabled (APP-SIZE and DATA-SIZE show storage usage) R (RUNNING) - Application actively running and accessible UI-URL: Direct web interface access URL when application is running MEMORY-CURRENT: Real-time memory consumption in MiB (only when running) APP-SIZE: Container image storage consumption in MiB (shows space used when downloaded) DATA-SIZE: Application persistent data size in KiB/MiB (shows configuration and user data) CATEGORY: Application functional classification DESCRIPTION: Application functionality description

Application Lifecycle Management

Deployment Process

Unlike manual Container deployment which requires multiple configuration steps (veth interfaces, bridge setup, environment variables, mounts, and firewall rules), App deployment automates the entire process:

1. Selection: Choose application from catalog via CLI or WebFig
2. Download: Automatic container image download and extraction
3. Network Setup: Automatic veth interface and bridge configuration
4. Port Forwarding: Automatic firewall rule creation for web access
5. Startup: Container initialization with pre-configured settings
6. Access: UI-URL becomes available for immediate web interface access
Cleanup Command

The cleanup command provides complete application removal, including all associated data. This operation is destructive and irreversible:

/app> cleanup pihole App data will be lost, continue? [y/N]:

Cleanup Process:

1. Stops the running container
2. Removes all application data and configuration files
3. Deletes container image from storage
4. Resets application to uninstalled state (empty APP-SIZE and DATA-SIZE)
5. Removes network configuration specific to the application
Warning: All user data, configuration settings, and application state will be permanently lost. The application will return to its original catalog state and require complete reconfiguration if reinstalled.

User-addable apps

Starting v7.22, users can create apps themselves by writing a compose YAML file within RouterOS.

This feature can be very useful in the hands of experienced users requiring custom solutions in their setups.

YAML Example

As an example, you can create a custom app running Alpine Linux, which adds iperf3 and runs a server.

|category: network services: iperf: ports:|name: alpine-iperf page: https://iperf.fr/ default-credentials: none image: docker.io/alpine:latest - 5201:5201:tcp - 5201:5201:udp|descr: Alpine Linux container running iperf3 server command: /bin/sh -c "apk add --no-cache iperf3 && iperf3 -s"|
|---|---|---|
|Add the custom app|/app add network=lan|To create an app. There are two ways. By using a .yml file or by creating a blank app and editing the YAML. In this example we will be adding the alpine-iperf3 app we created using the compose file, so for ease of use. We will be putting it into the LAN bridge, so that our devices in the network can easily access it and no NAT is required.|
|In the Terminal, run:|Then we must add the YAML. /app edit app yaml|Usually, after creating an app this way, it's default name is  "app".|
|command:|Afterwards press CTRL+O to save. Finally enable it. Available Applications by Category|A text editor will be opened and you can paste your YAML in there. Alternatively, you can save the compose text to a file and upload it to the device. Afterwards, you can set the file as the app's YAML using the following app add yaml=[/file get alpine-iperf.yml contents]|
|Category|Count|Applications|
|Productivity Media Media-Management Development Networking Monitoring Communication File-Management /Storage|15 9 2 7 10 14 5 9|adventurelog, babybuddy, calibre-web, convertx, docmost, excalidraw, fossil, hedgedoc, kimai, memos, partdb, wallabag, warracker, webtop, wordpress immich, jellyfin, lidarr, nzbget, plex, prowlarr, radarr, sonarr, transmission jackett, mediamanager, code-server, forgejo, gitea, gitlab, jupyter-notebook, livebook, sonatype-nexus caddy, chr, cloudflared, firefox, goaway, myip, pihole, pmacct-netflow, technitium, upsnap grafana, influxdb, librenms, librespeed, netbox, ntfy, rabbitmq, smokeping, snipeit, speedketchup, uptime-kuma, victoria-logs, victoria-metrics, zabbix cinny, conduit, element, redlib, roundcube copyparty, filegator, nextcloud, syncthing, backrest, minio, restic-server, urbackup-client, urbackup-server|

|Database/Search||4|elasticsearch, nocodb, searxng, solr|
|---|---|---|---|
|Automation||2|n8n, nodered|
|Home-Automation||2|home-assistant, HA-otbr-matter|
|Messaging||1|mosquitto|
|Video/AI||2|frigate, viseron|
|Radio||1|openwebrx|
|AI||1|openwebui|
|Security||1|vaultwarden|
|Tips and Best Practices|Storage: Use external storage (USB/SATA/NVMe) for better performance and capacity Memory: Monitor application memory usage through /app print Updates: Enable auto-update for security and feature updates Networking: Applications automatically handle port forwarding and URL generation Data Persistence: Application data is stored in configured storage paths and survives application restarts|||
