# Design Principles
- Mobile-first always — design for mobile, scale up to desktop
- One question per screen on mobile for quiz flow
- Plain English throughout — no jargon anywhere
- Clean, minimal, trustworthy — not cluttered like BetterEducation
- One school one card — scannable, not overwhelming

# Brand
- App name: Vic School Finder
- Logo: Option A — graduation cap with flag pole icon, green square mark with rounded corners (border-radius 8px)
- Logo mark colour: #1D9E75 (primary green)
- Wordmark: "Vic School Finder" single line, font-weight 500, system font
- Dark mode wordmark: white text
- Primary colour: #1D9E75 (teal green)
- Secondary green (darker): #0F6E56
- Light green (backgrounds): #E1F5EE
- Dark green (text on light green): #085041
- Supporting colours: blue (#378ADD), purple (#7F77DD), coral (#D85A30), amber (#BA7517)
- Typography: system font stack (system-ui, -apple-system, sans-serif), weights 400 and 500 only

# School Type Badge Colours
- Government: blue (#E6F1FB background, #0C447C text)
- Independent / private: purple (#EEEDFE background, #26215C text)
- Selective entry: coral (#FAECE7 background, #712B13 text)
- In zone: green (#E1F5EE background, #085041 text)
- Out of zone / warning: amber (#FAEEDA background, #633806 text)
- Match score badge: green (#E1F5EE background, #085041 text)

# Landing Page — v2 (current)
- Navigation: logo left, "How it works" link right
- Hero section (secondary background): tag pill "Victoria's school guide", headline "Find the right school for your child, not just the top-ranked one" (em tag on last phrase in primary green), body copy explaining 7 questions and personalised shortlist, primary CTA button "Find my school — it's free" (full width, green), no secondary browse button (removed)
- Trust signals bar: 3 columns — "2,800+ VIC schools", "4 types (Gov, Catholic, independent, selective)", "Free (top 3 matches, no account needed)"
- Sample results section: one real school card (Melbourne High School, 96% match, selective entry badge, no zone required badge, VCE median 40.5, distance 3.2km, reason text), followed by one blurred card with paywall overlay ("4 more schools match your profile", "Get full report — $29" button)
- Browse by suburb section: REMOVED from landing page
- "Browse top schools instead" secondary CTA: REMOVED

# Quiz Flow Design Decisions
- One quiz flow, 9 screens — no separate quick quiz
- Two entry modes on Screen 1 only; Screens 2–9 are identical for both modes
- Progress bar fills incrementally across all 9 steps, always visible
- Back button always visible
- Skip options on screens 7, 8, 9 shown top right in nav bar in green
- One question per screen on mobile
- Inline tooltips on education terms: NAPLAN, VCE, ATAR, selective entry, ACER, Edutest
- Final CTA on screen 9 reads "See my matches" (not "Continue")

## Screen 1 — Entry Mode

- **Precise mode:** Full address input with Google Places autocomplete. Green privacy note: "Used only to check zone eligibility — not stored or shared". Zone results on results page show confirmed green/amber zone badge
- **Broad mode:** Suburb or postcode input. Amber warning note: "Without a full address, zone eligibility results will be approximate. You can enter your address at any time for precise zone checking". Secondary button always visible: "Enter my full address for precise zone checking". Zone results on results page show approximate zone badge with link to verify via findmyschool.vic.gov.au

## Screens 2–9 — Quiz Flow (identical for both entry modes)

- **Screen 1 — Address:** See entry mode section above
- **Screen 2 — Children:** Year level and target start year per child. Dynamic pricing pill updates live as children are added (green background #E1F5EE, text #085041): 1 child $29 / 2 children $39 / 3+ children $49 (labelled "Family Report")
- **Screen 3 — School type:** government / Catholic / independent / no preference
- **Screen 4 — Selective entry:** yes / not sure / no, with inline tooltip explaining selective entry
- **Screen 5a — Priorities:** Tap to select from academics, wellbeing, culture, enrichment, support. Auto-assigns rank number as parent taps in order; no drag required unless reordering
- **Screen 5b — Priority follow-up:** Completely different content depending on top priority from 5a. Academics branch: learning environment (explicit vs inquiry-based), senior pathway (VCE / VM / IB / not sure — secondary only), class size preference
- **Screen 6 — Enrichment and language:** Language toggle — off hides dropdown, on reveals selector with 19+ Victorian curriculum languages. Enrichment chips: performing arts, STEM, elite sport, music, visual arts, humanities
- **Screen 7 — Fee budget:** Per child per year — under $10k / $10-20k / $20k+ / prefer not to say. Skippable (skip top right, green)
- **Screen 8 — School character:** Co-ed vs single-sex, school size (small community / large), school values (traditional / progressive / no preference) grouped on one screen. Skippable
- **Screen 9 — Specific needs:** Chips: learning support, gifted and talented, disability support, EAL, allied health on site, none. Open text field placeholder "e.g. close to public transport, specific suburb…". Skippable. CTA: "See my matches"

# Results Page Design Decisions

## Layout and Navigation
- Default view: list view, map toggle at top of page
- Nav bar: logo left, "Edit quiz" link right (allows parents to adjust answers without restarting)
- Results header: summary of quiz inputs (suburb, number of children, school types selected)
- Filter chips: All types / Government / Independent / Selective / Catholic
- Sort: default by match score, tappable to change

## School Cards — Free Tier
- Labelled "Your top 3 matches — free" above first card
- Cards vary by school type:
  - Government: school name, match score, government badge, zone status badge (in zone green / out of zone amber), NAPLAN percentile, distance, one-line match reason
  - Independent/private: school name, match score, independent badge, waitlist badge if applicable, VCE median, fee per year, one-line match reason
  - Selective entry: school name, match score, selective entry badge, no zone required badge, VCE median, distance, one-line match reason

## Paywall
- Appears after top 3 cards on scroll
- Blurred card behind overlay
- Overlay shows number of additional matches
- "Get full report" CTA button
- All three pricing options visible: $29 one child / $39 two children / $49 three or more
- 7-day money back guarantee shown

## Out of Zone Alert
- Amber bordered component below paywall
- Shows which school is out of zone
- Explains circumstances where out-of-zone applications may be considered
- Links to findmyschool.vic.gov.au

## Map View
- Mapbox map with colour-coded pins by school type: selective coral / government blue / independent purple / home address green
- Tap pin shows school card below map
- Free top 3 only visible on map without payment
- Map tap interaction: to be validated with real device testing before build

# School Detail Page Design Decisions
- 3 variants by school type
- Government variant: zone check (in zone green / out of zone amber / borderline warning), NAPLAN percentile, VCE median, year-on-year trend chart, performance relative to socioeconomic context, enrolment size, specialist programs, extracurriculars, Google rating, link to school website
- Private/independent variant: annual tuition fee range, compulsory levies, scholarship info, application timeline, waitlist system explanation, entrance exam details (ACER or Edutest), interview process, required documents, VCE or IB results, NAPLAN percentile, university pathway rates, year-on-year trend
- Selective entry variant: exam type (SEAL test), test date window, exam content breakdown, no zone requirement note, key selective schools listed (Melbourne High, MacRobertson Girls, Nossal, Suzanne Cory, John Monash), prep resources, link to VCAA official materials

# Compare Mode Design Decisions
- Up to 3 schools side by side
- Parent selects which dimensions to compare
- Dimensions: academics, fees, distance, extracurriculars, application complexity, wellbeing
- Free: compare on 2 dimensions
- Paid: all dimensions, included in report purchase

# Report Design Decisions
- Format: PDF generated server-side using React PDF
- Delivery: instant download on confirmation page + emailed via Resend
- Contents: full matched school list ranked with match score breakdown, per-school key data and zone status or application requirements, trend direction, side-by-side comparison of shortlist, application checklist per school type, "your next steps" personalised action plan with dates, plain-English glossary (NAPLAN, VCE, ATAR, SEAL, ACER, Edutest)
- Price: $25-35 one-time
- 7-day money back guarantee shown on checkout page

# Screens Still to Wireframe
- Results page
- School detail page (3 variants)
- Compare mode
- Report purchase and delivery confirmation
