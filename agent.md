# Agent notes for kankichi77.github.io

This file is for AI assistants working in this repo. Read it before changing pages, especially the homepage or HKU Catering.

The owner is a person, not a product team. Keep pages simple, static, and easy to edit by hand. Do not introduce a build step, a framework, a package manager, or a shared CSS/JS toolchain unless they ask.

## What this repo is

Personal GitHub Pages site:

- Live: https://kankichi77.github.io
- Repo: https://github.com/kankichi77/kankichi77.github.io
- Branch: `main` deploys as-is
- No generator. Each feature is a folder with its own `index.html`.

Ask before pushing. When they say “push”, commit the relevant work and push `main`.

## Site map

| Path | Page | Role |
|---|---|---|
| `/` (`index.html`) | Home | Menu of other pages on this site |
| `/hku/` | HKU Catering | Tap-to-order list of campus outlets |
| `/math/` | Papa's さんすうドリル | Existing math drills (Pico CSS + local `style.css`) |
| `/typing/` | Let's Type! | Existing typing practice (Bootstrap 4 + local JS/CSS) |
| `/learntocode/` | Beginner HTML sample | Teaching file. Keep it crude on purpose. |

Do not add scratch files to the home menu. `learntocode/` is a real page, not leftover demo junk.

## How to add a new page

1. Put it in its own folder: `name/index.html` so the URL is `/name/`.
2. Add a card on the homepage that links to `name/`.
3. Give the card its own pastel fill and a stronger pastel border (see homepage colors).
4. If the page should return home, use `href="/"` (root-relative), not `index.html` or `../`.
5. Stay mobile-first: `viewport` meta, large tap targets, one-column layout, no hover-only actions.

## Homepage (`index.html`)

The home page is a **simple menu of links to other pages on this site**. That is its whole job.

### Content rules

- Title text is **Hello you**. Do not change it to “Home” or add a subtitle. An earlier “Pick a page.” line was removed on purpose.
- Current cards, in this order:
  1. HKU Catering → `hku/` — “Order from campus outlets”
  2. Math → `math/` — “Papa's さんすうドリル”
  3. Typing → `typing/` — “Practice typing”
  4. Learn to Code → `learntocode/` — “A beginner HTML sample”
- The whole card is the link. No arrow, no separate button, no “Order now” pill here.

### Visual rules (current)

These were iterated in conversation. Prefer the current values over inventing a new palette.

- Page background: faint, slightly bright yellow, then lightened further → `#fff9d2`
- Cards: pastel fill that is **lighter than** the border
- Border: **3px**, same hue as the card, using the earlier (stronger) pastel
- No decorative arrows inside cards
- Mobile-first, max width ~40rem, system UI font, large tappable cards

Current card colors:

| Card | Fill | Border |
|---|---|---|
| HKU Catering | `#eaf9ef` | `#c8efd6` |
| Math | `#eaf3ff` | `#c9e0ff` |
| Typing | `#ffeee6` | `#ffd4c2` |
| Learn to Code | `#faeaf8` | `#f3cff0` |

Hover/focus may use a green outline (`#0b6b3a`) so the pastel border stays visible. Do not recolor the border to green on hover.

### What was rejected or reverted

- Neutral gray-green homepage background (too close to the catering page, then replaced with yellow)
- White cards (owner asked for pastels)
- Using the strong pastel as the fill (fill was then lightened; strong color moved to the border)
- 1px then 1.2px borders (now 3px)
- Arrow affordance on the right of each card (removed)

## HKU Catering (`hku/`)

Utility page: a phone-friendly list of HKU campus outlets that accept online orders. Tap a card → that outlet’s ordering site in a new tab.

### Source of truth

Official list: https://catering.hku.hk/en/eateries/

Only use restaurants from the **main body list** below the Location and Category filters. Ignore the “Temporary Closure” and “Adjusted Opening Hours” notices at the top of that official page.

**Include only outlets that have an “Order Now” button** on that main listing. If there is no button, skip the outlet (walk-up only, coming soon, staff-only, members-only, kiosks without online order, etc.).

When the official list was scraped (2026-08-18) there were 27 cards and **9** with Order Now. Those nine are on `hku/index.html`.

### The nine outlets

Keep names, locations, local image filenames, and order URLs together. If you refresh from the official site, re-check every Order Now URL; they are third-party carts and change.

