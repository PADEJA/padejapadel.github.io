# Padeja Design Guide

The single reference for how anything Padeja looks and feels — iOS, Android, web, club
TV displays, court tablets and watches. **Anything new should start here** so every
surface feels like the same product.

> Source of truth for the values below: `Color+Padeja.swift` (iOS Feed) and
> `PadejaTheme.kt` (Android Feed), which already match each other, plus usage counts
> measured across the iOS apps and the web pages. Where apps disagree, the "Known
> drift" section at the bottom says which value wins.

---

## 1. The feel in one paragraph

**Dark, sporty, scoreboard-confident.** Deep navy canvas, slightly lighter navy cards
with a thin blue-grey outline, one bright cyan brand colour for actions and highlights,
and a small set of semantic colours (green win, red loss, amber draw/warning, red LIVE).
Rounded corners (10–14), bold/semibold type, short uppercase captions. Content is
glanceable: big numbers, little chrome. Court-booking is the one deliberate exception:
a light, friendly theme (section 3.4).

---

## 2. Core colour tokens (use these first)

| Token | Hex | Use |
|---|---|---|
| `background` | `#0A1624` | App/page canvas |
| `card` | `#162035` | Cards, sheets, list rows (fill) |
| `border` | `#1E3050` | Card outline, dividers, inputs, chips (most-used colour in iOS Feed) |
| `surfaceDeep` | `#0D1B2E` | Inset fields, wells inside a card, deepest layer |
| `brand` | `#3BC8F5` | Primary actions, links, selected tab, key highlights. Text on it is **black** |
| `secondary` | `#8AA4C0` | Secondary text, icons |
| `tertiary` | `#5A7A99` | Captions, placeholders, disabled text |
| `text` | `#FFFFFF` | Primary text on dark |
| `win` | `#3DE39E` | Wins, positive deltas, "live/OK" greens |
| `loss` | `#F56040` | Losses, negative deltas |
| `draw` | `#F5B83D` | Draws, caution, gold highlights |
| `orange` | `#F09537` | Warnings, streaks, secondary accent |
| `green` | `#35D6A4` | Confirmations, availability |
| `teal` | `#00D4AA` | Club-account badge, scoring-app primary (section 3.2) |
| `danger` | `#E24B4A` | Destructive buttons, error banners |
| `success` | `#1D9E75` | Success messages, court-green chips |

Rows `border`, `surfaceDeep`, `tertiary`, `danger`, `success` are used hundreds of times as
raw hex today but have **no named token** in the code yet — add them (section 8).

Overlays on dark: white at 6% for card fill (`#0FFFFFFF`) and 10% for outline
(`#1AFFFFFF`) — used by the Android scoring app, good for glass-style cards.

---

## 3. Theme variants

### 3.1 Feed / community (default)
The table in section 2. Used by `Padejafeed` (iOS) and `PadejaFeed-Android`.

### 3.2 Scoring apps (`PadelScore`, `PadelScoreAndroid`, Watch/Wear)
Same navy world, but **teal leads** because the scoreboard is the product:

| Token | Hex |
|---|---|
| primary | `#00D4AA` (text on it black) |
| secondary | `#00A8FF` |
| error / team B | `#FF6B6B` |
| gold (winner/trophy) | `#FFD700` |
| canvas | `#0D1B2A` |
| deep / mid navy | `#0A2236` / `#1B3A4B` |

### 3.3 Court tablet & outdoor displays (`PadejaCourtTablet`)
Built for **sunlight**: pure black canvas, pure white text, bigger and bolder than
everything else, screen forced to max brightness.

| Token | Hex |
|---|---|
| bg | `#000000` |
| text / muted | `#FFFFFF` / `#C7D0DA` |
| brand | `#3BC8F5` |
| team green / red | `#16A34A` / `#DC2626` |
| LIVE | `#F23B2E` |
| serve ball | `#D7E04A` |
| winners / errors | `#3BC8F5` / `#FF9F40` |
| stat-bar track | `#20262E` |
| Who-hit winner / error | `#1B7A3B` / `#C0202A` |

### 3.4 Court booking (light section)
A lighter, friendlier area inside the dark app — the `cb*` palette:

| Token | Hex | | Token | Hex |
|---|---|---|---|---|
| `cbBg` | `#EEF2F6` | | `cbGreen` | `#0E9E50` |
| `cbCard` | `#FFFFFF` | | `cbGreenDeep` | `#0C7F40` |
| `cbInk` | `#16202E` | | `cbBrand` | `#1690C2` |
| `cbMuted` | `#5E6B7B` | | `cbBrandDeep` | `#0F6E97` |
| `cbLine` | `#E2E7EE` | | `cbReserved` | `#C87A0E` |
| `cbBooked` | `#ECEFF3` | | `cbBookedInk` | `#6B7788` |
| `cbLoss` | `#E4573D` | | | |

### 3.5 Club TV displays & the clubhouse kiosk (web + Android)
16:9 wall/TV screens. Slightly different navy and a **per-club accent**:

