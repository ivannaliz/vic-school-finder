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
- 9 screens, one per screen on mobile, progress bar, back/forward navigation, session state saved
- Screen 1: Full address entry with inline privacy note ("Used only to check zone eligibility — not stored or shared"), suburb/postcode alternative available
- Screen 2: Children entry — year level and target start year per child. Dynamic pricing pill updates live as children are added: 1 child $29 / 2 children $39 / 3+ children $49 (shown as "Family Report")
- Screen 3: School type preference — government / Catholic / independent / no preference
- Screen 4: Selective entry consideration — yes / not sure / no, with inline tooltip explaining selective entry
- Screen 5a: Top level priorities — tap to select from: academics, wellbeing, culture, enrichment, support. Auto-ranks in order tapped
- Screen 5b: Dynamic follow-up based on top priority selected in 5a. Academics branch: learning environment (explicit vs inquiry-based), senior pathway (VCE / VM / IB / not sure — secondary only), class size preference
- Screen 6: Enrichment and language — language toggle (reveals dropdown of 19+ Victorian curriculum languages when on), enrichment chips (performing arts, STEM, elite sport, music, visual arts, humanities)
- Screen 7: Fee budget per child per year — under $10k / $10-20k / $20k+ / prefer not to say — skippable
- Screen 8: Co-ed vs single-sex, school size (small community / large), school values (traditional / progressive / no preference) — skippable
- Screen 9: Specific needs (learning support, gifted and talented, disability support, EAL, allied health on site, none) + open text field "Anything else important to you?" — skippable. CTA reads "See my matches"
- Plain English throughout, inline tooltips explaining NAPLAN, VCE, ATAR, selective entry, ACER, Edutest
- Two quiz modes: full quiz (9 screens, full address) and quick quiz (3 screens, suburb/postcode)

# Search Modes
- Two distinct modes decided:
- Precise mode (full address): street-level zone matching for government schools, tailored to exact eligibility, 7-question full quiz, accurate zone results. Address input uses Google Places autocomplete. Inline privacy note: "Used only to check zone eligibility — not stored or shared"
- Broad mode (suburb/postcode): for parents relocating, exploring, or privacy-conscious. Shows all school types available in that area, zone results marked as approximate, 3-question quick quiz (primary or secondary, school type preference, one priority). Prompt at end of results: "For accurate zone checking, enter your address"
- Entry point: both modes accessed from the same "Find my school" CTA on landing page — choice presented as first step of quiz

# User Journey — 6 Phases
- Phase 1 — Discovery: landing page with hero CTA, trust signals, sample school card
- Phase 2 — Personalisation quiz: 7 questions (precise) or 3 questions (broad)
- Phase 3 — Free results: top 3 matches with match score, zone badge, key stats, out-of-zone handling
- Phase 4 — School detail pages: 3 variants — government (zone check, NAPLAN, VCE, profile), private/independent (fees, application process, academic data), selective entry (exam info, key schools, prep resources)
- Phase 5 — Compare and decide: compare mode up to 3 schools, free on 2 dimensions, paid on all dimensions
- Phase 6 — Purchase and delivery: Stripe checkout, instant PDF download, PDF emailed

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
