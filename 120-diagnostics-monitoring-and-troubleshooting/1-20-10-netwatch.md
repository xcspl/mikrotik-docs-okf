---
type: Reference
title: "Netwatch"
description: "src-address (Default: ) \"\" Source IP address which the Netwatch will try to use in order to reach the host. If address is not present, then the host will be considered as \"down\"."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Netwatch

Summary Properties Type-specific options ICMP probe options TCP-CONNECT TCP-CONNECT pass-fail criteria HTTP-GET probe options HTTPS-GET probe options HTTP-GET/HTTPS-GET probe pass/fail criteria DNS probe options Probe statistics/variables Generic: ICMP: TCP: HTTP: HTTPS: DNS: Logs Status Quick Example

## Summary

Netwatch monitors the state of hosts on the network. Monitoring can be done with the following probe types:

1) ICMP-pings to a specified IP address-hosts, with an option to adjust threshold values
2) Simple-uses ping, without use of advanced metrics
3) TCP conn, to test the TCP connection
4) HTTP GET/HTTPS GET, request against a server you are monitoring
5) DNS-sends DNS query to DNS server and checks for response. For each entry in the Netwatch table, you can specify an IP address, ping interval, and console scripts. The main advantage of Netwatch is its ability to issue arbitrary console commands on host state changes. Since 7.4, Netwatch functionality has been expanded, prior versions only support simple ICMP probes. While upgrading to the new version, old Netwatch entries will be unchanged, reporting probe type "simple" - preserving the same functionality. Default Netwatch values are always used -  even if they were not defined by the user. Make sure to check the "status" page of the probe to see if the default thresholds are appropriate for your use case. Default threshold values can be found under the "probe options" section on this page.
## Properties

Sub-menu: /tool/netwatch

Property Description

host (Default:"") The IP address of the server to be probed. Formats:

- ipv4 - ipv4@vrf - ipv6 - ipv6@vrf - ipv6-linklocal%interface

- domain name (for type=dns)

type (icmp | tcp-conn | http-get | ht Type of the probe: simple;tp-get | dns | Default: simple- icmp - (ping-style) series of ICMP request-response with statistics )- tcp-conn-test TCP connection (3-way handshake) to a server specified by IP and port

- http-get-do an HTTP Get request and test for a range of correct replies
- https-get-do an HTTP Get request and test for a range of correct replies
- dns-do a specified DNS query for domain name
- simple-simplified ICMP probe, with fewer options than "ICMP" type, used for backward compatibility with the older Netwatch version
interval (Default: 10s) The time interval between probe tests

timeout (Default: 3s) Max time limit to wait for a response

src-address (Default: ) "" Source IP address which the Netwatch will try to use in order to reach the host. If address is not present, then the host will be considered as "down".

start-delay (Default: 3s) Time to wait before starting probe (on add, enable, or system start)

startup-delay (Default: 5m) Time to wait until starting Netwatch probe after system startup

up-script (Default:"") Script to execute on the event of probe state change 'fail' --> 'OK'

down-script (Default:"") Script to execute on the event of probe state change 'OK' --> 'fail'

test-script (Default:"") Script to execute at the end of every probe test

ignore-initial-up (no | yes; Default: Specifies if "Up" script should be ran if probe state change goes from `Unknown` to 'Up', used to help against false no) positives after enabling the probe, or after a reboot. "no" means that change from Unknown to Up will not be ignored.

ignore-initial-down (no yes |; Specifies if "Down" script should be ran if probe state change goes from `Unknown` to 'Down'. "no" means that Default: no) change from 'Unknown' to 'Down' will not be ignored.

Should be used with care, as first "Down" status won't be executed, and Down script will only be ran if probe goes through "Up" > "Down" state.

Netwatch executes scripts as *sys user, so any defined global variable in the Netwatch script will not be readable by for an example a scheduler or other users

Netwatch is limited to read,write,test,reboot script policies. If the owner of the script does not have enough permissions to execute a certain command in the script, then the script will not be executed. If the script has greater policies than read,write,test,reboot-then the script will not be executed as well, make sure your scripts do not exceed the mentioned policies.

It is possible to disable permission checking for RouterOS scripts under /system/scripts menu. This is useful when Netwatch does not have enough permissions to execute a script, though this decreases overall security. It is recommended to assign proper permissions to a script instead.

## Type-specific options

All config options specific to one probe type (e.g. icmp's packet-interval) are ignored for other probe types.

### ICMP probe options

|Property|Description|
|---|---|
|packet-interval (Default: 50ms)|The time between ICMP-request packet send|
|packet-count (Default: 10)|Total count of ICMP packets to send out within a single test|
|packet-size (Default: 54 (IPv4) or 54 (IPv6))|The total size of the IP ICMP packet|

thr-max (Default: 1s) Fail threshold for rtt-max (a value above thr-max is a probe fail)

thr-avg (Default: 100ms) Fail threshold for rtt-avg (round trip time-avg)

thr-stdev (Default: 250ms) Fail threshold for rtt-stdev

thr-jitter (Default: 1s) Fail threshold for rtt-jitter

thr-loss-percent (Default: 85.0%) Fail threshold for loss-percent

thr-loss-count (Default: 4294967295( Fail threshold for loss-count max))

|max))|||
|---|---|---|
|ttl (Default; 255)||Manually set time to live value for ICMP packet|
|accept-icmp-time-exceeded (yes no|||; If the ICMP "time exceeded" message should be considered a valid response|
|Default no)|||
|early-failure-detection (no yes||;|Netwatch will not wait to finish all the packets to be processed to change probe status if it is already known that|
|Default: no)||host will be considered as "down".|
|early-success-detection (no yes||;|Netwatch will not wait to finish all the packets to be processed to change probe status if it is already known that|
|Default: no)||host will be considered as "up".|