| Token | Hex |
|---|---|
| bg / bg2 | `#0A111E` / `#0B1424` |
| panel / panel2 / panel3 | `#101C30` / `#152540` / `#0E1829` |
| line | `rgba(140,170,210,.12)` |
| ink / muted / faint | `#EDF3FC` / `#93A7C2` / `#5B7089` |
| **club accent** | Brentwood `#34D6C6` (hover `#22B9AE`, dim `rgba(52,214,198,.14)`) |
| tile accents | cyan `#3BC8F5`, gold `#F2C14E`, violet `#A98BEE`, live-green `#3DE39E` |

**Rule:** the accent is the *only* thing a club changes. Keep the rest identical, and
store the accent in the club's config row rather than in code.

### 3.6 Public web (`index`, `get`, `padeja-home`)
The public pages use the **scoring variant** (3.2): navy `#0D1B2A`, panels `#12243A` /
`#0F1E30`, teal `#00D4AA`, sky `#00A8FF`, coral `#FF6B6B`, gold `#FFD54A`, text `#EAF2FF`,
dim text `#8EA6C4`, hairline `rgba(255,255,255,.08)`. Font: Hanken Grotesk. Cards use
radius 16. (`clubconsole.html` is the page that already follows the core palette in
section 2.)

---

## 4. Typography

| Surface | Display / headings | Body / UI |
|---|---|---|
| iOS | SF (system), `.bold` | SF (system), `.semibold` |
| Android | Roboto/system via Material | system |
| Public web pages | **Hanken Grotesk** 500–900 | **Hanken Grotesk** |
| Club TV displays | **Saira** 500–800 | **Hanken Grotesk** 400–800 |

Observed iOS sizes: 13–16 semibold for rows and buttons; 9–11 **bold** for captions and
badges (often uppercase with letter-spacing); 14–16 bold for card titles. Big numbers
(scores, standings) are the largest thing on any screen. Section labels on TVs:
bold, uppercase, `letter-spacing: .2em`, colour `faint`.

---

## 5. Shape, depth and spacing

| Element | Corner radius |
|---|---|
| Card / list row | **12** (most common), **14** for large/hero cards |
| Input, button, chip | **10** |
| Small badge / tag | 6–8 |
| Sheet / modal | 16 |
| Pill, avatar | fully round (999 / 50%) |
| Web TV tile | 16–26 (scales with screen) |

* **Cards** = `card` fill + 1px `border`. No heavy shadows; depth comes from lighter
  surfaces on a darker canvas.
* **Backgrounds** on web may carry two soft radial glows (brand cyan top-left, blue
  top-right at 8–10% opacity) over the base colour.
* **TV/kiosk layouts** size everything with container units (`cqh` / `cqw`) so one page
  fits any screen without scrolling.

---

## 6. Layout patterns

**Phone apps (Feed)** — bottom tab bar, four tabs in this order: **Home**, **Community**,
**Calendar**, **Help**. Profile is reached from the header, not a tab. Selected tab uses
`brand`; badges (e.g. follow requests) sit on the Community icon. Detail screens push on
a navigation stack; actions (join, register, stats) open as bottom sheets.

**Play hub** — competitions, leagues, leaderboard and court booking live under Play;
court booking switches to the light `cb*` theme.

**Scoring apps** — linear flow: **Setup → Scoreboard → Result → Submit/Verify**.
Scoreboard is full-bleed, big tappable team halves (team colours), serve indicator in
`#D7E04A`. Watch/Wear shows only score + serve.

**Court tablet** — first run: court-code setup screen (stored on device, one build for
every court); then a black, huge-type live display with serve ball, countdown to the
slot end, and stats bars. Display only.

**Club TV hub (`bpc-home` pattern)** — top bar (greeting left, "Powered by Padeja" logo
right), then labelled sections of **tiles**: each tile has an icon, title, one-line
description, and its own accent colour as left/top highlight. Courts are a numbered row
of smaller green "Live" tiles.

**Android kiosk (`PadejaClubhouseApp`)** — same hub as above as a native grid: header
(`PADEJA` wordmark in brand, club name large), 3-column tile grid, gear in the corner
behind a PIN. Selected/focused tile gets a brand stroke (needed for TV remotes).

---

## 7. Components cheat-sheet

| Component | Spec |
|---|---|
| Primary button | `brand` fill, **black** text, radius 10, semibold 15 |
| Secondary button | transparent, 1px `border`, `secondary`/white text |
| Destructive | `danger` fill, white text |
| Card | `card` + 1px `border`, radius 12–14 |
| Input | `surfaceDeep` fill, 1px `border`, radius 10, placeholder `tertiary` |
| Chip / tag | `border` fill, `secondary` text, bold 10–11 |
| Club badge | `teal` fill, `#0A1624` text |
| LIVE pill | red (`#F23B2E` tablet / `#FF3B4E` web), white bold uppercase, pulsing dot |
| Win / loss / draw | `win` / `loss` / `draw` for deltas, form dots and result text |
| Empty state | centred icon + `secondary` text + one brand button |

---

## 8. Using this in code

