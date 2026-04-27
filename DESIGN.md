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
- Entry point: "Find my school" CTA launches quiz
- First screen of quiz presents two mode options:
  - Precise mode: "Enter your full address" with Google Places autocomplete, privacy note inline "Used only to check zone eligibility — not stored or shared"
  - Broad mode: "Search by suburb or postcode" for relocating, exploring, or privacy-conscious parents
- Precise mode: 7-question full quiz, street-level zone matching, accurate results
- Broad mode: 3-question quick quiz (primary or secondary, school type preference, one priority), shows all school types in area, zone results marked approximate, prompt at end to enter address for accurate zone checking
- Progress bar always visible
- Back button always visible
- One question per screen on mobile
- Inline tooltips on education terms: NAPLAN, VCE, ATAR, selective entry, ACER, Edutest

# Results Page Design Decisions
- Each school card shows: school name, type badge, match score (percentage + one-line reason), zone status badge (government only), key stat (NAPLAN percentile or VCE median), distance, fee range (private only)
- Free tier: top 3 cards fully visible
- Paywall: blurred cards below top 3, overlay with "X more schools match your profile", "Get full report — $29" button, 7-day money back guarantee
- Sort and filter bar: filter by school type, distance radius, fee range. Sort by match score, ranking, distance, fees
- Out-of-zone card: amber badge, expandable inline section explaining options, private/independent alternatives surfaced automatically, link to findmyschool.vic.gov.au

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
- Quiz flow (7-screen full + 3-screen quick)
- Results page
- School detail page (3 variants)
- Compare mode
- Report purchase and delivery confirmation
