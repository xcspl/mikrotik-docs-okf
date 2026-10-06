---
type: Reference
title: "Socksify"
description: "Socksify is a service that allows the router to send specific traffic through a SOCKS proxy server, even if the application itself does not natively support proxy connections. It intercepts network calls and redirects th."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Socksify

## Introduction

Socksify is a service that allows the router to send specific traffic through a SOCKS proxy server, even if the application itself does not natively support proxy connections. It intercepts network calls and redirects them through configured SOCKS proxy.

Socksify service is used in combination with NAT action=socksify. All available firewall filters can be used to precisely select only per-application/source traffic to be redirected via socks proxy.

Multiple Socksify services can be configured simultaneously, which allows connections to multiple SOCKS servers for better traffic management.

### Property Description

/ip/socksify

|Property||Description|
|---|---|---|
|disabled (yes no yes)||; Default:|Whether the Socksify record is active.|
|socks5-password (string; Default: )||Password for the SOCKS5 proxy server access.|
|socks5-user (string; Default: )||Username for the SOCKS5 proxy server access.|
|connection-timeout (integer:||Time in seconds that specifies how long to wait for the SOCKS proxy or destination to respond during connection setup|
|0..3000; Default: 60)||before aborting with an error. Setting this value to 0 disables the connection timeout.|
|name (string; Default: )||Name of the Socksify service.|
|socks5-port (integer: 1.. 65535; Default: 1080)||Listening port of the SOCKS5 proxy server.|
|socks5-server (IPv4; Default : 0.0.0.0 )||IP address of the SOCKS5 proxy server. (only IPv4 addresses are supported)|
|port (integer: 1..65535; Default: 952)||TCP port which will be used by Socksify service.|

## Configuration examples

Use in combination with TOR SOCKS5 proxy server

Socksify can be used in combination with TOR to achieve better privacy and anonymity for the application that does not have integrated SOCKS support. Configuration below will allow you to forward HTTP/s traffic through TOR SOCKS5 proxy server. First you will need to configure socksify service.

/ip socksify add connection-timeout=10 disabled=no name=TOR_socksify socks5-port=9050 socks5-server=<TOR_SOCKS_proxy_IP>

After that you will need to configure firewall to ensure that correct traffic is being socksified and socks traffic is allowed.

/ip firewall filter add action=accept chain=input dst-port=952 protocol=tcp src-address=<SOCKS_client_IP> /ip firewall nat add action=socksify chain=dstnat dst-port=80,443 protocol=tcp socksify-service=TOR_socksify src- address=<SOCKS_client_IP>

### TOR container and secure DNS tutorial

Since RouterOS supports running containers, you could also set up the Tor proxy in a container. In addition to that, if you are going to be using Tor for browsing the web, you should consider protecting your DNS requests.

For detailed, step-by-step instructions watch the video here.
