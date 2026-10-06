# Diagnostics and Monitoring

* [Diagnostics and Monitoring](diagnostics-and-monitoring.md) - This section provides tools for inspecting traffic, testing connectivity, collecting logs, monitoring resources, analyzing flow data, and troubleshooting network or device issues in RouterOS
* [Ping](ping.md) - The RouterOS ping tool: check that a host or the internet is reachable, read the status of each reply, find the path MTU, ping from a chosen address, interface or VRF, reach hosts that block ICMP with ARP and ND
* [Traceroute](traceroute.md) - The RouterOS traceroute tool: list the routers on the path to a host, read the per-hop loss and round-trip statistics, find where a path breaks, loops or is filtered, and trace from a VRF or a chosen source address
* [Torch](torch.md) - Torch shows the traffic that passes one interface right now, grouped into flows by address, protocol, port and DSCP, with the rate in each direction. Find the host that uses the bandwidth, watch one protocol or port,
* [Packet Sniffer](packet-sniffer.md) - The RouterOS packet sniffer: capture packets on the router, filter them, watch them live in the console, save them to a pcapng file for Wireshark or stream them to a PC over TZSP, and know what the sniffer cannot see
* [Bandwidth test](bandwidth-test.md) - The bandwidth test measures TCP or UDP throughput between two MikroTik routers: the client in /tool/bandwidth-test sends to or receives from the bandwidth test server of the other router. It covers prerequisites,
* [Speed Test](speed-test.md) - Speed test measures ping, jitter and TCP and UDP throughput in both directions between two MikroTik routers in one run, through the bandwidth test server of the remote router
* [Flood Ping](flood-ping.md) - Flood ping sends a series of up to 1000 ICMP echo requests in one run and shows only the totals: requests sent, replies received and the shortest, average and longest round-trip time. It needs the traffic-gen
* [Interface stats and monitor-traffic](interface-stats-and-monitor-traffic.md) - This page documents MikroTik RouterOS interface statistics and monitor-traffic tools for real-time monitoring of network utilization, hardware performance, packet rates, and bitrates across physical and virtual
* [Traffic Generator](traffic-generator.md) - Traffic Generator is a MikroTik RouterOS tool for evaluating device performance by generating and sending raw packets over ports, collecting latency, jitter, throughput, and packet loss data. It supports advanced
* [Netwatch](netwatch.md) - Netwatch monitors network hosts using multiple probe types including ICMP, TCP, HTTP, DNS, and simple pings. It allows custom scripts for state changes and supports VRFs and link-local IPv6 addresses, with
* [Graphing](graphing.md) - RouterOS graphing: record CPU, memory and disk usage and interface and simple queue traffic over time, view the daily, weekly, monthly and yearly graphs on the router's /graphs/ web page or in WinBox, choose who can
* [SNMP](snmp.md) - This page documents SNMP configuration in MikroTik RouterOS, covering enabling the service, general settings like contact info and trap configurations, community access rights for SNMPv1/2c/3, and warnings about
* [Health](health.md) - This page documents MikroTik RouterOS hardware health monitoring features, detailing metrics like temperature, voltage, fan speed, and CPU status for supported devices. It includes CLI examples, warnings about device
* [Resource](resource.md) - The Resource menu in RouterOS provides overview of system statistics including uptime, memory, disk usage, and hardware details like CPU model and frequency. It also offers submenus for detailed per-CPU usage, IRQ,
* [Profiler](profiler.md) - The Profiler tool in RouterOS displays CPU usage for each process, helping identify resource-intensive processes. It supports per-core monitoring and classifies CPU usage by process type for efficient debugging
* [IP Scan](ip-scan.md) - IP scan finds the devices on a network: scan an address range to list the hosts with their MAC addresses, response times, DNS and SNMP names, or listen on an interface to see the addresses that devices use, including
* [Detect Internet](detect-internet.md) - Detect Internet gives each watched interface a state (lan, wan, internet and others) from its link, its routes and MikroTik cloud reachability, and keeps interface lists up to date with the result
* [DNS update](dns-update.md) - The DNS update tool sends an RFC 2136 dynamic update, signed with a TSIG hmac-md5 key, to the authoritative DNS server of a zone to point a name at an IPv4 address
* [Watchdog](watchdog.md) - Watchdog reboots the router when the system stops responding or when one IP address stops answering pings, and writes a support output file after a software failure
* [Downgrading RouterOS](downgrading-routeros.md) - Learn how to downgrade RouterOS to a previous version, including pre-downgrade checks, architecture verification, and step-by-step instructions

## Logs

* [Log](log.md) - RouterOS logs system events in topics; rules in /system/logging send them to memory, a disk, the console, a syslog server (UDP, TCP or TLS; syslog or CEF format), email or a script. Read the log with /log/print
* [CEF with Elasticsearch](cef-with-elasticsearch.md) - This guide explains how to configure CEF log collection and analysis using Elasticsearch, Kibana, and Fleet Server with MikroTik RouterOS devices. It covers prerequisites, setup steps for both Elastic and RouterOS
* [Syslog with Elasticsearch](syslog-with-elasticsearch.md) - This guide explains how to configure Syslog data collection and analysis using Elasticsearch, Kibana, and Fleet Server with MikroTik RouterOS devices. It covers prerequisites, setup steps for both Elastic and

## Traffic Flow

* [Traffic Flow](traffic-flow.md) - MikroTik Traffic-Flow provides network monitoring and accounting by collecting statistical information about packets passing through the router, supporting NetFlow versions 1, 5, 9, and IPFIX for flexible flow
* [NetFlow analysis with Elasticsearch](netflow-analysis-with-elasticsearch.md) - This guide explains how to set up NetFlow analysis with Elasticsearch on MikroTik RouterOS by configuring data collection from RouterOS devices to an Elasticsearch server, including Kibana integration and Fleet
