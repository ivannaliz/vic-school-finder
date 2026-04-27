# Stage 1 — Strategy and Product Definition — COMPLETE
- [x] Product vision defined
- [x] Target audience confirmed
- [x] Competitor analysis — BetterEducation reviewed, gaps identified
- [x] Monetisation model decided — pay-per-report $25-35, free top 3 + paid full list and report
- [x] Personalisation approach — guided quiz 7 questions
- [x] Mobile-first confirmed
- [x] Solo build for V1
- [x] User journey mapped — all 6 phases, all school type branches
- [x] Address vs suburb entry decided — two search modes (precise and broad)
- [x] Out-of-zone handling designed
- [x] Report delivery decided — instant download + email copy
- [x] Search modes finalised — full quiz (7 questions, full address) and quick quiz (3 questions, suburb/postcode)

# Stage 2 — Data Strategy and Sourcing — IN PROGRESS
- [ ] BLOCKER: Confirm ACARA terms of use for commercial republishing before building
- [ ] Download ACARA My School annual data export (NAPLAN, enrolment, profiles)
- [ ] Download VCAA VCE school-level results (released each January)
- [ ] BLOCKER: Check data.vic.gov.au for Find My School zone boundary GIS data availability
- [ ] Compile school list from Independent Schools Victoria directory (is.vic.edu.au)
- [ ] DECIDE: Set up Google Places API account — understand cost at scale
- [ ] Design school record schema — all fields, sources, update frequency per field
- [ ] Plan annual ETL pipeline — download, clean, load process
- [ ] ABS socioeconomic data layer — download and map to school catchments

# Stage 3 — Tech Stack — DECIDED
- Frontend: Next.js (React, server-side rendering for SEO)
- Database: Supabase (managed Postgres, free tier, dashboard UI)
- Hosting: Vercel (free tier, auto-deploy from GitHub, native Next.js support)
- Payments: Stripe (one-time payment, Apple Pay + Google Pay, ABN required — BLOCKER)
- Email delivery: Resend (transactional email, 3,000 free/month, Next.js native)
- PDF generation: React PDF (@react-pdf/renderer, free, server-side)
- Maps: Mapbox (50,000 free map loads/month, swap to Google Maps later if needed — same effort either way)
- Address autocomplete: Google Places API
- Note: Mapbox can be swapped to Google Maps later with ~2-4 hours effort (one component file rewrite)
- [ ] ABN: must be active before Stripe can go live — BLOCKER (can build and test in sandbox without ABN)
- [ ] Set up Supabase account when Stage 5 Phase 1 begins

# Stage 4 — UX Design and Wireframes — IN PROGRESS
- [x] User journey fully mapped
- [x] Paywall placement decided — after top 3 results
- [x] School type branching designed
- [x] Landing page wireframed (v2) — see DESIGN.md
- [ ] Wireframe quiz flow — 7 screens + 3-screen quick quiz, mobile-first
- [ ] Wireframe results page — school cards, zone badges, match score, paywall blur
- [ ] Wireframe school detail page — 3 versions (government / private / selective)
- [ ] Wireframe compare mode
- [ ] Wireframe report purchase + delivery confirmation
- [ ] Test quiz flow with 2-3 real parents before building

# Stage 5 — V1 Build — NOT STARTED
- GitHub repo created: https://github.com/ivannaliz/vic-school-finder
- Local path: ~/Peronal Apps/vic-school-finder
- [ ] Phase 1: data layer — Supabase setup, school data import, postcode/suburb lookup
- [ ] Phase 2: quiz — mobile-first UI, 7-question full quiz + 3-question quick quiz, match score algorithm
- [ ] Phase 3: results page — school cards, zone badges, sort/filter, paywall blur
- [ ] Phase 4: school detail pages — 3 variants by school type
- [ ] Phase 5: compare mode
- [ ] Phase 6: Stripe payment integration + PDF report generation
- [ ] Phase 7: report delivery — instant download + email via Resend

# Stage 6 — SEO and Content Strategy — NOT STARTED
- [ ] Programmatic suburb pages: "Best schools near [suburb]" auto-generated for all VIC suburbs
- [ ] Region pages: "Top schools in Melbourne's North / East / South-East / West"
- [ ] School type pages: "Best government secondary schools VIC" etc.
- [ ] Write 3-5 evergreen guide articles: zone explainer, selective entry guide, private vs public, how rankings work, application timelines
- [ ] Submit sitemap to Google Search Console from day one

# Stage 7 — Legal and Compliance — NOT STARTED
- [ ] BLOCKER: Confirm ACARA / VCAA data republishing terms for commercial use
- [ ] BLOCKER: ABN must be active before Stripe goes live
- [ ] Privacy policy — address input, email collection, payment data
- [ ] Terms of service — accuracy disclaimer, ranking methodology note
- [ ] DECIDE: Data accuracy dispute process — what happens when a school disputes data
- [ ] GST obligations — understand threshold and requirements
- [ ] Disclaimer on all school pages: rankings based on available data, not an endorsement

# Stage 8 — Testing, Launch and Post-Launch — NOT STARTED
- [ ] Test quiz with real parents — does output feel accurate and useful?
- [ ] Test on real mobile devices — not just browser dev tools
- [ ] End-to-end payment and report delivery test
- [ ] Soft launch — share with 10-20 parents for feedback before going public
- [ ] Set up Google Analytics and Search Console
- [ ] Plan launch channels — Facebook parent groups, Reddit r/melbourne, local community groups
- [ ] Annual data refresh calendar: NAPLAN (mid-year), VCAA results (January)
- [ ] Add "report an error" button to every school page from day one
- [ ] Monitor for broken zone data, school closures, name changes
