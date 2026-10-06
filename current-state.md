---
type: Reference
title: "Current state (RouterOS up to 7.24.5)"
description: "The current picture: this bundle's base export is 2026-05-26, most RouterOS behaviour is unchanged, and everything added since is recorded here — 7.20 to 7.24.5, the September 2026 security advisories, and the present state of BGP, MLAG, containers and the app ecosystem, ACME, device-mode, ZeroTier, WireGuard, IPv6 and OSPFv3."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, current, updates, v7, security, bgp, mlag, container, zerotier, wireguard, ipv6, ospfv3, acme]
resource: https://manual.mikrotik.com/docs/introduction/
sources:
  - resource: https://forum.mikrotik.com/t/7-24-stable-is-released/272381
    last_modified: 2026-08-14
  - resource: https://forum.mikrotik.com/t/7-24-5-stable-is-released/273494
    last_modified: 2026-09-29
  - resource: https://forum.mikrotik.com/t/v7-23-stable-is-released/270721
    last_modified: 2026-05-25
  - resource: https://forum.mikrotik.com/t/v7-22-stable-is-released/269092
    last_modified: 2026-03-09
  - resource: https://forum.mikrotik.com/t/v7-21-stable-is-released/267773
    last_modified: 2026-01-12
  - resource: https://forum.mikrotik.com/t/v7-20-stable-is-released/265196
    last_modified: 2025-09-29
  - resource: https://mikrotik.com/supportsec/september-2026-vulnerability
    last_modified: 2026-09-03
  - resource: https://aviatrix.ai/threat-research-center/cisa-warns-critical-pre-auth-rce-flaw-mikrotik-routeros-cve-2026-84411
    last_modified: 2026-09-30
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Current state (RouterOS up to 7.24.5)

**How to read this bundle.** The body is a conversion of MikroTik's RouterOS
documentation PDF of **2026-05-26** (see [Provenance](provenance.md)). RouterOS
changes incrementally, so the great majority of that content — command
reference, configuration procedures, concepts — **is still current**; it is the
newer behaviour and additions that need this page. This doc is the *now*: the
version picture, the security position, the feature areas that have moved since,
and what is new in each release. It is accurate as of **2026-10-06**.

## Versions

| Release | Date | Note |
|---|---|---|
| 7.20 stable | 2025-09-29 | BGP instances, initial EVPN, Aquantia driver |
| 7.21 stable | 2026-01-12 | **the base of this bundle's PDF is between 7.21 and 7.22** |
| 7.22 stable | 2026-03-09 | custom apps, BGP unnumbered/add-path/multipath, MLAG per bridge |
| 7.23 stable | 2026-05-25 | app-store expansion, HTTPS upgrades, app `network-outgoing-access` |
| **7.24 stable** | 2026-08-14 | current **stable** line |
| **7.24.5** | 2026-09-29 | latest point release |
| **7.23.7** | 2026-09-16 | current **long-term** release |

There is no 7.30 — the latest stable is **7.24.x**. Always confirm with
`/system/package/update/check-for-updates` or
<mikrotik.com/download/changelogs>; point releases appear every few weeks.

## Security — do this first

1. **September 2026 "MikroTrick" (vendor advisory, 2026-09-03).** MikroTik found
   a vulnerability in RouterOS and **published fixes in all channels**;
   *"Most configurations are not at risk, but upgrading is highly recommended."*
   Details are withheld for now; the codename is **"MikroTrick"**, tracked as
   **CVE-2026-67276, CVE-2026-86060, CVE-2026-67277**, originally reported by
   **CERT.pl**. RouterOS now **checks the device and marks it "Flagged"** in the
   log if compromised — and even when it is not Flagged, the advisory says to
   inspect the configuration for unknown scripts or users.
2. **CVE-2026-84411** — pre-authentication integer underflow in RouterOS
   **web-management** HTTP handling; **CVSS 9.8**; one crafted request can yield
   root code execution or DoS. Affects **< 7.24**, fixed in 7.24; CISA advisory
   **2026-09-30**; no public exploit known at that time.
3. **API session expiry** — sessions could retain their previous (higher)
   permissions after inactivity timeouts or user-group changes.

**Position: run 7.24.x**, or 7.23.7 where you are pinned to long-term. Treat
internet-exposed web and API services as the risk surface.

## New in each release (headline additions)

### 7.20 — 2025-09-29
- **BGP instance configuration** (`/routing/bgp/instance`); NLRI filters;
  initial **EVPN** support; IPv4 NLRI over an IPv6 next hop.
- **Aquantia** NIC driver (arm64/x86/CHR); BTH file sharing, including from the
  WinBox Files menu; verbose STP debug logging.

### 7.21 — 2026-01-12
- **BGP RFC 9234** route-leak prevention/detection via roles; RFC 6286
  duplicate router-ids for eBGP.
- **arm64 receive packet steering** (`/system/resource/irq/rps`) to even out CPU
  load; LACP `lacp-system-id` / `-priority`; DHCP snooping Option 82
  improvements.
- **Certificate trust-store** parameter; Back-To-Home file-share improvements.