**SwiftUI** — extend `Color+Padeja.swift` (already has background, card, brand,
secondary, win, loss, draw, orange, green). Add:

```swift
static let padejaBorder      = Color(hex: "#1E3050")
static let padejaSurfaceDeep = Color(hex: "#0D1B2E")
static let padejaTertiary    = Color(hex: "#5A7A99")
static let padejaDanger      = Color(hex: "#E24B4A")
static let padejaSuccess     = Color(hex: "#1D9E75")
```

**Jetpack Compose** — extend `PadejaTheme.kt`:

```kotlin
val PadejaBorder      = Color(0xFF1E3050)
val PadejaSurfaceDeep = Color(0xFF0D1B2E)
val PadejaTertiary    = Color(0xFF5A7A99)
val PadejaDanger      = Color(0xFFE24B4A)
val PadejaSuccess     = Color(0xFF1D9E75)
```

**Web** — paste into `:root` and reference only variables:

```css
:root{
  --bg:#0A1624; --card:#162035; --border:#1E3050; --deep:#0D1B2E;
  --brand:#3BC8F5; --secondary:#8AA4C0; --tertiary:#5A7A99; --text:#FFFFFF;
  --win:#3DE39E; --loss:#F56040; --draw:#F5B83D; --orange:#F09537;
  --green:#35D6A4; --teal:#00D4AA; --danger:#E24B4A; --success:#1D9E75;
  --radius:12px; --radius-lg:14px; --radius-sm:10px;
  --display:"Saira","Hanken Grotesk",system-ui,sans-serif;   /* club TV headings; elsewhere use Hanken Grotesk */
  --body:"Hanken Grotesk",system-ui,sans-serif;
}
```

**Android XML (non-Compose, e.g. the kiosk)** — `res/values/colors.xml`:
`bg #0A1624`, `surface #162035`, `border #1E3050`, `brand #3BC8F5`,
`muted #8AA4C0`, `faint #5A7A99`, `win #3DE39E`, `gold #F5B83D`.

**Generated files.** `tokens.json` is the single place colours are edited. `node scripts/generate.mjs`
turns it into ready-made, collision-proof files under `dist/`: `web/tokens.css` (`--pj-*` variables),
`ios/PadejaTokens.swift` (`PadejaTokens.*`), `android/PadejaTokens.kt` (`PadejaTokens.*`) and
`android/padeja_colors.xml` + `padeja_dimens.xml` (`padeja_*` resources). `node scripts/check.mjs`
compares the guide with what the real apps and pages use today and reports drift.

---

## 9. Rules for anything new

1. **Dark first.** Start from `background` + `card`; only court booking goes light.
2. **No new hex values.** Use a token above; if you truly need one, add it here first.
3. **One accent per screen.** `brand` for the main action; semantic colours only mean
   what they say (green = good, red = bad, amber = caution, red pill = live).
4. **Text on `brand`, `teal` and `win` is black**, never white.
5. **Radius 12 cards / 10 controls** unless a variant above says otherwise.
6. **Big numbers, small chrome.** Scores and standings are the hero.
7. **TV/tablet = bigger, bolder, higher contrast** than phone, and never scroll.
8. **Clubs change the accent only.**
9. Don't ship Material/Android-Studio template colours (the purple/pink defaults).

---

## 10. Known drift (fix over time)

| Where | Today | Should be |
|---|---|---|
| Club teal | iOS `#14B8A6` vs Android/web `#00D4AA` | `#00D4AA` |
| Canvas navy | `#0A1624` (feed), `#0D1B2A` (score), `#0A111E` (club web), `#0A1628` (early kiosk build) | `#0A1624` for apps; `#0A111E` only for club TVs |
| Loss red | `#F56040` (token), `#E24B4A` (72 raw uses), `#FF6B6B` (score) | `loss` for results, `danger` for destructive/errors, coral only for team B |
| Success green | `#3DE39E`, `#35D6A4`, `#1D9E75`, `#1FB97A` | `win` / `green` / `success` per section 2 |
| Gold | `#F5B83D` vs `#FFD700` | `draw` amber for status; `#FFD700` only for trophies |
| `PadejaCourtTablet` theme files | still Android-Studio purple/pink template | replace with this guide (the screen itself already has its own palette) |
| Wear and Feed `colors.xml` | template purples left in | delete unused entries |
| Web page palettes | Public pages use scoring navy `#0D1B2A`; `clubconsole` uses the core `#0A1624`; `live-scores` `#0B1220`; `booking` `#0B1220` with brand `#4FB7FF`; `competition` a light cream theme | one of: core, scoring or club-TV palette per page |
| Web gold | `#FFD54A` (public pages) vs `#F5B83D` (core) vs `#FFD700` (apps) | `#F5B83D` for status, `#FFD700` for trophies |
| Web fonts | Hanken Grotesk (public), Saira + Hanken Grotesk (club TV) | keep these two; no new families |
| Guide itself | Section 3.6 was first written from an out-of-date copy of the site | run `node scripts/check.mjs` before editing colours |
| Raw hex in views | hundreds of `Color(hex:)` calls | named tokens (section 8) |
