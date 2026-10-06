---
type: Reference
title: "/user-manager/user/add-batch-users"
description: "RouterOS command reference for /user-manager/user/add-batch-users"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/user-manager/user/add-batch-users.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/user-manager/user/add-batch-users.md
---

-----------

## user-manager/user/add-batch-users 
**Package:** userman-5
**Type:** Command

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="username-length" typ="num"></ArgTableRow>
<ArgTableRow arg="number-of-users" typ="num"></ArgTableRow>
<ArgTableRow arg="username-prefix" typ="string"></ArgTableRow>
<ArgTableRow arg="password-length" typ="enum (empty | same-as-username)"></ArgTableRow>
<ArgTableRow arg="username-characters" typ="ubit (uppercase, lowercase, numbers)"></ArgTableRow>
<ArgTableRow arg="password-characters" typ="ubit (uppercase, lowercase, numbers)"></ArgTableRow>
<ArgTableRow arg="profile" typ="enum"></ArgTableRow>
<ArgTableRow arg="group" typ="enum"></ArgTableRow>
<ArgTableRow arg="caller-id" typ="enum (bind)"></ArgTableRow>
<ArgTableRow arg="shared-users" typ="enum (unlimited) { unlimited:0x0 }"></ArgTableRow>
<ArgTableRow arg="disabled" typ="bool"></ArgTableRow>
<ArgTableRow arg="comment" typ="string"></ArgTableRow>
</ArgTable>
