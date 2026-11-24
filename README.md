# Padeja Web (padejapadel.github.io)

The Padeja website and web apps — public pages, scoring/live pages, club consoles and the
TV/clubhouse displays — as plain static HTML served by **GitHub Pages** at
**https://app.padeja.com** (`CNAME`). The old `padejapadel.github.io` address redirects there.

| | |
|---|---|
| Stack | Static HTML/CSS/JS, no build step |
| Hosting | GitHub Pages from `main` (push = deploy) |
| Backend | Supabase project `odrckirnjavfptlfygbo`, called straight from the browser with the public anon key |
| Sibling apps | iOS/Android Feed and Score apps, the Court Tablet, and the Clubhouse kiosk launcher all use the same backend |

## Pages (by filename)

| Group | Pages |
|---|---|
| Public / legal | `index`, `get`, `privacy-policy`, `child-safety-standards`, `delete-account`, `reset-password` |
| Live scoring | `live-scores`, `scorer`, `match`, `broadcast`, `court`, `display` |
| Competitions | `competition`, `tournament`, `join-league`, `entry-paid`, `gkr-autumn-2026` |
| Club tools | `clubconsole`, `clubmanager`, `hostmanager`, `host-console`, `county-console`, `padeja-club-dashboard`, `statements`, `storeadmin`, `booking`, `coaching`, `Benefits`, `Benefitsadmin` |
| TV / clubhouse displays | `bpc-home`, `bpc-court?court=N`, `bpc-wall`, `padeja-display-brentwood`, `beaulieu-display`, `county-display`, `host-display`, `clubhouse-setup` → `clubhouse` |
| Payments | `stripe-return`, `stripe-refresh` |
| Assets | `promo/`, `sponsors/`, `team-logos/`, `padeja-og.jpg`, Padeja logos |

## Working on it

- Edit a page, open it locally in a browser, commit to `main` to publish. There is no
  staging — treat every push as live.
- Every page is self-contained (inline CSS/JS). Copy the `:root` block from
  [`DESIGN.md`](DESIGN.md) instead of inventing new colours.
- Android/iOS apps link to these pages, so don't rename or delete a page without checking
  `AppConstants.webBaseURL` usage in the apps (`https://app.padeja.com`).
- `bpc_games_wall.html` and `trustpadel-display.html` were removed; anything that still
  links to them (e.g. the Android kiosk's default tile list) will 404.

## Design

Follow [`DESIGN.md`](DESIGN.md): section 3.5 for club TV pages (`bpc-*`, displays), 3.6 for
public pages (`index`, `get`, `padeja-home`). Fonts: Hanken Grotesk on public pages; Saira
for headings on club TV pages. Club pages may change the **accent colour only**.

The design source of truth is the `padeja-design` repo (`jbrooker1/padeja-design`, private).
The copy of `DESIGN.md` here is refreshed from it with `node scripts/sync.mjs --write`; edit
colours there, not here.
