# Haven's Honey Do's — Project Brief

## What this is
The web presence and app prototype for **Haven Property Services, LLC** — a woman-owned, safety-led home maintenance subscription business in the Dallas/Fort Worth area. Owner: Robin. Phone: (469) 960-3220. Website: enjoyyourhaven.com. Robin is a non-technical founder; explain things in plain language and confirm before destructive actions.

## Live site
Deployed via GitHub Pages from this repository (`enjoyyourhaven/haven-demo`):
**https://enjoyyourhaven.github.io/haven-demo/**

Any commit to `main` publishes within ~2 minutes.

## File map
- `index.html` — the shareable front door: brand header, five persona cards (each card links directly into a persona demo, full message shown, gold "Try your demo" banner), then contact card with phone/website. This is the link Robin texts/emails and points QR codes at.
- `demo.html` — the standard app demo (client-only, no login, opens as "Good morning, Sarah"). Fully self-contained HTML with demo data; also contains Supabase auth groundwork (inactive in demo mode).
- `demo-safety.html` — persona demo: Rachel Torres (independent woman; safety emphasis).
- `demo-family.html` — persona demo: Jessica Alvarez (busy family; kid-related tasks).
- `demo-senior.html` — persona demo: Eleanor Whitfield (senior; grab bars/threshold tasks, larger simple fonts for readability).
- `safety-first.html` — landing page: The Single Woman (sovereignty/safety messaging; CTA "Book Your Visit").
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
1. **Single woman homeowner** — emotional core: sovereignty/autonomy. Trust: background checks first.
2. **First-time buyer** — wants a crash course; "first-year walkthrough" offer; anti-upsell promise.
3. **Busy family** — "a managed thing, not a recurring argument"; recurring visits; kids-safe vetting.
4. **Senior aging in place** — dual audience (senior + adult child decision-maker); dignity; documented visits; "home safety visit" offer.
5. **Custom home builder (B2B)** — paid acquisition channel: builder funds year one bundled with home sale; Haven wows homeowner for 12 months and converts at renewal.

## Known technical debt / cautions
- The demo apps are prototypes: demo data hardcoded client-side; not production-safe. Real client data must never go into these files.
- Production plan: Supabase backend (encrypted DB, server-side auth, row-level security), deploy with HTTPS. Demo files contain early Supabase wiring.
- Mobile viewport: the demo shell sizes via `--app-h` set from visualViewport JS + 100dvh fallback; portal sections need `min-height:0` (flexbox). Don't regress these fixes.
- IP protection pending: USPTO trademark for "Haven's Honey Do's," copyright registration. Keep the © 2026 Haven Property Services, LLC notice on all pages.

## Working conventions
- Ask before deleting or renaming files (links in the wild point at current filenames).
- After changes, remind Robin the site takes ~2 minutes to republish and to test in a private tab (cache).
- Test mobile scroll and bottom-nav visibility after touching the demo shell CSS.
