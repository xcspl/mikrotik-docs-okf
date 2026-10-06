---
type: Reference
title: "/task"
description: "RouterOS directory reference for /task"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/task.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/task.md
---

-----------

## task 
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="T" typ="terminated">terminated</ArgTableRow>
<ArgTableRow arg="C" typ="current">current</ArgTableRow>
<ArgTableRow arg="A" typ="autosave">autosave</ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="term-pid" typ="num"></ArgTableRow>
<ArgTableRow arg="task-id" typ="num"></ArgTableRow>
<ArgTableRow arg="user" typ="string"></ArgTableRow>
<ArgTableRow arg="name" typ="string"></ArgTableRow>
<ArgTableRow arg="source" typ="string"></ArgTableRow>
<ArgTableRow arg="file-name" typ="string"></ArgTableRow>
<ArgTableRow arg="save-interval" typ="time"></ArgTableRow>
<ArgTableRow arg="append" typ="switch"></ArgTableRow>
</ArgTable>
