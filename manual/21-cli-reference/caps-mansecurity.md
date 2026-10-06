---
type: Reference
title: "/caps-man/security"
description: "RouterOS directory reference for /caps-man/security"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/caps-man/security.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/caps-man/security.md
---

-----------

## caps-man/security 
**Package:** wireless-rep
**Type:** Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string" mandatory="1"></ArgTableRow>
<ArgTableRow arg="authentication-types" typ="ubit (wpa-psk, wpa2-psk, wpa-eap, wpa2-eap)" unset="1"></ArgTableRow>
<ArgTableRow arg="encryption" typ="ubit (aes-ccm, tkip)" unset="1"></ArgTableRow>
<ArgTableRow arg="group-encryption" typ="enum (aes-ccm | tkip)" unset="1"></ArgTableRow>
<ArgTableRow arg="group-key-update" typ="time"></ArgTableRow>
<ArgTableRow arg="passphrase" typ="string" unset="1"></ArgTableRow>
<ArgTableRow arg="eap-methods" typ="multi { array-id, method: enum (eap-tls | passthrough) { eap-tls:13, passthrough:0xffffffff }
 }" unset="1"></ArgTableRow>
<ArgTableRow arg="eap-radius-accounting" typ="bool" unset="1"></ArgTableRow>
<ArgTableRow arg="tls-mode" typ="enum (verify-certificate | dont-verify-certificate | no-certificates | verify-certificate-with-crl)"></ArgTableRow>
<ArgTableRow arg="tls-certificate" typ="enum (none) { none:0xffffffff }"></ArgTableRow>
<ArgTableRow arg="disable-pmkid" typ="bool" unset="1"></ArgTableRow>
</ArgTable>
