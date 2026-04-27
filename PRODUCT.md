# Product Vision
- App name: Vic School Finder
- Australian school comparison web app starting with Victoria, with planned national expansion to all Australian states after V1
- Helps parents find and compare schools based on location, child's needs, and personal priorities
- Competitor: BetterEducation (bettereducation.com.au) — our goal is better UX, personalisation, and cleaner monetisation
- Solo build for V1, freelance help if product grows

# Target Audience
- All parent types: first-time parents overwhelmed by the system, parents relocating to Melbourne, high-achieving families chasing selective entry
- All school types: government, Catholic, independent, private, selective entry

# School Types and Key Context
- Government schools: require zone eligibility. Parents must live within the school zone to be accepted. Zone check via findmyschool.vic.gov.au. Zone boundaries are drawn street by street — a postcode is not sufficient for accurate zone checking
- Private and independent schools: not tied to school zones. Involves early application, application fees, interviews, entrance exams (ACER or Edutest), waitlist systems with priority for siblings and alumni. Required documents include birth certificates, school reports, immunisation records, passports/visas. Applications best done years in advance
- Catholic and religious schools: similar to independent in terms of application process, not zone dependent
- Selective entry schools (Melbourne High, MacRobertson Girls, Nossal High, Suzanne Cory, John Monash Science School): require entrance exam (SEAL test), no zone requirement, open to all VIC students, Year 9 entry (Year 10 for John Monash)
- Key registrations: independent schools registered with vrqa.vic.gov.au, directory at is.vic.edu.au

# Monetisation Model
- Pay-per-report model: $25-35 one-time payment, no subscription
- Free tier: guided quiz + top 3 personalised school matches with basic info
- Paid tier: full personalised school list + detailed match score breakdown + application checklist per school type + year-on-year trend data + compare mode (all dimensions) + personalised PDF report (download + email) + "your next steps" action plan
- Paywall triggers after top 3 results with blurred cards showing "X more schools match your profile"
- 7-day money back guarantee
- Report delivery: instant PDF download on confirmation page + same PDF emailed to address provided at checkout
- Panel of experts: considered but deferred to V2
- No ads

# Personalisation — Guided Quiz
- One quiz flow, 9 screens, one per screen on mobile, progress bar, back/forward navigation, session state saved
- Two entry modes on Screen 1 only — all remaining screens (2–9) are identical regardless of mode:
  - Precise mode: parent enters full address, Google Places autocomplete, inline privacy note "Used only to check zone eligibility — not stored or shared", street-level zone matching, confirmed zone results
  - Broad mode: parent enters suburb or postcode, amber warning note shown, zone results marked as approximate throughout, secondary option to switch to full address always visible
- Screen 1: Address entry — precise mode (full address) or broad mode (suburb/postcode). See entry mode details above
- Screen 2: Children entry — year level and target start year per child. Dynamic pricing pill updates live as children are added: 1 child $29 / 2 children $39 / 3+ children $49 (shown as "Family Report"). Transition planning toggle appears for children in Years 4–6 only: "Also planning ahead for secondary school?" — when on, secondary school options are included in results alongside primary. Note shown: "We will include secondary school options in your results so you can start planning early." Toggle hidden entirely for Year 7 and above. Edge case: parents with a primary-age child planning ahead for secondary are captured via this toggle, not a separate question
- Screen 3: School type preference — government / Catholic / independent / no preference
- Screen 4: Selective entry consideration — yes / not sure / no, with inline tooltip explaining selective entry
- Screen 5a: Top level priorities — tap to select from: academics, wellbeing, culture, enrichment, support. Auto-ranks in order tapped
- Screen 5b: Dynamic follow-up based on top priority selected in 5a. Academics branch: learning environment (explicit vs inquiry-based), senior pathway (VCE / VM / IB / not sure — secondary only), class size preference
- Screen 6: Enrichment and language — language toggle (reveals dropdown of 19+ Victorian curriculum languages when on), enrichment chips (performing arts, STEM, elite sport, music, visual arts, humanities)
- Screen 7: Fee budget per child per year — under $10k / $10-20k / $20k+ / prefer not to say — skippable
- Screen 8: Co-ed vs single-sex, school size (small community / large), school values (traditional / progressive / no preference) — skippable
- Screen 9: Specific needs (learning support, gifted and talented, disability support, EAL, allied health on site, none) + open text field "Anything else important to you?" — skippable. CTA reads "See my matches"
- Plain English throughout, inline tooltips explaining NAPLAN, VCE, ATAR, selective entry, ACER, Edutest

# Entry Modes
- One quiz, two ways to start — choice made on Screen 1:
- Precise mode (full address): street-level zone matching, confirmed zone status on results, Google Places autocomplete, inline privacy note shown
- Broad mode (suburb/postcode): for parents relocating, exploring, or privacy-conscious. Zone results marked as approximate throughout with amber visual treatment. Prompt always visible to switch to full address for precise zone checking. Results page shows approximate zone badge with link to verify via findmyschool.vic.gov.au
- Entry point: "Find my school" CTA on landing page — entry mode choice is Screen 1 of the quiz