| Name | Location (as shown) | Local image | Order URL |
|---|---|---|---|
| CYM Canteen | 4/F, Chong Yuet Ming Cultural Centre | `hku/img/cym-canteen.jpg` | `https://now.order.place/#/store/102858/mode/prekiosk` |
| Hong Kong Daily 香江冰室 | 4/F, Chong Yuet Ming Cultural Centre | `hku/img/hong-kong-daily.jpg` | `https://csd2.order.place/store/112841/mode/takeaway` |
| Kiosk by The Sandwich Club | Run Run Shaw Podium | `hku/img/sandwich-club-kiosk.jpg` | Azure `odoui1` shop, `poiId=1714` |
| Union Restaurant | 4/F Haking Wong Building (Podium) | `hku/img/union-restaurant.jpg` | `https://now.order.place/#/store/12827/mode/prekiosk` |
| Starbucks Coffee | Shop G. 03, G/F, Composite Building | `hku/img/starbucks-coffee.jpg` | `https://www.starbucks.com.hk/en/new-app-launch` (HK app page, not a store cart) |
| TAI TAI FOODTOPIA 台台果腹 | Shop G. 02, G/F, Composite Building | `hku/img/tai-tai-foodtopia.jpg` | `https://order.taitaiteaology.com/#/goodslist?...` |
| OORI HANSIK | Shop G. 01, G/F, Composite Building | `hku/img/oori-hansik.jpg` | `https://order.oorihansik.com/#/autoroute?...` |
| Grove | 2/F Academic Building, 3 Sassoon Road | `hku/img/grove.jpg` | `https://order.grove.hk/#/goodslist?...` |
| Wholesome Hub | G/F Lift Lobby, Laboratory Block, 21 Sassoon Road | `hku/img/wholesome-hub.jpg` | Azure `odoui1` shop, `poiId=2266` |

The official page misspells Wholesome Hub’s location as “Sassoon Raod”. We corrected it to “Sassoon Road” on our page.

Listing photos on the official site are outlet photos, not logos. Image `alt` attributes on the official page are often camera filenames; we use the restaurant name as `alt`.

### Images must be local

Do **not** hotlink `https://catering.hku.hk/cache/img/...`. The owner wants this page to keep working if HKU changes or deletes those files.

- Store files in `hku/img/`
- Name them with a readable restaurant slug (`cym-canteen.jpg`, `sandwich-club-kiosk.jpg`, …)
- Reference them as `img/filename.jpg` from `hku/index.html`
- If you add or replace an outlet, download its photo again and give it a clear name

### Page structure

- Self-contained HTML + embedded CSS (same idea as the homepage)
- Each outlet is one card: photo, name, location, “Order now” pill
- The **entire card** is the order link (`target="_blank"` `rel="noopener noreferrer"`)
- Green “Order now” pill is extra affordance, not a second link
- Footer, in this order:
  1. Link to the official eateries page for hours and outlets without online ordering
  2. `Home` → `/`

The catering page still uses a muted green-gray background (`#f3f4f1`) and white cards. That is separate from the yellow/pastel homepage. Do not restyle catering to match home unless asked.

### Layout history (do not resurrect)

Earlier paths that were discarded:

- Root file `hku-catering.html` with images in `hku-catering/`
- Then images sat next to the HTML
- Final layout: `hku/index.html` + `hku/img/`

Old URLs (`/hku-catering.html`) are gone. Do not recreate them.

## Learn to Code (`learntocode/`)

This is a **beginner HTML teaching sample**. It used to be the repo-root file `thisishtml.html`.

Leave the markup intentionally simple and a bit inconsistent (mixed `HTML`/`html` tag case, incomplete last paragraph, no CSS). Do not “fix” it into a modern page unless the owner is revising the lesson.

## Other existing pages

`math/` and `typing/` were not redesigned in the 2026-08 session. They already have their own CSS, and typing already links home with `/`. Do not restyle them just to match the new home/catering look.

Typing includes an old Google Analytics snippet (`UA-106862143-1`). Leave it unless asked.

## Working style the owner prefers

- Show a list / confirm data **before** building a page when they ask for a list first.
- Prefer one static HTML file with embedded CSS for small new pages.
- Mobile-friendly is required for new UI. Large tap targets. Check both a phone-width layout and the real links.
- Keep copy short. Personal tone is fine (“Hello you”).
- Do not add homepage links they did not ask for, except: once a page is a real site section, it belongs on the home menu.
- Do not expand a “move this file” task into a redesign of that file.
- When they say push, push. Otherwise leave commits unpushed.

## If you update the catering list

1. Fetch https://catering.hku.hk/en/eateries/ (the main `.campus-inner` cards, not the top notices).
2. Keep only cards with `a.order` / “Order Now”.
3. Download any new or changed photo into `hku/img/` with a readable name.
4. Update `hku/index.html` cards (name, location, local `img/`, order URL).
5. Show the owner the proposed add/remove list before replacing the page if the set of outlets changed.

## Files you should usually not invent

- No `package.json`, bundler, or shared `styles.css` unless requested
- No CMS, no backend
- No new markdown site docs except this file and `README.md` (README is only the live URL)
