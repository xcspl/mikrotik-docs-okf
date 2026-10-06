---
okf_version: "0.2"
house_version: "0.3"
bundle: mikrotik-docs-okf
handling:
  - Read this index before opening any doc in this bundle.
  - Navigate by index entries; never glob the tree.
  - A write to any directory updates that directory's index.md in the same commit.
  - Full rules live in okf-guide.md in the workspace registry (Playbook at its bundle root).
---

# MikroTik RouterOS documentation

The MikroTik RouterOS manual as an OKF bundle.

**Base: MikroTik's RouterOS documentation of 2026-05-26** — the frozen legacy
`help.mikrotik.com` export — which remains current for the great majority of
RouterOS (command reference, procedures, concepts). Base docs are stamped
`timestamp: '2026-05-26'`, the source's capture date. Everything added or changed
since is carried in [Current state](current-state.md) through **7.24.5**; the
live, versioned manual is <https://manual.mikrotik.com/>. Conversion caveats are
in [Provenance and known limits](provenance.md).

# About

* [Provenance and known limits](provenance.md) - What the base export is, why its docs are dated 2026-05-26, and the anydoc table-collapse / image-read caveats.
* [Current state (RouterOS up to 7.24.5)](current-state.md) - The now: versions, the September 2026 security advisories, what each release added (BGP, MLAG, the app store, ACME, device-mode), and the state of containers, ZeroTier, WireGuard, IPv6 and OSPFv3.

# Chapters

* [1.1 Getting started](11-getting-started/index.md) - 25 sections.
* [1.2 IPv4 and IPv6 Fundamentals](12-ipv4-and-ipv6-fundamentals/index.md) - 6 sections.
* [1.3 Management tools](13-management-tools/index.md) - 15 sections.
* [1.4 Authentication, Authorization, Accounting](14-authentication-authorization-accounting/index.md) - 8 sections.
* [1.5 Bridging and Switching](15-bridging-and-switching/index.md) - 24 sections.
* [1.6 Firewall and Quality of Service](16-firewall-and-quality-of-service/index.md) - 26 sections.
* [1.7 High Availability Solutions](17-high-availability-solutions/index.md) - 8 sections.
* [1.8 Mobile Networking](18-mobile-networking/index.md) - 5 sections.
* [1.9 Multi Protocol Label Switching - MPLS](19-multi-protocol-label-switching-mpls/index.md) - 9 sections.
* [1.10 Network Management](110-network-management/index.md) - 15 sections.
* [1.11 Unicast Routing Protocols](111-unicast-routing-protocols/index.md) - 14 sections.
* [1.12 Multicast Routing Protocols](112-multicast-routing-protocols/index.md) - 4 sections.
* [1.13 Scripting](113-scripting/index.md) - 13 sections.
* [1.14 System Information and Utilities](114-system-information-and-utilities/index.md) - 16 sections.
* [1.15 Virtual Private Networks](115-virtual-private-networks/index.md) - 17 sections.
* [1.16 Wired Connections](116-wired-connections/index.md) - 4 sections.
* [1.17 Wireless](117-wireless/index.md) - 25 sections.
* [1.18 Internet of Things](118-internet-of-things/index.md) - 15 sections.
* [1.19 Hardware](119-hardware/index.md) - 16 sections.
* [1.20 Diagnostics, monitoring and troubleshooting](120-diagnostics-monitoring-and-troubleshooting/index.md) - 26 sections.
* [1.21 Extended features](121-extended-features/index.md) - 15 sections.

# Appendix

* [Recovered pages (OCR-flagged)](recovered-pages.md) - The 20 pages anydoc refused, with page images and content read from them.
