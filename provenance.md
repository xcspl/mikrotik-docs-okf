---
type: Reference
title: "Provenance and known limits"
description: "The base of this bundle: MikroTik's legacy help.mikrotik.com export of 2026-05-26, converted with anydoc — why the base docs are dated 2026-05-26, how much of it is still current, and the conversion's caveats (table collapse, image-read pages). Read with current-state.md."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, provenance, source, limitations]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
  - resource: https://box.mikrotik.com/d/df76f0d495284eb1b6a1/
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/115736772/Upgrading+to+v7
  - resource: https://manual.mikrotik.com/docs/introduction/
  - resource: https://mikrotik.com/download/changelogs
---

# Provenance and known limits

## What this is

The MikroTik **RouterOS documentation PDF dated 2026-05-26** (1952 pages),
converted to Markdown with [anydoc](https://github.com/firecrawl/anydoc) 0.2.4 and split into this
bundle. Every content doc carries `timestamp: '2026-05-26'` — **that is the date
of the source, not of the writing** — and the `resource` field points at the PDF.

**Where the PDF came from.** The file `ROS-260526-1445-796.pdf` was downloaded
from MikroTik's own distribution link, which the legacy documentation page for
RouterOS points to:

1. <https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS> — the
   RouterOS landing page in the legacy `ROS` space (pageId 328059, last updated
   2026-06-03), itself carrying the *"this documentation site has been frozen"*
   notice;
2. → <https://box.mikrotik.com/d/df76f0d495284eb1b6a1/> — MikroTik's Box share
   titled *doc_export*, holding the exported documentation;
3. → `ROS-260526-1445-796.pdf`.

Every base doc's `sources` field therefore cites the legacy RouterOS page
(328059) as its origin.

## Base export, and what "current" means here

The PDF is an export of the legacy `help.mikrotik.com` wiki, and its own first
page records that the wiki was frozen when MikroTik moved to a new manual. So
this bundle's *base* is the **2026-05-26 export** — that is a capture date, not
a warning that the content is wrong:

- RouterOS changes **incrementally**. Command reference, procedures and concepts
  rarely move, so the **great majority of this content is still current**; only
  newer behaviour and newly added features have moved on.
- The base docs carry `timestamp: '2026-05-26'` — the source's capture date — and
  their `resource` field points at the PDF.
- **[Current state](current-state.md)** is the "now": what is new or different,
  release by release, through **7.24.5** — including BGP, MLAG, the container app
  store, ACME, device-mode, ZeroTier, WireGuard, IPv6 and OSPFv3.
- MikroTik's live manual (restructured and versioned) is
  **<https://manual.mikrotik.com/>** — and it is **ingested in this bundle** as
  the `manual/` layer (as of 2026-10-06, 1473 pages, tables intact). Prefer
  `manual/` over the chapter directories whenever they disagree.

## Fidelity caveats from the conversion

1. **Tables were flattened by anydoc.** Where the PDF had a table, the bundle
   may have a run-together row. Verified example — the CRS106 hardware spec:

   | | |
   |---|---|
   | PDF | `CRS106-1C-5S  QCA-8511  400MHz  -  -  +  9204` (7 columns) |
   | Bundle | `|CRS106-1C-5S|QCA-8511 400MHz - - + 9204|` (2 cells) |

   The values survive but the column mapping does not. The same affects many
   parameter-reference tables (e.g. BGP). **For exact tables, read the PDF page**
   (`pdftotext -layout -f <page> -l <page>`, or the PDF itself).
2. **Twenty pages were read from images.** anydoc's per-page scan check refused
   20 of 1952 pages; those are in [Recovered pages](recovered-pages.md) with
   their rendered images, and their content was read from the images (no OCR
   engine is installed locally). That includes the master table of contents and
   several product/compatibility tables — treat those as read, not parsed.
3. **Some sections have no TOC entry.** 143 heading blocks (level-4
   subsections, chapter title pages) had no matching manual section in the TOC
   and were attached to their parent chapter; their filenames lack the `N-N-N-`
   prefix.

## What it is still good for

- Concepts, CLI procedures, and configuration examples from the legacy manual.
- The routing, firewall, VPN, wireless, scripting, MQTT/IoT and switch chapters.
- A searchable, indexed, offline copy — much better than scrolling a 1952-page
  PDF — **as of its date**.

## What it is not good for

- **Version-specific behaviour**: anything a release changed *after* 2026-05-26 —
  check [Current state](current-state.md) first.
- **Exact hardware numbers**: model port layouts and specs (see caveat 1).
- **Per-model switch pages**: the PDF's TOC has only the generic
  `1.5.1 Marvell Prestera switch chip features`, `1.5.2 CRS1xx and 2xx series
  switches` and `1.5.10 … Case Studies` — there is no dedicated CRS106 page, for
  instance; model detail lives in tables.

## Refreshing

The base body is only regenerated by re-exporting from `manual.mikrotik.com` (the
current, versioned source). For day-to-day currency, extend
[Current state](current-state.md) — which is what was done on 2026-10-06.
