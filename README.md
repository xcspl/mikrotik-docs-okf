# mikrotik-docs-okf

MikroTik **RouterOS** documentation as an [Open Knowledge Format (OKF)](https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md)
bundle — plain Markdown, indexed for people and agents, following the
[house OKF standard](https://github.com/xcspl/xyno-okf-guide) (house 0.3 on OKF v0.2).

> ## ⚠️ Snapshot, not current documentation
>
> Everything here is a conversion of MikroTik's RouterOS documentation **PDF
> dated 2026-05-26**, exported from the **now-frozen** legacy
> `help.mikrotik.com` wiki. The content is accurate **as of that date and no
> later**. MikroTik's current, versioned manual is
> **<https://manual.mikrotik.com/>**.
>
> **[Provenance and known limits](provenance.md)** explains what this is and
> where not to trust it. **[RouterOS updates and current state (2026-10)](updates-2026-10.md)**
> records what changed since — security advisories, v7 behaviour, containers,
> ZeroTier, WireGuard, IPv6, OSPFv3.
>
> RouterOS documentation © MikroTik; this is a format conversion for reference,
> not an official MikroTik publication.

## What's here

| Path | What |
|---|---|
| [`index.md`](index.md) | Bundle root — self-identification, entry contract, and the full listing. **Start here.** |
| [`provenance.md`](provenance.md) | What the bundle is, when it was captured, and its limits. |
| [`updates-2026-10.md`](updates-2026-10.md) | Current state as of 2026-10-06, sourced and dated. |
| 21 chapter directories | The manual's own chapters, e.g. `12-ipv4-and-ipv6-fundamentals/`. |
| 307 section docs | One `Reference` doc per manual section. |
| [`recovered-pages.md`](recovered-pages.md) | The 20 pages the converter refused, with page images and content read from them. |
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

1. MikroTik's RouterOS PDF (1952 pages) → Markdown with
   [anydoc](https://github.com/firecrawl/anydoc) 0.2.4.
2. Split into section docs using the manual's own two-level table of contents
   (chapter → section), one doc per section, frontmatter generated per doc.
3. anydoc's per-page scan check refused 20 pages; those were rendered to JPEG,
   read as images, and added under `recovered-pages.md` with the extracted text.

**Fidelity caveat:** anydoc 0.2.4 flattened some tables — values survive but
column mapping can be lost (for example the `CRS106-1C-5S` hardware row). For
exact tables, read the source PDF page. Details in
[`provenance.md`](provenance.md).

## Validation

Validated against the house standard's reference validator, **0 errors,
0 warnings**:

```bash
python3 okf-validate.py .        # from the xyno-okf-guide repo
```