# User Journey — 6 Phases
- Phase 1 — Discovery: landing page with hero CTA, trust signals, sample school card
- Phase 2 — Personalisation quiz: 9 screens, single flow, two entry modes on screen 1 (precise address or broad suburb/postcode)
- Phase 3 — Free results:
  - Two views: list view (default) and map view (toggle)
  - Nav bar shows "Edit quiz" link so parents can adjust answers without restarting
  - Results header summarises quiz inputs: suburb or address, number of children, school types selected
  - Filter chips: All types / Government / Independent / Selective / Catholic
  - Sort: default by match score, tappable to change
  - Free tier shows top 3 matches labelled "Your top 3 matches — free"
  - Card content varies by school type:
    - Government: match score, zone status badge (in zone green / out of zone amber), NAPLAN percentile, distance, one-line match reason
    - Independent/private: match score, waitlist badge if applicable, VCE median, fee per year, one-line match reason
    - Selective entry: match score, no zone required badge, VCE median, distance, one-line match reason
  - Paywall appears after top 3 cards on scroll — blurred card behind overlay, number of additional matches shown, "Get full report" CTA, all three pricing options visible ($29 one child / $39 two children / $49 three or more), 7-day money back guarantee
  - Out of zone alert: amber bordered component below paywall, explains circumstances, links to findmyschool.vic.gov.au
  - Map view: Mapbox, colour-coded pins by school type (selective coral / government blue / independent purple / home address green), tap pin shows school card below map, free top 3 only visible without payment, tap interaction to be validated with real device testing
- Phase 4 — School detail pages: 3 variants, all finalised
  - Shared: nav (back to results, + Add to compare), hero (school type badge, name, meta, match score), action buttons ("Book school tour" primary — parents are in research phase not ready to enrol, "School website", "Share"), sticky CTA with full pricing summary always visible while scrolling
  - Government: zone eligibility (in zone / out of zone / borderline — one state shown), NAPLAN percentiles, VCE median, year-on-year trend bars, socioeconomic context note, school profile
  - Private/independent: application and waitlist section at top (most urgent info), urgency banner, application timeline with timing badges, required documents, itemised fees, VCE/NAPLAN performance, school profile
  - Selective entry: key fact banner (no zone, no fees), SEAL exam detail (components, scoring, no interview), application timeline, exam preparation section, VCAA practice materials link. Tutoring directory is a V2 lead gen feature — placeholder shown in V1. Other selective schools chips at bottom
- Phase 5 — Compare and decide:
  - Up to 3 schools side by side, dimension tabs (Academics / Fees / Distance / Programs / Wellbeing / Application)
  - Contextual summary banner — plain English insight reading the comparison data
  - Free rows: match score, VCE median, NAPLAN, trend, zone status, fees, entry type — winning value highlighted green
  - Locked rows: Extracurriculars, Wellbeing, Class size, Teaching approach — shown with "Unlock to see" label
  - "+ Add a third school to compare" dashed button, sticky "Unlock full comparison + report" CTA
- Phase 6 — Purchase and delivery:
  - Purchase screen: report preview card (6 items listed), plan pre-selected from quiz (1 child $29 / 2 children $39 / 3+ $49), 7-day guarantee, email field (no account required), Card / Apple Pay / Google Pay, pay button shows amount, Stripe security note
  - Delivery confirmation: clean success state (no back nav), download card (primary green), email confirmation card, 4-item next steps action plan, "Back to your school results" button

# Out-of-Zone Handling
- Amber "Out of zone" badge on government school cards
- Inline expansion: explains out-of-zone application process and circumstances schools may consider
- Automatically surfaces private/independent alternatives nearby
- Link to findmyschool.vic.gov.au to verify officially
- "Borderline" scenario: "Your address is close to the zone boundary — verify directly with the school"

# Match Score
- Each school shows a percentage match score with one-line plain-English reason
- Score based on: quiz answers mapped to school attributes (academic performance, school type, distance, fee range, special programs, selective entry status)
- Year-on-year trend: is this school rising or declining? (paid tier)
- Performance relative to socioeconomic context using ABS data — makes rankings fairer and more honest

# Data Sources
- ACARA My School (myschool.edu.au): school profiles, NAPLAN results, enrolment numbers, financial data. Annual data download (no public API). Terms of use for commercial republishing must be confirmed — BLOCKER
- VCAA: VCE school-level results released each January as PDF/Excel. Annual download, process, load into database
- ABS Schools Statistics: socioeconomic context per school catchment area
- Independent Schools Victoria (is.vic.edu.au): school directory
- VRQA (vrqa.vic.gov.au): registered independent schools
- data.vic.gov.au: Find My School zone boundary GIS data — must confirm availability — BLOCKER
- Google Places API: school ratings and review counts, address autocomplete
- School websites: fees, extracurriculars, photos
- Data approach: ETL pipeline — Extract (download annual files), Transform (clean, standardise, enrich), Load (into Supabase database). Run once or twice per year
- Historical data: schema must support multiple years from day one even if V1 only has one year

# Key Product Principles
- Mobile-first design always
- Plain English — no jargon, inline explanations for all education terms
- "School Match" not "School Rank" — personalisation over raw rankings
- Trust before paywall — free tier must be genuinely useful
- One school one card — clean, scannable, no walls of data
- Honest rankings — socioeconomic context layer, trend direction, not just raw ATAR
