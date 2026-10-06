---
type: Reference
title: "IP Settings"
description: "Several IPv4 and IPv6 related kernel and system-wide parameters are configurable."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# IP Settings

Summary IPv4 Settings IPv6 Settings

## Summary

Several IPv4 and IPv6 related kernel and system-wide parameters are configurable.

## IPv4 Settings

Sub-menu: /ip settings

Property Description

accept-Whether to accept ICMP redirect messages. Typically should be enabled on a host and disabled on routers. redirects (yes | no; Default: no)

accept-Whether to accept packets with the SRR option. Typically should be enabled on the router. source-route ( yes | no; Default: no)

allow-fast-Allows Fast Path. path (yes | no; Default: yes)

arp-timeout (ti Sets Linux base_reachable_time (base_reachable_time_ms) on all interfaces that use ARP. The initial validity of the ARP entry is me interval; picked from the interval [timeout/2 - 3*timeout/2] (default from 15s to 45s) after the neighbor was found. Can use postfix ms, s, m, h, d Default: 30s)  for milliseconds, seconds, minutes, hours, or days. if no postfix is set then seconds (s) are used. The parameter means how long a valid ARP record will be considered complete if no one communicates with the specific MAC/IP during this time. The parameter does not represent a time when an ARP entry is removed from the ARP cache (see max-neighbor-entries setting).

icmp-errors-If enabled, the ICMP error message reply will be sent with the source address equal to primary address of the receiving interface that use-inbound-caused the error. This feature can be useful for complex network debugging. interface- address (yes | no; Default: no)

icmp-rate-Limit the maximum rates for sending ICMP packets whose type matches icmp-rate-mask to specific targets. 0 disables any limiting, limit (integer other values indicate the minimum space between responses in milliseconds. [0.. 4294967295]; Default: 10)

icmp-rate-Mask made of ICMP types for which rates are being limited. More info in Linux man pages mask ([0.. FFFFFFFF]; Default: 0x18

18) ip-forward (ye Enable/disable packet forwarding between interfaces. Resets all configuration parameters to defaults according to RFC1812 for s | no; routers. Default: yes)

Time in seconds to keep an IPv4 fragment in memory. Available staring with RouterOS version 7.23. ipv4- fragment- time (integer; Default: 3)

ipv4-high- fragment- thresh (integer; Default: )

ipv4- multipath- hash-policy(l3 | l4 | l3-inner; Default: l3)

rp-filter (loose | no | strict; Default: no)

secure- redirects (yes | no; Default: yes)

send- redirects (yes | no; Default: yes)

tcp- timestamps ( disabled | enabled | random-offset; Default: rand om-offset)

tcp- syncookies (y es | no; Default: no)

Sets the upper bound of memory (in bytes) the kernel may consume for all fragment reassembly queues combined (every interface and every flow). When the total memory used by the cache reaches this limit the kernel starts dropping newly arriving fragments, causing packets to be discarded. Raising the limit reduces the chance of drops under heavy fragmentation (e.g. high-throughput links with VPNs, or MTU-limited paths), but it also raises the maximum amount of RAM that can be used. Available staring with RouterOS version 7.23.

The default value depends on the installed amount of RAM:

512 KiB for 64 MiB of RAM, 1024 KiB for 128 MiB of RAM, 2048 KiB for 256 MiB of RAM, 4096 KiB for 512MiB of RAM, 16 MiB for 1 GiB of RAM, 32 MiB for 2 GiB of RAM or higher.

IPv4 Hash policy used for ECMP routing in /ip/settings menu

l3 -- layer-3 hashing of src IP, dst IP l3-inner -- layer-3 hashing or inner layer-3 hashing if available l4 -- layer-4 hashing of src IP, dst IP, IP protocol, src port, dst port

Disables or enables source validation.

no-No source validation. strict-Strict mode as defined in RFC3704 Strict Reverse Path. Each incoming packet is tested against the FIB and if the interface is not the best reverse path the packet check will fail. By default failed packets are discarded. loose-Loose mode as defined in RFC3704 Loose Reverse Path. Each incoming packet's source address is also tested against the FIB and if the source address is not reachable via any interface the packet check will fail.

The current recommended practice in RFC3704 is to enable strict mode to prevent IP spoofing from DDoS attacks. If using asymmetric routing or other complicated routing or VRRP, then the loose mode is recommended.

Warning: strict mode does not work with routing tables

Accept ICMP redirect messages only for gateways, listed in the default gateway list.

Whether to send ICMP redirects. Recommended to be enabled on routers.

Parameter allows to enable/disable TCP timestamps or add random offset to TCP timestamp (default behavior). Disabling timestamps completely may help to reduce spikes of performance drops.

