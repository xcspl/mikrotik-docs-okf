# mikrotik-docs-okf

MikroTik **RouterOS** documentation as an [Open Knowledge Format (OKF)](https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md)
bundle — plain Markdown, indexed for people and agents, following the
[house OKF standard](https://github.com/xcspl/xyno-okf-guide) (house 0.3 on OKF v0.2).

> ## Status — current for RouterOS; base export dated 2026-05-26
>
> The body is a conversion of MikroTik's RouterOS documentation of
> **2026-05-26** (the legacy `help.mikrotik.com` export). RouterOS changes
> **incrementally**, so the great majority of this content — command reference,
> procedures, concepts — **is still current**. Only newer behaviour and newly
> added features have moved on, and those are carried in
> **[Current state (up to 7.24.5)](current-state.md)**.
>
> **[Provenance and known limits](provenance.md)** explains why the base docs are
> dated 2026-05-26 and the conversion's caveats. MikroTik's live, versioned
> manual: **<https://manual.mikrotik.com/>**.
>
> RouterOS documentation © MikroTik; this is a format conversion for reference,
> not an official MikroTik publication.

## What's here

| Path | What |
|---|---|
| [`index.md`](index.md) | Bundle root — self-identification, entry contract, and the full listing. **Start here.** |
| [`provenance.md`](provenance.md) | Base export, dating, and the conversion's caveats. |
| [`current-state.md`](current-state.md) | The now: versions, security, per-release additions (7.20 → 7.24.5), containers and the app store, ZeroTier, WireGuard, IPv6, OSPFv3, BGP, MLAG, ACME. |
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

1. MikroTik's RouterOS documentation PDF (1952 pages) → Markdown with
   [anydoc](https://github.com/firecrawl/anydoc) 0.2.4. The PDF was obtained via
   the legacy [RouterOS page](https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS)
   → MikroTik's Box share [*doc_export*](https://box.mikrotik.com/d/df76f0d495284eb1b6a1/).
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
