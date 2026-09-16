# Writing guide: Laminar Copilot help center

Everything here is drawn from the existing pages. When something isn't covered, open the closest
neighboring article and match it — consistency with the site beats any rule below.

**Contents:** 1. Readers and voice · 2. Translating a card · 3. Past cards and what they became ·
4. Changelog format · 5. New article skeleton · 6. Updating an article · 7. Components and links ·
8. Vocabulary

## 1. Readers and voice

Readers are AFP owners and managers who use Copilot to schedule drivers, routes, and assets for
Amazon Relay. They want to know what changed, where to find it, and whether they need to do
anything.

- Address the reader as **you**. The docs never say "operator" or "dispatcher", even though cards
  use those words constantly.
- Lead with what the reader gets, not how it was built: "Weekly shift texts now send even when a
  route has no assigned asset" rather than "Removed the asset check from the texting job."
- Changelog entries are plain and short: "We added…", "We fixed a bug where…", "We improved X so
  that…", "Copilot can now…", "X now…".
- Articles use short paragraphs and numbered click paths. **Bold** UI labels exactly as they appear
  in the app: buttons, tabs, fields, dropdown options.
- Skip hype and exclamation points.

## 2. Translating a card

**Keep**

- What customers can now do, or what behaves differently.
- Where it lives in the app (page, tab, drawer, button), when the card actually says.
- Rules and limits they'll run into ("only SO2 contracts support this").
- Whether Support has to turn it on.

**Drop**

- Code, schema, API, and file names (`Driver#prefers_start_time?`, `routes.actual_start_time`,
  `/api/relay_integration/drivers`), plus PR, Rollbar, PostHog, and migration details.
- Internal version names. Say "Dynamic Scheduler", never "DS", "DS v2", or "the v2 algorithm".
- People: teammates ("Moses's call", "check in with Jeremy") and customers or their drivers named in
  examples.
- Acceptance-criteria phrasing, metrics, success criteria, risks, open questions, out-of-scope lists.
- Future plans and upgrade paths. Don't promise what hasn't shipped.
- Internal links: Google Docs, claude.ai artifacts, Trello attachment images.

Acceptance Criteria checklists are the best raw material for articles. Items starting with "UI:"
usually describe exactly what customers see; schema, API, and regression items usually don't.

## 3. Past cards and what they became