Send out syncookies when the syn backlog queue of a socket overflows. This is to prevent the common 'SYN flood attack'. syncookies seriously violate TCP protocol, and disallow the use of TCP extensions, which can result in serious degradation of some services (f.e. SMTP relaying), visible not by you, but to your clients and relays, contacting you.

max-Sets Linux gc_thresh3. A maximum number of allowed neighbors in the ARP table. Since RouterOS version 7.1, the default value neighbor-depends on the installed amount of RAM. It is possible to set a higher value than the default, but it increases the risk of out-of- entries (integ memory condition. er [0.. 2147483647]; The default values for certain RAM sizes: Default: ) 2048 for 64 MiB, 4096 for 128 MiB, 8192 for 256 MiB, 16384 for 512 MiB or higher.

The ARP cache stores ARP entries, and if some of these entries are incomplete, they can stay in the cache for an indefinite period of time. This will only happen if the number of entries in the cache is less than one-fourth of the maximum number allowed. The reason for this is to prevent the unnecessary running of the garbage-collector when the ARP table is not close to being full.

route-cache ( Disable or enable the Linux route cache. Note that disabling the route cache, will also disable the fast path. yes | no; Default: yes)

|Read-Only Properties||
|---|---|
|Property|Description|
|ipv4-fast-path-active (yes | no)|Indicates whether fast-path is active|
|ipv4-fast-path-bytes (integer)|Amount of fast-pathed bytes|
|ipv4-fast-path-packets (integer)|Amount of fast-pathed packets|
|ipv4-fasttrack-active (yes | no)|Indicates whether fasttrack is active|
|ipv4-fasttrack-bytes (integer)|Amount of fasttracked bytes|
|ipv4-fasttrack-packets (integer)|Amount of fasttracked packet.|

## IPv6 Settings

Sub-menu: /ipv6 settings

Changing /ipv6 settings will not dynamically remove the old SLAAC configuration present on your router. A reboot is required to apply the new settings.

Property Description

accept-redirects (no | yes-if-forwarding-Whether to accept ICMP redirect messages. Typically should be enabled on the host and disabled on disabled; Default: yes-if-forwarding-disabled) routers

accept-router-advertisements (no | yes | yes-Accept router advertisement (RA) messages. If enabled, the router will be able to get the address if-forwarding-disabled; Default: yes-if-using stateless address configuration forwarding-disabled)

accept-router-advertisements-on (interface Specifies on which interfaces to listen for incoming router advertisements (RAs). list; Default: all)

disable-ipv6 (yes | no; Default: no) Enable/disable system wide IPv6 settings (prevents LL address generation)

forward (yes | no; Default: yes) Enable/disable packet forwarding between interfaces

|max-neighbor-entries (integer [0..||A maximum number or IPv6 neighbors. Since RouterOS version 7.1, the default value depends on|
|---|---|---|
|2147483647]; Default: )||the installed amount of RAM. It is possible to set a higher value than the default, but it increases the risk of out-of-memory condition. The default values for certain RAM sizes: 1024 for 64 MiB, 2048 for 128 MiB, 4096 for 256 MiB, 8192 for 512 MiB, 16384 for 1024 MiB or higher.|
|multipath-hash-policy (l3 | l4 | l3-inner; Default: l3)||IPv6 Hash policy used for ECMP routing in /ipv6/settings menu l3 -- layer-3 hashing of src IP, dst IP, flow label, IP protocol l3-inner -- layer-3 hashing or inner layer-3 hashing if available l4 -- layer-4 hashing of src IP, dst IP, IP protocol, src port, dst port|
|disabled-link-local-address (no | yes;||Disable automatic link-local address generation for non-VPN interfaces. This can be used when|
|Default: no)||manually configured link-local addresses are being used.|
|stale-neighbor-timeout (time ; Default: 60)||Timeout after which stale IPv6/Neighbor entries should be purged.|
|min-neighbor-entries (integer; Default: 4096)||Minimal number of IPv6/Neighbor entries, for which device must allocate memory.|
|soft-max-neighbor-entries (integer; Default:||Expected maximum number of IPv6/Neighbor entries which system should handle.|
|max-neighbor-entries (integer; Default:|16|Maximum number of entries for IPv7/Neighbor list.|
|allow-fast-path (yes | no; Default: yes) Read-Only Properties||Allows Fast Path.|
|Property|Description||
|ipv6-fast-path-active (yes | no)|Indicates whether fast-path is active||
|ipv6-fast-path-bytes (integer)|Amount of fast-pathed bytes||
|ipv6-fast-path-packets (integer)|Amount of fast-pathed packets||
|ipv6-fasttrack-active (yes | no)|Indicates whether fasttrack is active||
|ipv6-fasttrack-bytes (integer)|Amount of fasttracked bytes||
|ipv6-fasttrack-packets (integer)|Amount of fasttracked packet.||

8192)
384)
