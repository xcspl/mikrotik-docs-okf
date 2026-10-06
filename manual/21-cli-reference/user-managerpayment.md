---
type: Reference
title: "/user-manager/payment"
description: "RouterOS directory reference for /user-manager/payment"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/user-manager/payment.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/user-manager/payment.md
---

-----------

## user-manager/payment 
**Package:** userman-5
**Type:** Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="user" typ="enum"></ArgTableRow>
<ArgTableRow arg="profile" typ="enum"></ArgTableRow>
<ArgTableRow arg="price" typ="num"></ArgTableRow>
<ArgTableRow arg="currency" typ="string"></ArgTableRow>
<ArgTableRow arg="trans-start" typ="date"></ArgTableRow>
<ArgTableRow arg="trans-end" typ="alt { constant: enum (not-finished) { not-finished:0 }
, date: date
 }"></ArgTableRow>
<ArgTableRow arg="trans-status" typ="enum (started | pending | approved | declined | error | timeout | aborted | user-approved)"></ArgTableRow>
<ArgTableRow arg="method" typ="enum (paypal | authorize-net)"></ArgTableRow>
<ArgTableRow arg="user-message" typ="string"></ArgTableRow>
</ArgTable>