| Card | What it became |
|---|---|
| "Send 24 hour and weekly shift texts for routes even if they don't have an assigned asset" | Improvement, **Texting improvements for unassigned assets**: "24-hour shift confirmation and weekly shift texts now send to drivers on routes even when the route doesn't have an assigned asset." |
| "Audit Panel Bug - relay rejected routes" | Fix, **Audit Panel fix**: "We fixed a bug where the Audit Panel incorrectly flagged drivers for not accepting routes that were Relay Rejected." |
| "Relay integration improvements" (generic connection error, per-route failure messages, a logging fix) | Improvement, **Relay Integration sync errors**: the two visible changes became one sentence, and the logging fix was dropped as internal. |
| "Updating SCV to sync Drivers" (extension reads Relay's drivers response and posts it to a new endpoint) | Improvement, **SCV Extension syncs driver status**, ending with "See the [SCV Chrome Extension](/help-center/solutions/scv-chrome-extension) article for setup." That article was updated too. |
| "Contract Breakdown Table" | Feature, **Contract Breakdown Table**: "We added a new Breakdown view where you can see your SO1 and SO2 routes broken down by contract." |
| "Fix unresolvable invalid driver audit notification" (no description) | Fix, **Audit Panel fix**: "…incorrectly flagged an error for drivers that had been deleted from Copilot." The deleted-drivers detail isn't on the card; the writer knew it. That's why thin cards get flagged for the user instead of guessed at. |
| "Upgrade heroku redis", "Remove certified sync feature flag", "Admin Page Improvements", "Update Fake Relay Trips Endpoint…", "Relay integration tractor rollbar error" | Skipped. Nothing customers see. |

Headings name the feature area readers recognize (Audit Panel, Relay Integration), not the ticket
title.

## 4. Changelog format

A real entry, for reference:

```mdx
<Update label="2026-08-18" tags={["feature","improvement","fix"]}>
  ### Shift Patterns

  SO2 contracts can now be configured with a 2-on-2-off shift pattern, in addition to the existing 4-on-4-off pattern. Dynamic Scheduler assigns the contract's two drivers automatically according to the selected rotation. See the [Shift Patterns](/help-center/solutions/shift-patterns) article for setup.

  ### Relay Integration sync errors

  We improved Relay Integration so that when a sync fails, you'll now see detailed error messaging explaining why.

  ### GeoTab integration fix

  We fixed the GeoTab integration so it properly pulls in certified route times.
</Update>
```

- `label` is the release date as `YYYY-MM-DD`. The newest `<Update>` goes first under
  `## Recent Releases`.
- `tags` holds only the types present, always ordered `"feature","improvement","fix"`.
- Indent everything inside `<Update>` two spaces, with a blank line after each heading and between
  entries. Keep each paragraph on one line.
- Order entries features first, then improvements, then fixes.
- Headings are short plain phrases, not bold (some older entries bold them; don't copy that). Fixes
  are usually "<Area> fix".
- One to three sentences per entry. If an article covers the entry, end with "See the [Title](/path)
  article for setup." or "…for details." when there's nothing to set up.

## 5. New article skeleton

```mdx
---
title: <Feature Name as it appears in the app>
description: >-
  <One or two sentences, about 20–30 words: what it does and what it saves the
  reader. Wrap near 80 characters.>
---
<Intro, two or three sentences: what the feature is and what it does for you. Bold its key options
or terms the first time they appear.>

## Setting up <Feature Name>

<Callout kind="info" collapsed="false">
  [Submit a support ticket](/submit-a-support-ticket) to get <Feature Name> enabled for your workspace.
</Callout>

## <Task-named section, e.g. "Syncing assignments to Relay">

1. From the Copilot dashboard, go to **Command Center** in the side navigation.
2. Click **<Button>**.
3. <…>

<Callout kind="alert" collapsed="false">
  <A limit or gotcha readers will hit.>
</Callout>

## <How it works: rules and behavior people would otherwise ask Support about>

## Need Help?

If you're unsure how to <task>, contact the **Laminar Copilot Support Team** for assistance.
```

- Include **Setting up** only when Support has to enable or connect something. Leave out any section
  that would be empty rather than padding it.
- The filename is the kebab-case title in `help-center/solutions/` (`shift-patterns.mdx`), and the
  nav entry's `title` matches the page title.
- Every new page needs both `title` and `description`.
- Most articles run 30–60 lines.
- Good models to open: `shift-patterns.mdx` (a setting on a contract), `relay-integration.mdx` (an
  integration with setup), `cover-shift.mdx` (a multi-step flow).

## 6. Updating an article

The 8/31 release is a good model: the SCV Chrome Extension article went from assets only to assets
and drivers.

- Widen the frontmatter `description`, heading, and intro when a feature's scope grows.
- When a step now depends on what you're doing, split it into sub-bullets instead of rewriting it.
- Add a subsection that mirrors the existing one (`### Assets`, then `### Drivers`), and leave the
  existing wording alone.
- When a release moves or renames something in the UI, grep every `.mdx` file for the old label or
  location. The article named after the feature isn't always the only one describing it.
- Remove "work in progress" callouts the release fulfills.

## 7. Components and links

- **Callout**: `kind="info"` for enablement and neutral notes, `kind="alert"` for limits and
  gotchas, `kind="tip"` for helpful habits. Include `collapsed="false"` and indent the content two
  spaces.
- **Steps**: for flows that span several screens, `<Steps>` wrapping
  `<Step title="Select drivers" icon="users" title-type="h3">`. Icons are Lucide names (`pencil`,
  `users`, `message-square`, `list-checks`). Use a plain numbered list for short click paths.
- **Image**: only blob-cdn.documentation.ai URLs, which come from uploading through the
  documentation.ai editor. Trello attachment, Gmail, and other external image URLs break for
  visitors. You can't upload, so don't add `<Image>` tags; suggest screenshots in the report instead.
- **Expandable**: only for `## Upcoming Changes` in the changelog.
- **Internal links**: root-relative with no extension, like `/help-center/solutions/shift-patterns`
  and `/submit-a-support-ticket`.
- **App links** the docs already use: `https://app.laminarcopilot.com/contracts`, `/drivers`,
  `/tractors` (the Assets page), and `/maintenance_blocks`. Don't guess other app URLs; describe the
  navigation instead ("go to **Command Center** in the side navigation").

## 8. Vocabulary

| Write | Not |
|---|---|
| Copilot, Laminar Copilot | LCP |
| Dynamic Scheduler | DS, DS v2, the v2 algorithm |
| GeoTab | Geotab |
| Amazon Relay, Relay | |
| you, AFP owners and managers | operator, dispatcher |
| Solo 1 (SO1) and Solo 2 (SO2) on first mention, then SO1 and SO2 | solo1, solo2 |
| Edit Drawer (for a route) | "edit assigned route", "shift edit drawer" |
| Command Center, Driver Roster, Audit Panel, Contracts tab, Breakdown tables, Time Off Tracker, Maintenance Tracker | |
| Laminar Copilot Support Team, support ticket | |
