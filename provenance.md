---
type: Reference
title: "Provenance and known limits"
description: "What this bundle is, when it was captured, and how far to trust it — a frozen snapshot of the legacy MikroTik wiki exported 2026-05-26 and converted with anydoc, with the table-collapse and image-read caveats. Read this before relying on any fact here."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, provenance, source, limitations]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/115736772/Upgrading+to+v7
  - resource: https://manual.mikrotik.com/docs/introduction/
  - resource: https://mikrotik.com/download/changelogs
---

# Provenance and known limits

## What this is

The MikroTik **RouterOS documentation PDF dated 2026-05-26** (1952 pages),
converted to Markdown with [anydoc](../../../anydoc) 0.2.4 and split into this
bundle. Every content doc carries `timestamp: '2026-05-26'` — **that is the date
of the source, not of the writing** — and the `resource` field points at the PDF.

## The source is frozen — this is not current documentation

The PDF is an export of the **legacy** `help.mikrotik.com` wiki, and its own
first page says so:

> This documentation site has been frozen, no further edits will be made here!
> The new RouterOS documentation site is available here:
> <https://manual.mikrotik.com/docs/introduction/>

So:

- Content here is **accurate as of 2026-05-26** and no later.
- MikroTik now publishes at **`manual.mikrotik.com`** — restructured (Getting
  Started → topic sections → Developer Guides → CLI Reference) and **versioned**
  (a version selector in the top navigation).
- Anything changed or added after 2026-05-26 is **absent**. For current facts,
  see [RouterOS updates and current state](updates-2026-10.md), then the live
  manual and `mikrotik.com/download/changelogs`.

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

- **Currency**: version-specific behaviour, new features, fixed bugs.
- **Exact hardware numbers**: model port layouts and specs (see caveat 1).
- **Per-model switch pages**: the PDF's TOC has only the generic
  `1.5.1 Marvell Prestera switch chip features`, `1.5.2 CRS1xx and 2xx series
  switches` and `1.5.10 … Case Studies` — there is no dedicated CRS106 page, for
  instance; model detail lives in tables.

## Refreshing

Either re-export from `manual.mikrotik.com` (the current, versioned source) and
rebuild the bundle, or keep this snapshot and extend
[updates-2026-10.md](updates-2026-10.md) — which is what was done on 2026-10-06.
