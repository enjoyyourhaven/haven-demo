# Haven's Honey Do's — Project Brief

## What this is
The web presence and app prototype for **Haven Property Services, LLC** — a woman-owned, safety-led home maintenance subscription business in the Dallas/Fort Worth area. Owner: Robin. Phone: (469) 960-3220. Website: enjoyyourhaven.com. Robin is a non-technical founder; explain things in plain language and confirm before destructive actions.

## Live site
Deployed via GitHub Pages from this repository (`enjoyyourhaven/haven-demo`):
**https://enjoyyourhaven.github.io/haven-demo/**

Any commit to `main` publishes within ~2 minutes.

## File map
- `index.html` — the shareable front door: brand header, five persona cards (each card links directly into a persona demo, full message shown, gold "Try your demo" banner), then a "Book your free walkthrough" form (`#book` — composes a prefilled text to Robin's phone or an email to robin@enjoyyourhaven.com; no backend), then contact card with phone/website. This is the link Robin texts/emails and points QR codes at.
- `demo.html` — the standard app demo (client-only, no login, opens as "Good morning, Sarah"). Fully self-contained HTML with demo data; also contains Supabase auth groundwork (inactive in demo mode).
- `demo-safety.html` — persona demo: Rachel Torres (independent woman; safety emphasis).
- `demo-family.html` — persona demo: Jessica Alvarez (busy family; kid-related tasks).
- `demo-senior.html` — persona demo: Eleanor Whitfield (senior; grab bars/threshold tasks, larger simple fonts for readability, "Shared with family" card).
- `demo-builder.html` — persona demo: David Chen (new-build homeowner in Prosper whose builder gifted year one; warranty-item honey-do list, builder-covered billing). Linked from the fifth "Is this you?" tile.
- All five demos end the home screen with a "This could be your home" card linking to `index.html#book`.
- `safety-first.html` — landing page: The Single Woman (capability/safety messaging — her home, on her terms; CTA "Book Your Visit").
- `first-year.html` — landing page: First-Time Home Buyer (CTA "Book Your First-Year Walkthrough").
- `busy-families.html` — landing page: Young Busy Family (CTA "Book Your Visit · Recurring Plans").
- `staying-home.html` — landing page: Senior Aging in Place + adult children ("For sons & daughters" section; CTA "Book a Home Safety Visit").
- `builders.html` — B2B page for custom home builders: the warranty-year model (builder buys year one as an amenity; Haven converts homeowner at renewal). CTA "Let's structure your warranty year."
- `qr-slide.html` — printable QR slide for presentations/print; QR points at the main index URL.

## Brand system
- Fonts: Playfair Display (serif headers) + Inter (body). Senior-facing surfaces use Inter only, larger sizes.
- Colors: navy #2B4570, sage #2D8B6F, cream #FAF9F4, gold #C9A452, honey-light #FEF3C7.
- Voice: warm, dignified, safety-forward, never salesy. Key phrases: "make your home your haven," "woman-owned · safety-led," "the house stops winning."

## The five client personas (drive all marketing decisions)
1. **Single woman homeowner** — emotional core: capability and independence — her home, on her terms. Trust: background checks first.
2. **First-time buyer** — wants a crash course; "first-year walkthrough" offer; anti-upsell promise.
3. **Busy family** — "a managed thing, not a recurring argument"; recurring visits; kids-safe vetting.
4. **Senior aging in place** — dual audience (senior + adult child decision-maker); dignity; documented visits; "home safety visit" offer.
5. **Custom home builder (B2B)** — paid acquisition channel: builder funds year one bundled with home sale; Haven wows homeowner for 12 months and converts at renewal.

## Known technical debt / cautions
- The demo apps are prototypes: demo data hardcoded client-side; not production-safe. Real client data must never go into these files.
- Production plan: Supabase backend (encrypted DB, server-side auth, row-level security), deploy with HTTPS. Demo files contain early Supabase wiring.
- Mobile viewport: the demo shell sizes via `--app-h` set from visualViewport JS + 100dvh fallback; portal sections need `min-height:0` (flexbox). `setH()` floors the value at `max(window.innerHeight, 380px)` — without that floor the topbar + bottom nav (~130px of unshrinkable chrome) eat the whole shell when the iOS keyboard opens in landscape and `.scroll-area` collapses to 0px. Don't regress these fixes.
- Demo dates self-refresh: a small IIFE before `</body>` in each demo rewrites every date at load relative to today (visit always 3 days out, weekday derived, past visits/tasks shift with it). It matches date strings in text nodes, so if you add or reword a date, add its token to that map or it will go stale.
- Form controls are 16px minimum (`.ig input/textarea/select`, `#isel`) — anything smaller makes iOS auto-zoom on focus and never zoom back out.

## Dormant defects — these arm the day real logins are enabled
The demos are inert mockups: the boot script sets `demoMode=true` and calls `enterPortal('client')`, `logout()` has zero callers, and the sign-in screen is unreachable. A 56-agent stress test (Jul 2026) confirmed the app is safe *because* of that. The following are real defects in code that simply cannot be reached today — fix them before wiring up real auth (e.g. logins for Manuel and Rodrigo):
- `saveTask()` never resets the picked service, priority, or form visibility, so the next task inherits the previous one — in the real branch that writes the wrong `service`/`priority` to the database.
- `saveTask()`'s demo branch returns *before* its own `if(!desc)` validation; an empty task reports "Saved ✓".
- No double-click guard on save (project convention requires one on every create-record button).
- `doLogin()` ignores `prof.error`, so any profiles read failure silently drops the user into the client portal.
- `loadTasks()`'s error branch injects the raw Supabase error message into `innerHTML` unescaped — the only unescaped sink in the app.
- `esc()` escapes only `& < >`; it is not attribute-safe.
- `enterPortal()` has no fallback for an unrecognized role, and a bad/missing `profiles.role` blanks the whole app.
- The boot script discards any restored Supabase session, so a signed-in user's real tasks would be replaced by demo data.
- Network failure and a paused Supabase project both surface to the user as "Incorrect email or password".
- Handyman/admin portals ship in the static HTML of a public page; today they hold only invented data, and the Admin Security panel asserts RBAC / 2FA / audit-log controls that have no implementation.
- Verified Jul 2026: RLS on the demo Supabase project (`sstipdekzaywxxcdrjks`) *is* enabled and correctly denies the anon key (`profiles`/`tasks`/`appointments` all return `[]` while a bogus table 404s). That project does allow open email signup. This is NOT the HavenPro project.
- IP protection pending: USPTO trademark for "Haven's Honey Do's," copyright registration. Keep the © 2026 Haven Property Services, LLC notice on all pages.

## Working conventions
- Ask before deleting or renaming files (links in the wild point at current filenames).
- After changes, remind Robin the site takes ~2 minutes to republish and to test in a private tab (cache).
- Test mobile scroll and bottom-nav visibility after touching the demo shell CSS.