### 7.22 — 2026-03-09
- **Custom apps and app health checks** — the container **app store** becomes a
  real feature (configurable app-store URL, health checks that rewrite the
  composed YAML, swap enabled on app devices).
- **BGP: unnumbered support, `add-path`, and `multipath`** (best path may select
  ECMP routes).
- **MLAG moved per bridge interface** (`/interface/bridge/mlag` → per bridge,
  config auto-updated) with local/static MAC synchronisation and MLAG host-table
  flags; **RA guard** added.
- **Multiple ACME certificates**; **device-mode configurable via Netinstall /
  FlashFig "mode script"**.

### 7.23 — 2026-05-25
- **HTTPS by default** when contacting MikroTik upgrade servers.
- **App ecosystem expansion** — many new apps (Nextcloud-family, Paperless-ngx,
  Zulip, Odoo, LoRaWAN Stack, Portainer/Komodo/Dockge variants, …), apps on
  **XFS**, app restart command, CLI parameters, swap on the app's own file,
  automatic hardware-device passing.
- **`network-outgoing-access=yes/no`** to stop a container making outbound
  connections.

### 7.24 — 2026-08-14
- **Bridge/MLAG hardening**: `querier-uses-bridge-address` for the IGMP querier,
  MLAG MAC aging/flush fixes, stuck-MLAG-on-mismatched-L2MTU fix, STP priority
  validation, DHCPv4-snooping **IP binding table**.
- **BGP**: EVPN label-corruption and type-5 fixes; malformed-packet stability.
- **Certificate `acme-renew`**; **btest/speed-test VRF support**; adlist
  stability.
- **Apps**: opencloud, hermes-agent, inventree, `HF_TOKEN`; VETH IP reserved
  while stopped (stable addresses across restarts); secrets made sensitive so
  they do not leak in `export`.

### 7.24.5 — 2026-09-29
Stability release: **disabled the DHCP snooping IP binding table added in
7.24**, OSPF interface-template fix, PoE-out fix on CRS328-24P-4S+, LTE MBIM
stability, **updated Wi-Fi regulatory information**.

## Where the feature areas stand

- **Containers / apps.** Beyond the bundled `1.21.1 Container` doc: the **app
  store** (`/app`) with custom apps, health checks, per-app YAML, outgoing-access
  control, and hardware passing is the significant addition of 7.22-7.24. Still
  needs a disk; **16 MB-flash boards must use pre-built images on external
  media** (remote-image needs substantial free RAM).
- **BGP.** The 7.20-7.24 work is the current picture: instance-based
  configuration, EVPN, unnumbered, add-path, multipath/ECMP, RPKI, and RFC 9234
  roles. If your BGP config predates 7.20, expect instance reconfiguration.
- **MLAG / bridge.** Per-bridge MLAG (7.22) plus the 7.24 fixes; RA guard.
- **ZeroTier.** Separate package for ARM/ARM64 since v7.1rc2; `/zerotier`
  instances and peers, as in the bundled `1.15.12 ZeroTier`.
- **WireGuard.** Native `/interface/wireguard` (bundled `1.15.11`); current docs
  add policy-based-routing examples. Forum-reported niggle: peers can break
  after disable/enable — toggling `responder` recovers them.
- **IPv6.** DHCPv6 client with prefix delegation, DHCPv6 server, RA, IPv6
  firewall, IPv6 NAT, IPv6 policy routing; BGP `address-families=ipv6` and
  OSPFv3 are the dynamic-routing paths.
- **OSPFv3.** Shares one framework with OSPFv2 under `/routing/ospf/` (instances
  per version) — the big change from v6; OSPF runs as its own process.
- **Certificates.** ACME (Let's Encrypt) with **multiple certificates** and
  `acme-renew`; built-in trust store configurable.
- **Upgrades.** HTTPS to MikroTik servers by default as of 7.23.

## Known wrinkles

- **16 MB flash** devices (hAP ac2, cAP ac, wAP ac, cAP XL ac, Chateau, 60 GHz
  units, SXTsq/LHG XL 5 ac) run tight with `routeros + wifi-qcom-ac`; the 7.22
  plan to split that package was struck through and had not happened by 7.24.
- **v7 uses more CPU/RAM** than v6 (new kernel/features); some v6 staples (BFD
  reliability on certain hardware, for example) are still catching up.
- **Downgrading across the BGP instance change** (pre-7.20 ↔ 7.20+) can cause
  configuration issues — note the 7.20 changelog warning.
- **Docs site moved**: legacy `help.mikrotik.com` is frozen → current manual is
  **`manual.mikrotik.com`** (restructured, versioned). Forum announcements (used
  above) are MikroTik's own release notes.

## Sources

Release announcements above are MikroTik's official forum posts (linked with
dates in the frontmatter). Security detail is from MikroTik's support-security
page and the CISA/third-party coverage of CVE-2026-84411, both cited. The
feature descriptions for containers, ZeroTier, WireGuard, IPv6 and OSPFv3 come
from MikroTik's documentation pages (last updated April 2026) and the "Upgrading
to v7" page.
