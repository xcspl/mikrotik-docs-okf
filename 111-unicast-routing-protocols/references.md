---
type: Reference
title: "References"
description: "BGP MED attribute is local to the router. It is also used in the output of iBGP peers."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# References

RFC 4364: BGP/MPLS IP Virtual Private Networks (VPNs)

MPLS Fundamentals, chapter 7, Luc De Ghein, Cisco Press 2006

||Filter Syntax|Route Filtering Route Selection Routing Filter Wizard Route Filtering|Filter Syntax Operators Deleting BGP Communities AS-PATH Regexp Matching Community and Num Lists|Route Selection and Filters Only Readable Properties Writeable Properties Commands Matcher Operators Num Prop Operators Prefix Operators BGP Community Operators String Operators Regex Testing Tool Supported Operators The routing filter rule implements script-like syntax. The example below is a quick demonstration of a routing filter that matches prefixes with a prefix length greater than 24 from subnet 192.168.1.0/24 and increments the default distance by 1. If there is no match then subtract the default distance by one.|
|---|---|---|---|---|
||[matchers]: [actions]:|/routing filter rule add chain=myChain \ There are two types of properties: Example without boolean operator:|Filter rule may consist of multiple matchers and actions: [action] [prop writeable] [value] if (protocol connected) {accept}|rule="if (dst in 192.168.1.0/24 && dst-len>24) {set distance +1; accept} else {set distance -1; accept}" if ([matchers]) {[actions]} else {[actions]} only readable-ones that value is only readable and cannot be rewritten, these properties can be used only by matchers readable/writable-ones that value is readable and writeable, used by filter actions, and also can be used by matchers Readable properties can be matched by other readable properties (for numeric properties only) or constant values using boolean operators. [prop readable] [bool operator] [prop readable] The boolean operator is not used if there is only one possible operation.|

Example with boolean operator:

if ( bgp-med < 30 ) { accept }

With readable flag properties, matcher is used without specified boolean operator and without value

if ( ospf-dn ) { reject }

Be aware that the default action of the routing filter chain is "reject"

Only Readable Properties

Property Type

Numeric properties

dst-len

bgp-path-len

bgp-input- local-as

bgp-input- remote-as

bgp-output- local-as

bgp-output- remote-as

ospf-metric

ospf-tag

rip-metric

rip-tag

Flag properties

active

bgp-atomic- aggregate

bgp- communities- empty

bgp-ext- communities- empty

bgp-large- communities- empty

bgp-network

Description

Destination prefix length

The current length of the BGP AS-PATH

AS number of the local peer to which the prefix was sent

AS number of the remote peer from which the prefix was received

AS number of the peer that will advertise the prefix

AS number of the peer to which the prefix will be advertised

Current OSPF metric

Current OSPF tag

Current RIP metric

Current RIP tag

indicates whether the route is active

indicates if the BGP Communities attribute is empty

indicates if the BGP Extended Communities attribute is empty

indicates if the BGP Large Communities attribute is empty

Indicates if the prefix is originated from BGP networks

ospf-dn

Prefix properties

dst

ospf-fwd

bgp-input- local-addr

bgp-input- remote-addr

bgp-output- local-addr

bgp-output- remote-addr

Other Properties

afi ipv4 | ipv6 | l2vpn | l2vpn-cisco | vpnv4 | vpnv6

bgp-as-path numeric_regexp

bgp-as-path-string_regexp slow-legacy

chain chain_name

origin string

ospf-type ext1 | ext2 | inter | intra | nssa1 | nssa2

Indicates if the OSPF route has DN bit set.

Destination

Current OSPF forwarding address

The IP address of the local peer to which the prefix was sent

The IP address of the remote peer from which the prefix was received

The IP address of the peer that will advertise the prefix

The IP address of the peer to which the prefix will be advertised

The address family of the route.

AS path matching, read more>>

Deprecated. Extremely slow old-style AS path matching. This parameter should be used only as a temporary matcher while migrating from an old ROS v6 config. Read more>>

Match route's origin instance, for example it can match routes imported from specific OSPF instance: "if (origin <instance_name>) {}"

Type of the OSPF route:

