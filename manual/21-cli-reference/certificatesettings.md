---
type: Reference
title: "/certificate/settings"
description: "RouterOS settings reference for /certificate/settings"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/certificate/settings.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/certificate/settings.md
---

-----------

## certificate/settings 
**Type:** Settings Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="builtin-trust-store" typ="alt { all-none: enum (default | all | untrusted)
, component: ubit (ipsec, wpa-eap, capsman, fetch, sstp, ovpn, mqtt, email, netwatch, radius, container, userman, lora, wiliot, openflow, tr069, dot1x, dns, www, api, reverse-proxy, logging)
 }">RouterOS provided CA certificates</ArgTableRow>
<ArgTableRow arg="current-defaults" typ="ubit (ipsec, wpa-eap, capsman, fetch, sstp, ovpn, mqtt, email, netwatch, radius, container, userman, lora, wiliot, openflow, tr069, dot1x, dns, www, api, reverse-proxy, logging)"></ArgTableRow>
<ArgTableRow arg="crl-download" typ="bool">auto CRL download and update</ArgTableRow>
<ArgTableRow arg="crl-use" typ="bool">perform CRL checking when validating trust chain</ArgTableRow>
<ArgTableRow arg="crl-store" typ="enum (system | ram)">CRL storage location</ArgTableRow>
</ArgTable>
