---
type: Reference
title: "Reverse Proxy"
description: "Reverse proxy is a service that allows the router to send HTTPS traffic to servers or to RouterOS containers/apps when \"use-https\" parameter is enabled in app settings, behind the router using simple URL, instead of IP a."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Reverse Proxy

## Introduction

Reverse proxy is a service that allows the router to send HTTPS traffic to servers or to RouterOS containers/apps when "use-https" parameter is enabled in app settings, behind the router using simple URL, instead of IP address and creating separate destination NAT rule.

Please note that by default reverse-proxy service uses HTTPS port 443, same as a default www-ssl service port. For reverse-proxy to function correctly you need to ensure that www-ssl service is disabled or uses different TCP port. (/ip/service documentation)

### Property Description

|/ip/reverse-proxy|||
|---|---|---|
|Property||Description|
|disabled (yes no||;|Whether the reverse proxy record is active.|
|Default: yes)|||
|ip-address (IPv4;||IP address of the server, connection to which should be proxied. (only IPv4 addresses are supported)|
|Default: 0.0.0.0 )|||
|port (integer: 1..65535;||Listening port of the server.|
|Default: 0)|||
|sni (string; Default: )||Server Name Indication of the server.|
|certificate (certificate;||The name of the certificate used by a particular reverse-proxy instance. When set to none, reverse-proxy instance will use|
|Default: none)||certificate from reverse-proxy service set in ip/service menu.|
|comment (string;||Descriptive name of an item.|
|Default: )|||
