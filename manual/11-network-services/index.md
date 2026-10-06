# Network Services

* [Network Services](network-services.md) - Network Services documentation provides configuration guides for essential network services including DHCP, DNS, ARP, Cloud services, proxy features, SOCKS, and OpenFlow to support network-facing operations

## Cloud

* [Cloud](cloud.md) - MikroTik cloud services in RouterOS: a DDNS name for the router, the clock and time zone at startup, cloud backup, Back To Home VPN and File Share. Which services are on by default and how the router reaches the
* [Back To Home](back-to-home.md) - Back To Home turns a RouterOS device into a WireGuard VPN server you can reach from anywhere, also behind NAT through a MikroTik relay. Set it up with the phone app, share tunnels with other people and computers, or
* [Cloud backup](cloud-backup.md) - Store one encrypted RouterOS backup on the MikroTik cloud server, replace or delete it, and download or restore it on the same or another router with its secret download key
* [Communication with MikroTik Cloud Services](communication-with-mikrotik-cloud-services.md) - Every connection RouterOS makes to MikroTik servers: the menu that starts it, the server, whether it runs by default, and how to turn it off
* [File Share](file-share.md) - File Share serves a directory or a single file from the router's storage over HTTPS through a secret link, with a Let's Encrypt certificate and a routingthecloud.net name, directly or through a MikroTik relay,

## DHCP

* [DHCP](dhcp.md) - How DHCP and DHCPv6 work in RouterOS: address assignment, leases and renewal, conflict checks, client identification, options and relays, and which RouterOS component to use: the DHCP client, server and relay for
* [DHCP Client](dhcp-client.md) - The RouterOS DHCP client gets an IPv4 address and network settings for an interface from a DHCP server. This page explains what the client applies from a lease, the options it requests and sends, the routes it adds,
* [DHCP Server](dhcp-server.md) - The RouterOS DHCP server assigns IPv4 addresses and network settings to clients from IP pools, with static leases, networks, DHCP options and option sets, option matchers, RADIUS support, rate limiting and rogue DHCP
* [DHCP Relay](dhcp-relay.md) - DHCP relay forwards DHCP and DHCPv6 requests from clients to a DHCP server in another network, with optional relay agent information (option 82) and VRF support
* [DHCPv6 Client](dhcpv6-client.md) - The RouterOS DHCPv6 client requests IPv6 addresses and delegated prefixes (DHCPv6-PD) from a DHCPv6 server, adds received prefixes to IPv6 pools, and can run scripts on status changes
* [DHCPv6 Server](dhcpv6-server.md) - The RouterOS DHCPv6 server delegates IPv6 prefixes (DHCPv6-PD) and assigns IPv6 addresses to clients, with static bindings, RADIUS support and per-binding rate limiting
* [DNS](dns.md) - The RouterOS DNS resolver: use the router as the DNS server for your network, check and troubleshoot it, add local names, send domains to other servers, use domain names in the firewall, block ads with adlists, use
* [Openflow](openflow.md) - RouterOS supports OpenFlow protocols 1.0 and 1.3 for SDN integration, enabling centralized traffic management through controller applications that access switch data paths. It includes basic statistics support and

## Proxy

* [Proxy](proxy.md) - RouterOS has two web proxies: the web proxy forwards, filters and caches the web requests of clients on your network, and the reverse proxy makes web servers behind the router reachable over HTTPS by host name
* [Web Proxy](web-proxy.md) - The RouterOS web proxy fetches web content for the clients on your network. It filters requests by host name, path and method, caches plain HTTP content, sends requests through a parent proxy, and works as a regular
* [Reverse Proxy](reverse-proxy.md) - The RouterOS reverse proxy accepts HTTPS connections, selects a rule by the TLS server name and forwards the requests as HTTP to a server or container app behind the router

## SOCKS

* [SOCKS](socks.md) - The SOCKS proxy server in RouterOS: enable the server, restrict who can use it with the access list, authenticate clients with users, and monitor active proxied connections
* [Socksify](socksify.md) - Socksify forwards traffic chosen by firewall NAT rules through an upstream SOCKS5 server, so applications without SOCKS support can use a SOCKS proxy. Includes a Tor proxy example
