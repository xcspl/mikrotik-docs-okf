---
type: Reference
title: "/interface/ethernet/poe/settings"
description: "RouterOS settings reference for /interface/ethernet/poe/settings"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/ethernet/poe/settings.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/ethernet/poe/settings.md
---

-----------

## interface/ethernet/poe/settings 
**Syscap:** (poe or poe-in) and poesettings
**Type:** Settings Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="ether1-poe-in-long-cable" typ="bool" syscap="poeattiny"></ArgTableRow>
<ArgTableRow arg="psu-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="psu1-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="psu2-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="jack-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="jack1-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="jack2-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="2pin-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="2pin1-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="2pin2-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="poe-in-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="version" typ="string" syscap="poeattiny"></ArgTableRow>
<ArgTableRow arg="routerboard-max-self-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="routerboard-max-total-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="poe-out-limit-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="psu-poe-out-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="psu1-poe-out-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="psu2-poe-out-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="jack-poe-out-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="jack1-poe-out-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="jack2-poe-out-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="2pin-poe-out-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="2pin1-poe-out-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="2pin2-poe-out-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
<ArgTableRow arg="poe-in-poe-out-max-power" typ="num" syscap="poepwrchg"></ArgTableRow>
</ArgTable>
