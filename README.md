# mikrotik-docs-okf

MikroTik **RouterOS** documentation as an [Open Knowledge Format (OKF)](https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md)
bundle — plain Markdown, indexed for people and agents, following the
[house OKF standard](https://github.com/xcspl/xyno-okf-guide) (house 0.3 on OKF v0.2).

> ## Status — two layers: the current manual, and a dated base
>
> **[`manual/`](manual/index.md) is the current manual** (manual.mikrotik.com) as
> of **2026-10-06** — 1473 docs, one per page, tables intact. Start there.
>
> The **chapter directories are the dated base**: a conversion of MikroTik's
> RouterOS documentation of **2026-05-26** (the frozen legacy `help.mikrotik.com`
> export). Still accurate for most concepts and procedures, but older and with
> some tables flattened by the converter — prefer `manual/` when they disagree.
>
> **[Provenance and known limits](provenance.md)** covers the base and its
> caveats; **[Current state (up to 7.24.5)](current-state.md)** covers versions,
> security and what each release added.
>
> RouterOS documentation © MikroTik; this is a format conversion for reference,
> not an official MikroTik publication.

## What's here

| Path | What |
|---|---|
| [`index.md`](index.md) | Bundle root — self-identification, entry contract, and the full listing. **Start here.** |
| [`manual/`](manual/index.md) | **The current manual** (manual.mikrotik.com) as of 2026-10-06 — 1473 Reference docs, one per page, grouped by the manual's own menu, tables intact. The authoritative layer. |
| [`provenance.md`](provenance.md) | The dated base export and the conversion's caveats. |
| [`current-state.md`](current-state.md) | Versions, security, and the per-release additions 7.20 → 7.24.5. |
| 21 chapter directories | The **dated base** (2026-05-26 legacy export), by the PDF's own chapters, e.g. `12-ipv4-and-ipv6-fundamentals/`. |
| 307 section docs | One `Reference` doc per section of that base. |
| [`recovered-pages.md`](recovered-pages.md) | The 20 base pages the converter refused, with page images and content read from them. |
| `assets/pages/` | The 20 page images (JPEG). |

## Reading it

OKF is designed for progressive disclosure: read a directory's `index.md`,
decide from the entry's `title`/`description`/`tags` whether to open the doc, and
open only that. Do not start by grepping the tree. Every concept doc carries
`type`, `title`, `description`, `timestamp`, `status` and `tags` in its
frontmatter.

The conventions, the `handling` entry contract, and the validator are defined by
the house standard: <https://github.com/xcspl/xyno-okf-guide>.

## How it was built

**Current manual layer (`manual/`, 2026-10-06).** Built from
<https://manual.mikrotik.com/> using its own machine-readable menu
([`llms.txt`](https://manual.mikrotik.com/llms.txt)) and the per-page Markdown
pages it links. The menu supplies the grouping and each page's one-line
description (used as the OKF `description`); the page Markdown supplies the body,
tables intact.

**Dated base (chapter directories, 2026-05-26).**

1. MikroTik's RouterOS documentation PDF (1952 pages) → Markdown with
   [anydoc](https://github.com/firecrawl/anydoc) 0.2.4. The PDF was obtained via
   the legacy [RouterOS page](https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS)
   → MikroTik's Box share [*doc_export*](https://box.mikrotik.com/d/df76f0d495284eb1b6a1/).
2. Split into section docs using the manual's own two-level table of contents
   (chapter → section), one doc per section, frontmatter generated per doc.
3. anydoc's per-page scan check refused 20 pages; those were rendered to JPEG,
   read as images, and added under `recovered-pages.md` with the extracted text.

**Fidelity caveat (base only):** anydoc 0.2.4 flattened some tables — values
survive but column mapping can be lost (for example the `CRS106-1C-5S` hardware
row). The `manual/` layer does not have this problem. Details in
[`provenance.md`](provenance.md).

## Validation

Validated against the house standard's reference validator, **0 errors,
0 warnings**:

```bash
python3 okf-validate.py .        # from the xyno-okf-guide repo
```