ext1 - external (Type 5 LSA) with type1 metric ext2 - external (Type 5 LSA) with type2 metric inter-inter-area-route (Type 3 LSA) intra-intra-area-route (Type 4 LSA) nssa1 - Type 7 LSA with type1 metric nssa2 - Type 7 LSA with type1 metric

Protocol type from which the route was imported.

RPKI validation status of the prefix

Name of the routing table the route was imported from

Name of the VRF the route was imported from

protocol bgp | connected | dhcp | fantasy | modem | ospf | rip | static | vpn

rpki invalid | unknown | valid | unverified

rtab routing_table_name

vrf vrf_name

Writeable Properties

Property Type Description

Numeric properties

distance route distance

scope

scope-target scope target

bgp- weight

bgp-med

bgp-out- med

bgp-local- pref

bgp-igp- metric

bgp-path- peer- prepend

bgp-path- prepend

ospf-ext- metric

ospf-ext- tag

rip-ext- metric

rip-ext-tag

Flag properties

ospf-ext- dn

blackhole

suppress- hw-offload

use-te- nexthop

Other properties

gw ipv4/6 address

BGP WEIGHT attribute

BGP MED attribute is local to the router. It is also used in the output of iBGP peers.

BGP MED attribute to be sent to a remote peer. Should be used in the output chain of eBGP peers.

BGP LOCALPREF attribute

BGP IGP METRIC

Prepend last received remote peers ASN. If the prefix is originated from the router, then this parameter will not do anything on the router's output, because ASN does not exist yet.

If used as a matcher in BGP input, it is possible to filter prefixes exceeding a certain number of prepends. For example, if a remote peer prepends its ASN 5 times, but we want to allow max 4 times prepended ASN, then we can use: "if (bgp-path-peer-prepend > 4) {reject}"

This parameter also overrides any prepends received from the remote peer, for example, if the remote peer prepended it's AS 3 times, we can remove this prepend by setting "bgp-path-peer-prepend 1" in BGP input

Prepend routers ASN, should be used in BGP output.

OSPF External route metric

OSPF external route tag

RIP External route metric

RIP External route tag

DN bit for external OSPF routes

Whether to suppress L3 HW offloading

IPv4/IPv6 address or interface name. In the case of BGP output, a gateway can be adjusted in the following setups:

is BGP reflector nexthop-choice is set to propagate is not eBGP and nexthop-choice=force-self is not set.

ipv6 link local nexthop attribute. In the case of BGP output, a gateway can be adjusted in the following setups:

is BGP reflector nexthop-choice is set to propagate is not eBGP and nexthop-choice=force-self is not set.

gw-ll ipv6 link-local

gw- interface

gw-check

pref-src

bgp-origin

ospf-ext- fwd

ospf-ext- type

comment

bgp- communiti es

bgp-ext- communiti es

bgp-large- communiti es

Commands

Command

accept

reject

return

jump

unset

append

filter

delete

set

interface_name Interface part of the gateway. Should be used if it is required to attach a specific interface for next-hop, like (1.2.3.4% ether1)

*none|arp|icmp* *|bfd|bfd-mh*

ipv4/6 address

*igp|egp|incom* *plete*

ipv4/6 address Forwarding address of External OSPF route

*type1|type2* OSPF External route type

string

inline_community BGP Communities attribute is defined in RFC 1997. Each community is 32-bit in size. _set | community_list_n ame

inline_ext_commu BGP Extended Communities attribute is defined in RFC 4360. RouterOS parses site-of-origin (prefixed with soo:) and nity_set | route-target (prefixed with rt:) extended communities. For example, "set bgp-ext-communities rt:1111:2.3.4.5;". It is
ext_community_li possible to set/match RAW extended communities value in 64-bit hex, for example, "set bgp-ext-community 0x.........;"
st_name

inline_large_com BGP Large Communities attribute is defined in RFC 8092. Suitable for use with all ASNs including 32-bit ASNs. Each munity_set | community is 12-bytes in length and consists of 3 parts: "global_admin:locap_part_1:local_part_2". large_community _list_name

Params Description

accept matched prefix and stop processing the chain.

reject matched prefix and stop processing the chain, the prefix will be stored in the memory as "filtered" and will not be the candidate to be selected as the best path.

return to the parent chain

