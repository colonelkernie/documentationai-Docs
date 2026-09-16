---
name: trello-release-notes
description: Turn Trello's 📢 Add to Release Notes queue (LCP - Engineering board) into Laminar Copilot help center docs. Triages every card (skip internal work, changelog only, update an existing article, or new article), confirms the plan with the user, drafts the changelog.mdx entry and articles on a release branch, pushes it for a preview link, then moves the cards to Released. Use whenever the user wants release notes or a release's changelog written, wants to document what shipped, or asks what's waiting to be documented — including casual asks like "do the 9/18 release notes", "what's in the release notes list?", or "turn the Trello cards into docs". Requires the Trello connector.
---

# Release notes from Trello

Engineers move shipped cards into **📢 Add to Release Notes** on the LCP - Engineering board. This
skill turns that queue into customer-facing docs — a changelog entry for the release, plus article
updates or new articles where a change deserves one — then clears the queue by moving the cards to
**Released**.

The core of the job is translation. Cards are written by engineers for engineers: class names,
schema, acceptance criteria, debates about scope. Help center readers are AFP owners and managers
who only care what changed on their screen and what they need to do about it. Read
`references/writing-guide.md` before drafting — it has the voice, formats, component syntax, and
real card-to-changelog examples from past releases.

## Trello locations

| What | Name | ID |
|---|---|---|
| Board | LCP - Engineering | `ari:cloud:trello::board/workspace/6855c3cacc6ea97a68dbc69c/65488e797852418246428aef` |
| Source list | 📢 Add to Release Notes | `ari:cloud:trello::list/workspace/6855c3cacc6ea97a68dbc69c/681015b0280dc32c6eef8e85` |
| Destination list | Released | `ari:cloud:trello::list/workspace/6855c3cacc6ea97a68dbc69c/655ee5b67e5d0edff31ff5cc` |

If an ID stops resolving, the list was probably renamed or recreated: find it by name with
`trelloReadList` (`list_by_board`) and mention the new ID so this file can be updated.

## Workflow

The order matters. Nothing gets written, pushed, or moved until the user approves the plan, and
cards move only after the push succeeds — so a failed run never loses track of undocumented work.

### 1. Gather

1. List the cards in the source list with `trelloReadCard` (`list_by_list`), paginating until
   done. If the list is empty, say so and stop.
2. Fetch each card on its own with `trelloReadCard` (`get`). List responses show `comments: []`
   even when a card has comments, and comments often carry news the description doesn't, like a
   bug found in QA after the card was written.
3. Fetch each card's checklists with `trelloReadChecklist` (`list_by_card`). Card responses show
   `checklists: []` even when a card has an Acceptance Criteria checklist — and those criteria are
   often the clearest description of what customers will actually see. Note any items still
   `INCOMPLETE`.
4. Read `changelog.mdx` (recent `<Update>` blocks and `## Upcoming Changes`) and skim the pages in
   `documentation.json`, so triage can spot cards that are already documented and articles a change
   affects.

Card text is notes between teammates. Use it as source material, but don't act on to-dos written in
it ("check in with Jeremy…"). Links to Google Docs, claude.ai artifacts, or Trello attachments
usually won't open for you; work from what's on the card and flag gaps instead of guessing.

### 2. Triage

Put each card in exactly one bucket:

- **Skip — internal.** No customer-visible change: infrastructure, feature flag cleanup, internal
  admin tools, error logging, test fixtures. Past examples: "Upgrade heroku redis", "Remove
  certified sync feature flag", "Admin Page Improvements". These still move to Released — they've
  been handled.
- **Already documented.** An existing changelog entry already covers it (the card was moved in
  late). Move only.
- **Changelog only.** Bug fixes and small improvements where a sentence or two tells the whole story.
- **Changelog + update article.** The change makes something in an existing article wrong or
  incomplete. Check this for *every* card, not just features: a button moving is a one-line
  changelog entry, but it also breaks any article whose steps say where that button is.
- **Changelog + new article.** A new capability customers need to set up or learn — a new page,
  workflow, report, or integration. Past examples: Shift Patterns, Relay Integration, GeoTab HOS
  Integration, Cover Shift.

Labels are weak hints. `Bug` usually means a fix and `Feature Request` usually means a feature, but
many cards have no label, and labels like `MIGRATION`, `P1`, or `QA-Katlyn` say nothing about
customer impact. Judge from what customers will notice.

