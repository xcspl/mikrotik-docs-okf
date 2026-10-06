---
type: Reference
title: "/ipv6/nd/settings"
description: "The IPv6 ND menu has a sub-menu 'Settings' which allows changing global neighbor discovery settings"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ipv6/nd/settings.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ipv6/nd/settings.md
---

-----------

## ipv6/nd/settings 
**Type:** Settings Directory

The IPv6 ND menu has a sub-menu "Settings" which allows changing global neighbor discovery settings.

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="router-advertisement-route-distance" typ="num">Specify the distance that must be used when installing SLAAC default route.</ArgTableRow>
<ArgTableRow arg="router-advertisement-ignored-options" typ="ubit (dns, mtu)">Lets you ignore specific received ND options such as DNS and MTU. If RA will contain such options, they simply will be ignored if selected on this list.</ArgTableRow>
</ArgTable>