*jump* jump to a specified chain *chain_n* *ame*

*unset* used to unset the value of the following properties: *prop_na* pref-src|bgp-med|bgp-out-med|bgp-local-pref *me*

append at the end of the list or string. Following property values can be appended: bgp-communities, bgp-ext- communities, bgp-large-communities, comment

Inverse of the delete action (Delete everything except the specified values). Values of the following properties can be filtered: bgp-communities, bgp-ext-communities, bgp-large-communities

Delete the value of the specified property. Values of the following properties can be deleted: bgp-communities, bgp- ext-communities, bgp-large-communities

*set* The command is used to set a new value to writeable properties. Value can be set from other readable properties of *prop_wr* matching types. For numeric properties, it is possible to prefix the value with +/- which will increment or decrement the *iteable* current property value by a given amount. For example, "set bgp-local-ref +1" will increment current LOCAL_PREF *value* by one, or extract value from other readable num property, "set distance +ospf-ext-metric"

Enable RPKI verification in the current chain from the specified RPKI group.

|rpki-verify|rpki-||
|---|---|---|
||verify rpki_gr oup_name||
|Operators|||
|Matcher Operators|||
|Operator|Description|Example|
|&&|Logical AND operator|if (dst in 192.168.0.0/16 && dst-len in 16-32) {reject;}|
||||Logical OR operator||
|not Num Prop Operators|Logical NOT operator|if ( not bgp-network) {reject; }|
|Operator|Description||
|in|return true if the value is in provided numeric range. Numeric range can be written in following formats: {int..int}, {int-int}||
|==|return true if numeric values are equal||
|!=|return true if numeric values are not equal||
|>|return true if the left numeric value is greater than the right numeric value||
|<|return true if the left numeric value is less than the right numeric value||
|>=|return true if the left numeric value is greater than or equal to the right numeric value||
|<= Prefix Operators|return true if the left numeric value is less than or equal to the right numeric value||
|Operator|Description||
|in|Return true if the prefix is the subnet of the provided network. If an operator is used to match prefixes from the address list (e.g "dst in list_name"), then it will match only the exact prefix.||
|!=|Return true if the prefix is not equal to the provided value||
|==|Return true if the prefix is equal to the provided value||

Address lists by design are matching host address which menas that it will match also  /32 prefix that belongs to any range from the address list. Workaround to exclude /32  prefixes from being advertised is to use dst-len "if (dst in list_name && dst-len < 32) {}"

BGP Community Operators

Operator Description Example

equal return true if provided communities are equal to the routes property value

equal-list return true if communities from provided community-list are equal to the route's property value

any returns true if the route's property value contains at least one of provided communities

any-list returns true if the route's property value contains at least one community from the provided list

includes returns true if the route's property value includes specified communities

includes-list returns true if the route's property value includes all communities from the specified communities-list

subset returns true if route community subset matches communities from the list 1:1,3:3 will match 1:1,2:2,3:3

subset-list the same as "subset", but matches communities form the community list.

any-regexp the same as "any", but matched by regexp

subset-regexp the same as "subset", but matched by regexp

String Operators

Operator Description

find Check if provided substring is part of the property value

regexp Match string regexp of the property value

### Deleting BGP Communities

Routing filters allow to clear BGP communities by using "delete" command. Delete command accepts several parameters based on the type of the community type:

communities: "wk" - will match and remove well known communities "other" - will match and remove other communities that are not well known "regexp" - regexp pattern to match communities that should be deleted "<community-list name>" - deletes communities from specified community-list ext-communities: " " - will match and remove rt RouteTarget "soo" - will match and remove Site-of-Origin "other" - will match and remove other ext communities that are not RT or SSO "regexp" - regexp pattern to match ext communities that should be deleted "<community-ext-list name>" - deletes communities from specified community-ext-list large-communities: "all" - removes everything "regexp" - regexp pattern to match large communities that should be deleted "<community-large-list name>" - deletes large communities from specified community-large-list

It is possible to specify multiple community types, for example delete all SSOs, other type of ext communities and specific RTs from the community-ext list:

/routing/filter/community-ext-list add list=myRTList communities="rt:1.1.1.1:222" /routing/filter/rule add chain=myChain rule="delete bgp-ext-communities sso,other,myRTList;"

