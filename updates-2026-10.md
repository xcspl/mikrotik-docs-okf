---
type: Reference
title: "RouterOS updates and current state (2026-10)"
description: "What has changed since this bundle's 2026-05-26 snapshot: current stable/LTS versions, the September 2026 security advisories, the v7-vs-v6 differences, and the current state of containers, ZeroTier, WireGuard, IPv6 and OSPFv3."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, updates, v7, security, container, zerotier, wireguard, ipv6, ospfv3]
resource: https://manual.mikrotik.com/docs/introduction/
sources:
  - resource: https://mikrotik.com/supportsec/september-2026-vulnerability
    last_modified: 2026-09-03
  - resource: https://forum.mikrotik.com/t/7-24-stable-is-released/272381
    last_modified: 2026-08-14
  - resource: https://forum.mikrotik.com/t/7-24-5-stable-is-released/273494
    last_modified: 2026-09-29
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/115736772/Upgrading+to+v7
  - resource: https://aviatrix.ai/threat-research-center/cisa-warns-critical-pre-auth-rce-flaw-mikrotik-routeros-cve-2026-84411
    last_modified: 2026-09-30
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# RouterOS updates and current state (2026-10)

**Baseline.** The rest of this bundle is the frozen legacy manual of
**2026-05-26** (see [Provenance](provenance.md)). This doc is what a web check
on **2026-10-06** found different or newer. Where a claim is a vendor statement,
the source is named; where it is forum/third-party, it says so.

## Versions

| Release | Date | Note |
|---|---|---|
| 7.22 stable | 2026-03-09 | wifi-mediatek driver/firmware update |
| 7.23 stable | 2026-05-25 | ~the snapshot date of this bundle's PDF |
| **7.24 stable** | 2026-08-14 | current stable line |
| **7.24.5 stable** | 2026-09-29 | latest point release seen |
| 7.23.7 | 2026-09-16 | **long-term** release |

Check `mikrotik.com/download/changelogs` (or `/system/package/update/
check-for-updates`) — these move; the numbers above are as of 2026-10-06.

## Security — act on this before anything else

1. **September 2026 "MikroTrick" vulnerability** (vendor advisory, 2026-09-03).
   *"MikroTik has found a security vulnerability in RouterOS and releases
   containing a fix have been published in all channels… Most configurations are
   not at risk, but upgrading is highly recommended."* Detailed information is
   withheld for now; the issue codename is **"MikroTrick"**, tracked as
   **CVE-2026-67276, CVE-2026-86060 and CVE-2026-67277**, originally reported by
   **CERT.pl**. After upgrading, RouterOS checks the device and marks it
   **"Flagged"** in the log if it was compromised; even if it is not Flagged, the
   advisory says to inspect the configuration for unknown scripts or users.
2. **CVE-2026-84411** — pre-authentication integer underflow in RouterOS
   **web-management** HTTP request handling; **CVSS 9.8**; a single crafted
   request can give root code execution or DoS. Affects **< 7.24**; fixed in
   7.24. CISA published an advisory on **2026-09-30**; no public exploit known at
   that time.
3. **API session expiry** — CISA notes an insufficient session-expiration flaw in
   the RouterOS **API**: after inactivity timeouts or user-group changes, sessions
   could retain their previous (higher) permission set.

Practical read: **run 7.24.x** (or 7.23.7 LTS where you must stay on LTS), and
treat any internet-exposed web or API service as the risk surface.

## v7 versus v6 — what actually changed

From MikroTik's "Upgrading to v7" page (still live at
`help.mikrotik.com/docs/spaces/ROS/…`, migrated to a Confluence space):

- **New kernel** — different performance profile (route cache changes); some
  tasks use more CPU and RAM than under v6.
- **Packages merged** — mostly a single bundle plus a few extra packages;
  the LCD and KVM packages were dropped.
