---
type: Reference
title: "/cmr/upgrade/version-check"
description: "Lists the newest version available for each upgrade channel that is configured in an upgrade rule. Channels that no rule uses are not checked"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/cmr/upgrade/version-check.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/cmr/upgrade/version-check.md
---

-----------

## cmr/upgrade/version-check 
**Package:** cmr
**Type:** Command

Lists the newest version available for each upgrade channel that is configured in an upgrade rule. Channels that no rule uses are not checked.

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="channel" typ="alt">Channel checked.</ArgTableRow>
<ArgTableRow arg="version" typ="string">Available versions.</ArgTableRow>
</ArgTable>
