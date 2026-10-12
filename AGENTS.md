# AGENTS.md

Guidance for coding agents working in this repository.

## Overview

`calendar-sync` syncs events from a Google Spreadsheet to Google Calendars. It is a CLI
(`src/main.ts`) and a library (`src/index.ts`). It is an app, not a published package. It stays
active until the CRM jobs replace it.

## Tasks

mise provides the tools. Run `mise trust`, then `mise run install`.

- `mise run ci`: `check`, then `test`
- `mise run check`: typecheck, Prettier check, ESLint
- `mise run format`: fix formatting and lint
- `mise run test`: run the tests with vitest
- `mise run build`: compile into `dist/`

## Auth

Google only. The tool uses Application Default Credentials from
`gcloud auth application-default login`, as your own account. Never commit credentials or use
service account keys.

## Testing

Mock the external SDK boundary (google-spreadsheet, googleapis) and test pure logic.
`test/calendar.test.ts` is the pattern: hand-rolled mock worksheets and no live Google API.

## Code style

TypeScript with ESLint and Prettier from `@cyc-seattle/ts-config`. ESM: import paths carry the
`.js` extension. PR titles are conventional commits. Never push to `main`.

### Comments

Comments explain **why**, not what. Keep them to a line or two. Write one where a reader would
otherwise get it wrong: a non-obvious constraint, a surprising API behavior, or a decision that
looks arbitrary but isn't.

- Don't narrate the code, restate the diff, or argue for the approach you chose.
- Cite an issue (`#107`) instead of recounting its discussion.
- Don't cite a local plan file. A `docs/` reference is fine.
- Test each comment: if you deleted it, would a competent reader still make the same change
  correctly? If yes, delete it.

The same applies to docs:

- **Record the outcome, not the path to it.** Say what to do today, not what failed on the way.
- **No personal identifiers.** Use a role name or `<placeholder>` instead of an email address or a
  numeric account ID.