### AS-PATH Regexp Matching

AS Path is the sequence of autonomous system numbers (ASNs), for example AS Path 123 456 789 would indicate, that route originated from AS with the number 789, and to reach the destination, the packet would need to travel through two autonomous systems: 456 and 789. To apply specific routing policies administrator might want to match specific AS numbers or set of numbers in the AS Path (for example, reject prefixes that travel through AS 456), which can be achieved using regular expression (regexp).

There are two common ways how to operate with AS Path data:

convert whole AS path to string and let regexp operate on the string (ROS v6 or Cisco style) let regexp operate on each entry in the AS path as a number (ROS v7, Juniper style)

Basically, the first method is performing the match per character, the second method is performing the match per whole AS number. As you would imagine the latter method is much faster and less resource-intensive than the string matching approach.

||they will result either in syntax errors or unexpected results. Let us take a very basic AS Path filter rule. /routing/filter/rule add chain=myChain rule="if (bgp-as-path .1234.) {accept}"|This change would require administrators to implement new Regex strategies. Old Regex patterns from RouterOS v6 cannot be directly copied/pasted as|||
|---|---|---|---|---|
||dangerous configurations in some scenarios. regular expression, aka "^$". bgp-path-len should be used instead. Regex Testing Tool tested against any as-path before applying it to the routing filters. /routing/filter/num-list add list=test range=100-1500 /routing/filter/test-as-path-regexp regexp="[[:test:]]5678\$" as-path="1234,5678" Supported Operators|In ROS v7 this Regex pattern will match ASN 1234 anywhere in the middle of the AS-path, the same pattern in ROS v6 would match any AS path that contains ASN consisting of at least 6 characters and contains a string of "1234".  Obviously, if we directly copy/paste the Regex pattern from one implementation to another it will lead to unexpected/dangerous results. An equivalent pattern in ROS v6 would look something like this: "._1234_.". Let's take another example from ROS v6, say we have a pattern "1234[5-9]" what it does is it matches 12345 to 12349 anywhere in the string, which means that valid matches are AS-path "12345 3434", "11 9123467 22" and so on. If you enter the same pattern in ROS v7 it will match AS path containing exact ASN 1234 followed by ASN in a range from 5 to 9 (matching AS-paths would be "1234 7 111", "111 1234 5 222" etc., it will not match "12345 3434"). Do not copy Regex patterns directly from ROS v6 or Cisco configurations, they are not directly compatible. It can lead to unexpected or even AS-Path parameter must exist for regexp matcher to be applied. This means that it is not possible to match non-existent (empty) AS-Path with RouterOS now has a built-in regex checking tool to simplify the hard life of the administrators. This tool supports also num-list so now exact regex can be|||
|Operator|Description|Example|Example Explained|Example Matches|
|^ $ *|Represents the beginning of the path Represents the end of the path Zero or more occurrences of the  listed ASN|^1234 1234$ ^1234*$|will match AS-path starting with ASN 1234 will match AS-path of origin ASN 1234 will match Null as-path or as-path where ASN 1234 may or may not appear multiple times|Match: 1234 1234 1234 1234 Null path No Match: 1234 5678|

+ One or more occurrences of the listed ASN 1234+ will match AS-path where ASN 1234 appears at least once Match: 1234 3 1234 6 No match: 12345 678 ? Zero or one occurrence of the listed ASN ^1234? will match AS-path that may or may not start with ASN Match: 5678 1234 appearing once. 5678 1234 5678 No match: 1234 1234 5678 12345 5678. One occurrence of any ASN ^.$ will match any AS-path with the length of one. Match: 12345 45678 No match: 1234 5678 | Match one of two ASNs on each side ^ will match AS-path starting with ASN 1234 or 5678 Match: (1234|5678) 1234 5678 1234 5678 No Match: 91011 [] Represents the set of AS numbers where one AS number ^[1234 will match the AS-path that starts with 1234 or 5678 or from Match: from the list must match. 5678 1-100] the range of 1 to 100 [^] 1234 Use ^ after opening the bracket to negate the set. 99 It is also possible to reference the pre-defined num-lists from n um-list with [[:numset_name:]] 5678 No Match: 101 () Group of regexp terms to match ^ will match AS-path that starts and ends with 1234 or AS-Match: (1234$|567 path that starts with 5678

8) 1234
5678 9999 No Match: 1234 5678

