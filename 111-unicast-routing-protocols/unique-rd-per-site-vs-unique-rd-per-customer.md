---
type: Reference
title: "Unique RD per-site vs unique RD per-customer"
description: "Let's consider BGP VPN setup where two CUSTA sites announce the same network (111.12.0.0/24)."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Unique RD per-site vs unique RD per-customer

Let's consider BGP VPN setup where two CUST_A sites announce the same network (111.12.0.0/24).

+----------+ +----------+ |+-vrf-+ | | +-vrf-+| CUST_A(10.12.0.0/24)-----|+-----+ |---(BGP VPN)---| +-----+|-------CUST_A(10.12.0.0/24) +----------+ +----------+

There are two ways to handle setups like this:

per-customer (CUST_A VPN on Router 1 have the same route distinguisher (lets assume RD=1:1) as CUST_A VPN on Router 2) per-site (each CUST_A site  have unique Route Distinguisher)

In first case CUST_A sites on Router1  have exported the VPNv4 route and advertise it to remote PE.

Ay afi=vpnv4 contribution=active dst-address=111.12.0.0/24&1:1 routing-table=main label=16 gateway=vrf- dummy@vrfTest immediate-gw=vrf-dummy distance=200 scope=40 target-scope=10 belongs-to="bgp-mpls-vpn-1-connected- export" bgp.ext-communities=rt:1:1 .origin=incomplete debug.fwp-ptr=0x20302600

CUST_A site on Router2 also exports VPNv4 route and has received VPNv4 route from another site as well:

Ab + afi=vpnv4 contribution=active dst-address=111.12.0.0/24&1:1 routing-table=main label=16 gateway=111.

11.0.2 immediate-gw=111.11.0.2%sfp-sfpplus1 distance=200 scope=40 target-scope=30 belongs-to="bgp-VPNv4-
111.11.0.2" bgp.session=to-tested-1 .ext-communities=rt:1:1 .local-pref=100 .origin=igp debug.fwp-ptr=0x203421E0 Ay + afi=vpnv4 contribution=active dst-address=111.12.0.0/24&1:1 routing-table=main label=32 gateway=vrf- dummy@vrfTest immediate-gw=vrf-dummy distance=200 scope=40 target-scope=10 belongs-to="bgp-mpls-vpn-1-connected- export" bgp.ext-communities=rt:1:1 .origin=incomplete debug.fwp-ptr=0x20342540
Currently RouterOS advertises only one best route. In case of ECMP by default it picks the first one from the list which happens to be BGP VPNv4 route received from remote site, and of course remote site will not get the second route. This leads to situation that one site has two redundant routes in the VRF but other site does not. On that site where VRF does not have installed VPN route and local route becomes inactive, BGP needs to send withdraw, recalculate main table, receive update from remote site and import new best route into CUST_A VRF, leading to slower convergence.

This behavior of course could be changed with route selection filters, but it is outside the scope of this example.

Similar situation happens if exported to VPNV4 route is also BGP route received from customers CE-PE session, except that now instead of ECMP, BGP best-path selection process is applied to VPNv4 routes and only one best is selected.

Now if we assign unique route-distinguisher per site, lets say (1.1.1.1:1 on first site and 1.1.1.2:1 on second site), there is no longer selection on VPNv4 routes because these are now considered unique destinations and both destinations are imported into VRF.

CUST_A on Router1

[admin@CCR2004_2XS_111] /routing/route> print detail ... Ay afi=vpnv4 contribution=active dst-address=111.12.0.0/24&1.1.1.1:1 routing-table=main label=17 gateway=vrf- dummy@vrfTest immediate-gw=vrf-dummy distance=200 scope=40 target-scope=10 belongs-to="bgp-mpls-vpn-1-connected- export" bgp.ext-communities=rt:1:1 .origin=incomplete debug.fwp-ptr=0x20302240

Ab afi=vpnv4 contribution=active dst-address=111.12.0.0/24&1.1.1.2:1 routing-table=main label=33 gateway=111.

11.0.1 immediate-gw=111.11.0.1%sfp-sfpplus1 distance=200 scope=40 target-scope=30 belongs-to="bgp-VPNv4-
111.11.0.1" bgp.session=to-tester-1 .ext-communities=rt:1:1 .local-pref=100 .origin=igp debug.fwp-ptr=0x20302480 [admin@CCR2004_2XS_111] /ip/route> print ... DAc 111.12.0.0/24 vrf-dummy@vrfTest vrfTest 0 D y 111.12.0.0/24 111.11.0.1 vrfTest 200
CUST_A on Router2

[admin@CCR2004_2XS_111] /routing/route> print detail ... Ab afi=vpnv4 contribution=active dst-address=111.12.0.0/24&1.1.1.1:1 routing-table=main label=17 gateway=111.

11.0.2 immediate-gw=111.11.0.2%sfp-sfpplus1 distance=200 scope=40 target-scope=30 belongs-to="bgp-VPNv4-
111.11.0.2" bgp.session=to-tested-1 .ext-communities=rt:1:1 .local-pref=100 .origin=igp debug.fwp-ptr=0x203421E0 Ay afi=vpnv4 contribution=active dst-address=111.12.0.0/24&1.1.1.2:1 routing-table=main label=33 gateway=vrf- dummy@vrfTest immediate-gw=vrf-dummy distance=200 scope=40 target-scope=10 belongs-to="bgp-mpls-vpn-1-connected- export" bgp.ext-communities=rt:1:1 .origin=incomplete debug.fwp-ptr=0x20342240 [admin@CCR2004_2XS_111] /ip/route> print ... DAc 111.12.0.0/24 vrf-dummy@vrfTest vrfTest 0 D y 111.12.0.0/24 111.11.0.2 vrfTest 200
In this case compared to previous setup, when local route from any of sites becomes inactive, switch to alternative route happens momentarily.
