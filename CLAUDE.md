# CLAUDE.md

Padeja web (static HTML on GitHub Pages at app.padeja.com). Pages are self-contained; every push to main is live.

## Read first
1. `README.md` - what this is, how to build, folder layout.
2. `DESIGN.md` - the Padeja design guide (colours, type, radii, layouts).

## Workspace layout
`C:\Dev\Padeja` is the Padeja workspace root **and** the website repo. The other projects sit
inside it as separate git repos: `Padejafeed` (iOS), `PadejaFeed-Android`, `PadelScore`,
`PadelScoreAndroid`, `PadejaClubhouseApp` (kiosk, not a repo) and `padeja-design` (master design
guide). They are listed in `.git/info/exclude` so they can never be committed to this
site — **never `git add` them here, and run git commands for them from inside their own folder.**

## Rules
- **Use the design tokens in DESIGN.md.** Do not invent new hex colours, radii or fonts; if a
  new value is genuinely needed, add it to DESIGN.md (and the master copy in `padeja-design`) first.
- All Padeja apps share one Supabase backend. Only the public **anon** key may appear in code.
  Never commit a service-role key, signing keystore, `google-services.json` or `GoogleService-Info.plist`.
- Do not push, open PRs or change the database without asking the maintainer first.
- Keep iOS and Android twins in step: when a feature changes in one, flag the other.
