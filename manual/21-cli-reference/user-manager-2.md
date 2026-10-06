---
type: Reference
title: "/user-manager"
description: "RouterOS settings reference for /user-manager"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/user-manager.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/user-manager.md
---

-----------

## user-manager 
**Package:** userman-5
**Type:** Settings Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="enabled" typ="bool"></ArgTableRow>
<ArgTableRow arg="authentication-port" typ="num"></ArgTableRow>
<ArgTableRow arg="accounting-port" typ="num"></ArgTableRow>
<ArgTableRow arg="certificate" typ="enum (none)"></ArgTableRow>
<ArgTableRow arg="radsec-certificate" typ="enum (none)"></ArgTableRow>
<ArgTableRow arg="use-profiles" typ="bool"></ArgTableRow>
<ArgTableRow arg="require-message-auth" typ="enum (no | yes-access-request)"></ArgTableRow>
</ArgTable>
