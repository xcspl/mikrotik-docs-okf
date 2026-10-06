---
type: Reference
title: "/snmp/send-trap"
description: "RouterOS command reference for /snmp/send-trap"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/snmp/send-trap.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/snmp/send-trap.md
---

-----------

## snmp/send-trap 
**Type:** Command

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="oid" typ="string"></ArgTableRow>
<ArgTableRow arg="type" typ="enum (integer | string | nullobj | obj-id | ip-address | counter32 | timeticks | unsigned) { integer:0x02, string:0x04, nullobj:0x05, obj-id:0x06, ip-address:0x40, counter32:0x41, timeticks:0x43, unsigned:0x47 }"></ArgTableRow>
<ArgTableRow arg="value" typ="string"></ArgTableRow>
</ArgTable>