- **New CLI style** — v6 commands are still accepted.
- **Let's Encrypt** certificate generation.
- **REST API** (the bundle's `1.3.7 REST API` and page 234 cover it).
- **UEFI boot on x86**, and CHR FastPath for `vmxnet3` / `virtio-net`.
- **Queues**: `Cake` and `FQ_Codel` added.
- **IPv6 NAT** added; IPv6 policy routing, recursive routing, ECMP and VRF.
- **New NTP client and server** implementation.
- **User Manager redesigned** — configured from WinBox/CLI, no web admin;
  migrate an old database with `/user-manager/database/migrate-legacy-db`.
- **BGP rewritten** — a peer can be processed by up to two cores; per-protocol
  processes (OSPF is separate, fixing cross-protocol stalls); one shared router
  ID; RPKI; script-like filter rules with match/assign on other protocols'
  parameters (e.g. set BGP local preference from an OSPF constant).

## Feature-by-feature status

### Containers
- Sub-menu `/container`, package **`container`**; needs a RouterOS with the
  package installed **plus a disk** (HDD/SSD/USB) to hold images, and container
  mode enabled on the device.
- Compatible with **arm, arm64 and x86**. `remote-image` (docker-pull-like)
  needs **a lot of free main memory** — **16 MB SPI-flash boards should use
  pre-built images on USB/other disk media** instead.
- Bundled docs: `1.21.1 Container` (main) and the container app notes
  (`1.21.1.1`-`1.21.1.8`), page 254-adjacent examples in `1.21 Extended features`.

### ZeroTier
- Added in **v7.1rc2** as a **separate package for ARM/ARM64**. Config lives
  under `/zerotier` (instances, peers, moon/planet), and the bundled
  `1.15.12 ZeroTier` doc matches that menu layout. Useful for LAN access behind
  NAT without port-forwarding (SSH, game servers, Pi-hole).

### WireGuard
- Native in v7 (`/interface/wireguard`), covered by the bundled
  `1.15.11 WireGuard` and the Back To Home examples (pages 904-adjacent).
- Current docs (page last updated 2026-04) add policy-based-routing examples
  (address lists + connection/routing marks per WAN).
- **User-reported niggle (forum, 2026):** peers can end up "broken" after
  disable/enable; toggling the peer's **`responder`** setting recovers them.

### IPv6
- Full stack: DHCPv6 **client with prefix delegation**, DHCPv6 **server**,
  Router Advertisements, IPv6 firewall, **IPv6 NAT**, IPv6 policy routing.
- BGP `address-families=ipv6` and OSPFv3 are the dynamic-routing paths.
- The bundled snapshot covers addressing and neighbour discovery in
  `1.2.1 IP Addressing` / `1.2.2 IPv6 Neighbor Discovery`; the security and
  policy-routing additions above are the newer material.

### OSPFv3
- **The biggest structural change from v6:** OSPFv2 and **OSPFv3 share one
  configuration framework under `/routing/ospf/`** — you create instances for
  v2 or v3 rather than using the separate v6 menus.
- OSPF runs as its own process in v7, which fixed stalls that happened when it
  ran alongside CPU-heavy protocols such as BGP.
- The bundled `1.11.2 OSPF` doc describes the v7 menu layout; third-party
  walkthroughs (StubArea51) show the same `/routing ospf area|interface` shape
  with `network-type=point-to-point` and separate v2/v3 instances.

## Other nuances worth knowing

- **16 MB flash devices are tight.** Boards such as hAP ac2, cAP ac, wAP ac,
  cAP XL ac, Chateau LTE6/LTE7, wAP/LHG 60G and SXTsq/LHG XL 5 ac can run out of
  space with `routeros + wifi-qcom-ac`; a 7.22 changelog line to split
  `wifi-qcom-ac` was struck out and by 7.24 the `wifi-qcom-ac` package was still
  a single ~2.7 MB `.npk`. Budget storage before upgrading these.
- **v7 wants more resources** than v6 (new kernel/features); the forum is blunt
  that some v6 staples (e.g. BFD reliability on some hardware) are still
  catching up.
- **Docs site moved**: legacy `help.mikrotik.com` is frozen → current manual is
  **`manual.mikrotik.com`**, restructured and **versioned**. Third-party and
  forum material is often more current than either.

## What this means for the bundle

Nothing here exists in the 2026-05-26 body — by construction. Use this doc (and
the live manual) for anything version-sensitive: security fixes, container/
ZeroTier/WireGuard behaviour, OSPFv3 menus, IPv6 features, release-specific
fixes. The snapshot remains the better source for legacy concepts and examples
that have not changed.
