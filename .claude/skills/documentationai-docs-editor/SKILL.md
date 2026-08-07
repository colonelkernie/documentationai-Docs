---
name: documentationai-docs-editor
description: Use whenever making changes to the documentationai-Docs repo (Laminar Copilot help center) — adding, editing, renaming, moving, or removing an MDX page, or fixing site navigation. Triggers even on indirect asks like "add a page about X" or "update the audit panel article," since any page-level change here needs its documentation.json nav entry kept in sync. Component syntax and writing style live in this repo's CLAUDE.md (already loaded) — this skill covers the one thing CLAUDE.md doesn't: keeping files and navigation.json from drifting apart.
---

# documentationai-Docs editor

This repo publishes MDX pages, and `documentation.json` is the single source of truth for site
navigation. The two must stay in sync: a page isn't done until it has a nav entry, and a nav
entry isn't done until it points at a real file.

- **New page**: write it wherever the existing group's siblings live (match the folder and
  naming pattern of neighboring pages — don't invent a new location), then add a matching entry
  to `documentation.json` in that group.
- **Edit**: just edit the content; leave the nav entry alone unless the title or location is also
  changing.
- **Rename or move**: update the file and its `documentation.json` entry together, grep the repo
  for anything else linking to the old path, and consider adding an entry to the top-level
  `redirects` array if the old link might be out in the wild.
- **Remove**: delete the file and its nav entry; consider a `redirects` entry pointing at a
  reasonable replacement.

`documentation.json` here is a flat `navigation.pages` tree (not tabs), with groups nesting up to
one level deep (e.g. Solutions → Managing Routes). Hub pages built with `<CollectionList>`/
`<CollectionContent>` reference a group by name only, e.g. `node="groups:Solutions"`.

Before calling any change done, double check: does every page you touched have a nav entry, and
does that entry's `path` point at a file that actually exists? For content style and which
component to reach for, follow CLAUDE.md.