Repetition ranges {} are not supported.

### Community and Num Lists

A list of commonly used numbers can be configured from the /routing/filter/num-list menu. These lists of numbers can be used in the filter rules to simplify the filter setup process.

In a similar manner, you are allowed to define also community, extended community, and large community lists. Community sets can be used for matching, appending, and setting.

For example match communities from the list and clear the attribute:

/routing/filter/community-list add communities=111:222 list=myCommunityList

/routing/filter/rule add chain=myChain rule="if (bgp-communities equal-list myCommunityList) {delete bgp-communities wk,other; accept;}"

## Route Selection

Route selection rules allow controlling how output routes are selected from available candidate routes. By default, (if no selection rules are set) output always picks the best route.

For example, if we look at the routing table below, we can see that there are 2 candidate routes and one best route. By default when BGP selects which route to send out, it will pick the active route.

[admin@4] /routing/route> print where dst-address=1.0.0.0/24 Flags: A-ACTIVE; b, y-COPY Columns: DST-ADDRESS, GATEWAY, AFI, DISTANCE, SCOPE, TARGET-SCOPE, IMMEDIATE-GW DST-ADDRESS GATEWAY AFI DISTANCE SCOPE TARGET-SCOPE IMMEDIATE-GW b 1.0.0.0/24 10.155.101.217 ip4 19 40 30 10.155.109.254%ether1 Ab 1.0.0.0/24 10.155.101.232 ip4 20 40 30 10.155.109.254%ether1 b 1.0.0.0/24 10.155.101.231 ip4 20 40 30 10.155.109.254%ether1

But there might be cases where you would want preference for other routes, not the active ones, and here come in-play selection rules.

Selection rules in RouterOS are configured from /routing/filter/select-rule menu.

Select rules can also call routing filters where routes get selected based on filter rules. For example, to mimic default output selection we can set up the following rule sets:

/routing filter rule add chain=get_active rule="if (active) {accept}"

/routing filter select-rule add chain=my_select_chain do-where=get_active

## Routing Filter Wizard

Cmd: /routing/filter/filter-wizard

Due to incresed complexity of writing filters in script like manner, v7.20 introduces new routing filter wizard that allows to generate filter rules with ROSv6- like syntax. Quick demonstration:

[admin@CCR2004_2XS_111] /routing/filter> filter-wizard <tab> action dst ospf-type scope-target set-gw-check use-te- nexthop afi dst-len protocol set-bgp-... set-scope bgp-... gateway routing-table set-blackhole set-scope-target blackhole jump-target-chain rpki set-comment set-suppress-hw-offload chain match-chain rpki-verify set-distance set-use-te-nexthop distance ospf-metric scope set-gateway suppress-hw-offload

[admin@CCR2004_2XS_111] /routing/filter> filter-wizard action=accept chain=vpn-in afi=vpnv4 set-bgp-ext- communities=rt:2:2 result: Filter rule 'if (afi vpnv4) { set bgp-ext-communities rt:2:2; accept; }' added

[admin@CCR2004_2XS_111] /routing/filter> /routing/filter/rule/print Flags: X-disabled, I-inactive 0 ;;; added by filter-wizard chain=vpn-in rule="if (afi vpnv4) { set bgp-ext-communities rt:2:2; accept; }"

added by filter-wizardFilter wizard adds rules at the end of the list and will have a comment " ".

Returned errors when trying to add filter with unacceptable values will be printed in CLI and logged in system log with "route,error" topics.

[admin@CCR2004_2XS_111] /routing/filter> filter-wizard action=accept chain=vpn-in afi=vpnv4 match-chain=vpn-in result: Error adding 'if (chain vpn-in && afi vpnv4) { accept; }'match with 'vpn-in' creates chain loop (6)

[admin@CCR2004_2XS_111] /routing/filter> /log/print 2025-05-19 13:05:15 route,error Error adding 'if (chain vpn-in && afi vpnv4) { accept; }'match with 'vpn-in' creates chain loop (6)
