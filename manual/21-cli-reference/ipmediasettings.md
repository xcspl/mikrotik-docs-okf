---
type: Reference
title: "/ip/media/settings"
description: "Settings shared by all DLNA media servers in /ip/media. See DLNA Media Server"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ip/media/settings.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ip/media/settings.md
---

-----------

## ip/media/settings 
**Conditions:** !smips
**Type:** Settings Directory

Settings shared by all DLNA media servers in [`/ip/media`](https://manual.mikrotik.com/docs/cli-reference/ip/media/). See [DLNA Media Server](https://manual.mikrotik.com/docs/storage/dlna).

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="thumbnails" typ="string">Comma separated list of filenames (should end with .jpg). If name of a file in a directory matches any filename in the list, that file is treated as a thumbnail to any media file in that directory: it is no longer listed as a picture, and players show it as the cover picture of the other files. See [DLNA Media Server](https://manual.mikrotik.com/docs/storage/dlna). Default: empty.</ArgTableRow>
</ArgTable>