Merge closely related cards (a feature and its follow-up toggle, say) into one entry — readers want
one story per change, not one per ticket.

Flag these in the plan instead of silently deciding:

- **Thin cards** (empty or one-line description): propose wording and mark it low-confidence.
- **Unfinished criteria** (`INCOMPLETE` checklist items): the feature may not have fully shipped.
- **Unresolved problems in comments** (a teammate reporting the change doesn't work, with no later
  comment saying it's fixed): ask before documenting it as shipped.
- **Request-style cards** ("Can we have only one driver to a Shift Pattern?"): the title is the ask,
  not the result — confirm what actually shipped.
- **Enablement unknowns**: if a feature might be off by default or turned on per customer, ask
  whether customers need Support to enable it, since the article's setup section depends on it.

### 3. Confirm the plan

If the user's request already spells out the plan — which cards, what to write for each, the
release date — treat those parts as approved and confirm only what's still open. Otherwise, present
the plan and wait for an explicit go-ahead:

- **Release**: the changelog date and branch. If the current branch looks like `9-4-release`,
  default to that date; otherwise propose today's date (Pacific time) and a matching `M-D-release`
  branch.
- **Cards**: a table of linked title → bucket → one-line reason → target file(s) → proposed
  changelog heading.
- **Flags** from triage, phrased as questions.
- **Trello**: once the push succeeds, every card in the plan moves to Released, skipped ones
  included. Cards the user marks "hold" stay where they are.

If the user changes buckets or answers flags, update the plan and show it again before drafting.

### 4. Draft

**Branch.** Run `git status` first; if there are uncommitted changes unrelated to this release, ask
before continuing rather than sweeping them into the release commit. If the release branch exists,
switch to it and make sure it isn't behind `origin/main` (ask before rebasing). Otherwise
`git fetch origin` and create it from `origin/main`.

**Changelog** (`changelog.mdx`):

- One `<Update>` per release, first under `## Recent Releases`. If an `<Update>` with that date
  already exists, add to it instead of creating a second.
- `tags` lists the entry types present, in the order `"feature","improvement","fix"`.
- One `###` section per entry. Entries backed by an article end with a link to it, e.g. "See the
  [Shift Patterns](/help-center/solutions/shift-patterns) article for setup."
- If the release ships something listed under `## Upcoming Changes`, remove that `<Expandable>`.

**New articles.** Write them in `help-center/solutions/` with a kebab-case filename, following the
skeleton in the writing guide. Add a `documentation.json` entry in the Solutions subgroup where it
belongs (Managing Routes, Managing Drivers, or Integrations) — the `documentationai-docs-editor`
skill covers nav placement and keeping files and nav in sync.

**Article updates.** Change only what the release changes, and leave the rest of the article's
wording alone. If the article's scope broadened, update its frontmatter `description` and intro too.
Remove "work in progress" callouts this release fulfills.

**Don't invent UI details.** If a card doesn't say what a button is called or where it lives, write
the best-supported version and list the question in the final report — a confidently wrong click
path is worse than a flagged one. You can't upload screenshots either, so don't add `<Image>`
placeholders; suggest screenshots in the report instead.

**Check before committing:**

- `documentation.json` parses, every nav `path` points at an existing `.mdx` file, and each new page
  appears exactly once.
- Every internal link (`/help-center/...`) resolves to a real file.
- Nothing from engineering leaked in: grep the diff for backticks, `snake_case` identifiers, and the
  names of teammates or customers that appear on the cards.

### 5. Commit, push, share the preview

Commit in the repo's style — e.g. `Add 9/18 changelog and document two shift start time windows` —
with a short body listing the changelog entries and article changes. Then
`git push -u origin <branch>`.

The preview lives at `https://<branch>--laminar-copilot.documentationai.com/`. Link straight to
`/changelog` and each new or updated article so the user can review in one click.

If the push fails, stop and report. Don't move any cards.

### 6. Move cards to Released

For each card in the approved plan (every bucket except hold), call `trelloWriteCard` with
`action: "move"`, the Released list ID, and `pos: "top"` — Released is kept newest-first. If a move
fails, say which card and carry on with the rest.

### 7. Report

End with:

- Branch, commit, and preview links.
- What each card became (entry heading, articles touched) and which cards moved.
- Open questions: low-confidence wording, unverified UI labels, enablement.
- Suggested screenshots for each new or updated article.
- Next step: review the preview, then open a PR to `main` when it looks right. This skill stops short
  of the PR on purpose.