accept-icmp-time-exceeded=yes can be used together with a manually set low ttl value to monitor Internet connectivity, without relying on a specific endpoint.

For example, you can monitor a public IP address, but that address can filter your ICMP request, or just become unreachable itself, if the Netwatch probe is using this address to monitor Internet connectivity this would cause a false alarm.

To make sure you can reach the Internet, it's generally enough to make sure you can reach a device a few routing hops away. Low time to live value will expire in transit to the specified host you want to monitor-each router passing the ICMP packet will subtract "1" from TTL value, upon TTL reaching 0, ICMP "time exceeded" packet will be generated, and sent back to the Netwatch probe. If all other fail thresholds are not broken, this response will be considered a success.

When writing Up/Down/Test scripts for Netwatch, use the rtt-* elements instead of the thr-* elements. If the element names differ, their script- specific forms are listed in the description.

Simple, ICMP, HTTP, and TCP-connect probes are sent with the "don't fragment" flag set. With an ICMP probe, you can set packet-size, which in combination with the DF flag, can be used to aid with path MTU discovery

TCP-CONNECT

Property Description

port (Default: 80) TCP port (for both tcp-conn and http-get probes)

### TCP-CONNECT pass-fail criteria

Property Description

thr-tcp-conn-time (Default: 0 Fail threshold for tcp-connect-time, the configuration uses microseconds, if the time unit is not specified (s/m/h), log and 0:05...00:30) status pages display the same value in milliseconds.

### HTTP-GET probe options

|Property|||Description|||
|---|---|---|---|---|---|
||port (Default: 80)|HTTPS-GET probe options||TCP port (for both tcp-conn and http-get probes)||
|Property|port (Default: 443) certificate (Default:"") check-certificate (yes no|||; Default no)|HTTP-GET/HTTPS-GET probe pass/fail criteria|Description TCP port (for both tcp-conn and http-get probes) Certificate from local store that should be used for host verification. Enables trust chain validation from local certificate store.|
|Property|||Description|||
|Property|||||Description|
|) dns-server Generic:|host (Default:"") record-type (| would be $"done-tests"|A AAAA MX NS | Probe statistics/variables|||; Default: A|DNS name that should be resolved. Record type that will be used for DNS probe. The DNS server that the probe should send its requests to, if not specified it will use the value from "/ip dns". You can view statistics and use these variables in scripting, keep in mind that variables containing "-" must be written like this, for example, "done-tests"|
|Property||Description||||
|name comment host type interval timeout|interval timeout|user added comment host that was probed probe type|user added name for the Netwatch entry|||

00) 99) thr-http-time (Default: 10s) http-code-min (Default: 1 http-code-max (Default: 2 DNS probe options status or   rfc7231 Fail threshold for http-resp-time OK/fail criteria for HTTP response code. Response in the range [http-code-min,   http-code-max] is a probe pass/OK; outside-a probe fail. See mozilla-http-

since The last time the status change happened

status The current status of probe

done-tests total count of probe tests already done so far

failed-tests count of failed probe tests

ICMP:

Property Description

sent-count ICMP packets sent out

response-count Matching/valid ICMP packet responses received

thr-loss-count number of lost packets

thr-loss-percent number of lost packets in percent

thr-avg mean value of round trip time (rtt-avg)

thr-max max round trip time (rtt-max)

thr-jitter jitter ( = max-min) of round trip time (rtt-jitter)

thr-stdev standard deviation of round trip time (rtt-stdev)

TCP:

Property Description

tcp-connect-time time taken to establish a TCP connection

HTTP:

Property Description

http-status-code HTTP response status code (200 OK, 404 Not Found, etc.). See mozilla-http-status or RFC7231

HTTPS:

Property Description

http-status-code HTTP response status code (200 OK, 404 Not Found, etc.). See mozilla-http-status or RFC7231

DNS:

|Property|Description|
|---|---|
|ip|IP address-the result of A record-type probe|
|ip6|IPv6 address-the result of AAAA record-type probe|
|mail-servers|Mail servers along with their priority-the result of MX record-type probe|
|name-servers|Name servers-the result of NS record-type probe|

## Logs

On each probe's OK/fail state change:

probe identification info and OK->fail or fail->OK is printed to info level detailed probe stats and config is printed to debug level

## Status

Command /tool/netwatch/print will show the current status of Netwatch and read-only properties:

since-Indicates when a state of the host changed last time; status-Shows the current status of the host; host-address being monitored

## Quick Example

Here we will use a simple ICMP check to host with IP 8.8.8.8:

[admin@MikroTik] > /tool/netwatch add host=8.8.8.8 interval=30s up-script=":log info \"Ping to 8.8.8.8 successful\""

Afterward, in the logging section we can see Netwatch executed script:

[admin@MikroTik] > log print where message~"8.8.8.8" 08:03:26 script,info Ping to 8.8.8.8 successful
