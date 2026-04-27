# Data Schema

## Overview
This document defines the complete database schema for Vic School Finder. All tables are stored in Supabase (managed Postgres). Data is sourced from ACARA annual downloads and updated once or twice per year via ETL pipeline. The ACARA SML ID is the master unique identifier linking all tables.

---

## Core identifier note
Every ACARA dataset shares a common set of fields. The ACARA SML ID is the unique school identifier used to join all tables. All tables also include Calendar Year, School Name, Suburb, State, Postcode, School Sector, School Type, Campus Type, and Rolled Reporting Description.

---

## Table 1: schools (master school directory)
Source: School Profile 2025 (free download) + School Location 2025 (free download)
Update frequency: Annually (new files released each year)

Fields:
- id — primary key (auto-generated UUID)
- acara_sml_id — unique ACARA school ID (integer, indexed)
- location_age_id — Australian Government Department of Education Location ID
- school_age_id — Australian Government Department of Education School ID
- school_name — official school name (text)
- suburb — suburb (text)
- state — state abbreviation (VIC, NSW, QLD etc.)
- postcode — postcode (text)
- school_sector — G=Government, C=Catholic, I=Independent
- school_type — Primary, Secondary, Combined, Special
- campus_type — School Single Entity, School Head Campus, School Sub-Campus
- rolled_reporting — Individual Reporting or Rolled Reporting
- latitude — decimal degrees (numeric)
- longitude — decimal degrees (numeric)
- lga — Local Government Area (text)
- statistical_area_1 — ABS Statistical Area Level 1 (text)
- statistical_area_2 — ABS Statistical Area Level 2 (text)
- statistical_area_3 — ABS Statistical Area Level 3 (text)
- statistical_area_4 — ABS Statistical Area Level 4 (text)
- abs_meshblock — ABS Meshblock (text)
- remoteness_area — ABS remoteness classification (text)
- calendar_year — year of data (integer)
- created_at — timestamp
- updated_at — timestamp

---

## Table 2: school_profiles (enrolment and socioeconomic data)
Source: School Profile 2008–2025 (free download)
Update frequency: Annually
Note: Store all years to support trend charts from day one

Fields:
- id — primary key
- acara_sml_id — foreign key → schools.acara_sml_id
- calendar_year — year of data (integer)
- total_enrolments — total student enrolments (integer)
- icsea — Index of Community Socio-Educational Advantage score (integer) — key for contextual comparison
- icsea_percentile — ICSEA percentile rank (integer)
- lbote_pct — percentage of students with Language Background Other Than English (numeric)
- indigenous_pct — percentage of Indigenous students (numeric)
- sea_lower_quartile_pct — percentage of students in lower socioeconomic quartile (numeric)
- sea_middle_quartiles_pct — percentage of students in middle socioeconomic quartiles (numeric)
- sea_upper_quartile_pct — percentage of students in upper socioeconomic quartile (numeric)

---

## Table 3: enrolments_by_grade
Source: Enrolments by Grade 2008–2025 (free download)
Update frequency: Annually

Fields:
- id — primary key
- acara_sml_id — foreign key → schools.acara_sml_id
- calendar_year — year of data (integer)
- foundation — Foundation/Prep enrolments (integer)
- year_1 — Year 1 enrolments (integer)
- year_2 — Year 2 enrolments (integer)
- year_3 — Year 3 enrolments (integer)
- year_4 — Year 4 enrolments (integer)
- year_5 — Year 5 enrolments (integer)
- year_6 — Year 6 enrolments (integer)
- year_7 — Year 7 enrolments (integer)
- year_8 — Year 8 enrolments (integer)
- year_9 — Year 9 enrolments (integer)
- year_10 — Year 10 enrolments (integer)
- year_11 — Year 11 enrolments (integer)
- year_12 — Year 12 enrolments (integer)
- ungraded_primary — ungraded primary enrolments (integer)
- ungraded_secondary — ungraded secondary enrolments (integer)
- total — total enrolments (integer)

---

## Table 4: naplan_results (requires ACARA Data Access application)
Source: NAPLAN Results dataset
Update frequency: Annually (mid-year)

Fields:
- id — primary key
- acara_sml_id — foreign key → schools.acara_sml_id
- calendar_year — year of data (integer)
- domain — Reading, Writing, Spelling, Grammar and Punctuation, Numeracy
- student_grade_level — Year 3, Year 5, Year 7, Year 9
- test_type — Online or Paper
- student_count — number of students assessed (integer)
- average_naplan_score — school average NAPLAN scale score (numeric)
- score_margin_lower — lower bound confidence interval at 90% (numeric)
- score_margin_upper — upper bound confidence interval at 90% (numeric)
- all_australian_average — national average NAPLAN score for same domain and grade (numeric)
- similar_students_average — average for students with similar socioeconomic background (numeric)
- colour_comparison_all — comparison colour to all Australian students (text)
- colour_comparison_similar — comparison colour to similar students (text)
- band_1_pct — percentage of students in Band 1 (numeric)
- band_2_pct — percentage of students in Band 2 (numeric)
- band_3_pct — percentage of students in Band 3 (numeric)
- band_4_pct — percentage of students in Band 4 (numeric)
- band_5_pct — percentage of students in Band 5 (numeric)
- band_6_pct — percentage of students in Band 6 (numeric)
- band_7_pct — percentage of students in Band 7 (numeric)
- band_8_pct — percentage of students in Band 8 (numeric)
- band_9_pct — percentage of students in Band 9 (numeric)
- band_10_pct — percentage of students in Band 10 (numeric)
- participation_rate — percentage of students who participated (numeric)
- assessed_pct — percentage assessed (numeric)
- exempt_pct — percentage exempted (numeric)
- absent_pct — percentage absent (numeric)
- withdrawn_pct — percentage withdrawn (numeric)

---

## Table 5: student_progress (requires ACARA Data Access application)
Source: Student Progress dataset
Update frequency: Annually

Fields:
- id — primary key
- acara_sml_id — foreign key → schools.acara_sml_id
- calendar_year — year of data (integer)
- calendar_year_range — year range (e.g. 2022-2024)
- domain — Reading, Writing, Numeracy
- student_grade_level_range — year level range (e.g. Year 3 to Year 5)
- matched_student_count — number of matched students (integer)
- matched_student_pct — matched students as percentage of assessed (numeric)
- prev_matched_avg_score — average NAPLAN score two years ago for matched students (numeric)
- prev_score_lower — lower confidence bound (numeric)
- prev_score_upper — upper confidence bound (numeric)
- current_matched_avg_score — current average NAPLAN score for matched students (numeric)
- current_score_lower — lower confidence bound (numeric)
- current_score_upper — upper confidence bound (numeric)
- average_student_progress — difference between previous and current matched average (numeric)
- similar_students_avg — average for similar students with same starting score (numeric)
- similar_students_progress — difference between matched and similar students progress (numeric)
- above_avg_progress_pct — percentage of students with above average progress (numeric)
- colour_comparison — colour comparison to similar students (text)
- prev_all_australian_avg — previous national average for domain and grade (numeric)
- current_all_australian_avg — current national average for domain and grade (numeric)

---

## Table 6: student_attendance (requires ACARA Data Access application)
Source: Student Attendance dataset
Update frequency: Annually (Semester 1 and Term 3)

Fields:
- id — primary key
- acara_sml_id — foreign key → schools.acara_sml_id
- calendar_year — year of data (integer)
- term_semester — Semester 1 or Term 3
- attendance_rate — overall attendance rate percentage (numeric)
- indigenous_attendance_rate — Indigenous student attendance rate (numeric)
- non_indigenous_attendance_rate — Non-Indigenous student attendance rate (numeric)
- attendance_level — percentage of students attending 90% or more of days (numeric)
- indigenous_attendance_level — Indigenous attendance level (numeric)
- non_indigenous_attendance_level — Non-Indigenous attendance level (numeric)

---

## Table 7: school_finances (requires ACARA Data Access application)
Source: Finance Data dataset
Update frequency: Annually

Fields:
- id — primary key
- acara_sml_id — foreign key → schools.acara_sml_id
- calendar_year — year of data (integer)
- income_australian_govt — Australian Government recurrent funding (numeric)
- income_state_govt — State/Territory Government recurrent funding (numeric)
- income_fees — fees, charges and parental contributions (numeric)
- income_other_private — other private income sources (numeric)
- total_gross_income — total gross recurrent income (numeric)
- total_net_recurrent_income — net recurrent income after deductions (numeric)
- total_capital_expenditure — total capital expenditure (numeric)
- fte_funded_enrolments — full-time equivalent funded enrolments (numeric)
- income_australian_govt_per_student — Australian Government funding per student (numeric)
- income_state_govt_per_student — State/Territory funding per student (numeric)
- income_fees_per_student — fees per student (numeric) — KEY field for fee estimation
- income_other_private_per_student — other private income per student (numeric)
- total_gross_income_per_student — total gross income per student (numeric)
- total_net_recurrent_income_per_student — net recurrent income per student (numeric)

---

## Table 8: senior_secondary_outcomes (requires ACARA Data Access application)
Source: Senior Secondary Outcomes dataset
Update frequency: Annually

Fields:
- id — primary key
- acara_sml_id — foreign key → schools.acara_sml_id
- calendar_year — year of data (integer)
- senior_secondary_certificates_awarded — total senior secondary certificates awarded (integer)
- completed_senior_secondary — total students completing senior secondary (integer)
- students_at_university_pct — proportion going to university (numeric) — KEY field
- students_at_tafe_pct — proportion going to TAFE/vocational study (numeric)
- students_in_employment_pct — proportion entering employment (numeric)

---

## Table 9: vet_in_schools (requires ACARA Data Access application)
Source: VET in Schools dataset
Update frequency: Annually

Fields:
- id — primary key
- acara_sml_id — foreign key → schools.acara_sml_id
- calendar_year — year of data (integer)
- vet_category — VET course enrolments or qualifications completed
- head_classification — broad field of education (ASCED)
- sub_classification — narrow field of education (ASCED)
- classification_total — total enrolments/completions (integer)
- certificate_1 — Certificate I count (integer)
- certificate_2 — Certificate II count (integer)
- certificate_3 — Certificate III count (integer)
- certificate_4 — Certificate IV count (integer)
- diploma_or_higher — Diploma or higher count (integer)
- other_certificate — other certificate count (integer)
- school_based_apprenticeships — SBAT count (integer)

---

## Table 10: quiz_sessions (app data — not ACARA)
Source: Generated by quiz flow
Update frequency: Real-time

Fields:
- id — primary key UUID
- session_token — anonymous session identifier (text, indexed)
- address_mode — precise or suburb (text)
- address_input — full address or suburb/postcode entered (text)
- latitude — geocoded latitude from address (numeric)
- longitude — geocoded longitude from address (numeric)
- children — JSON array of child objects [{year_level, start_year, transition_planning}]
- school_type_preference — JSON array [government, catholic, independent]
- selective_entry — yes, no, not_sure
- priorities — JSON array of ranked priorities
- priority_detail — JSON object of screen 5b answers keyed by top priority
- enrichment — JSON object of enrichment selections
- language_preference — specific language or null
- fee_budget — under_10k, 10k_20k, 20k_plus, prefer_not_to_say, null
- co_ed_preference — co_ed, single_sex, no_preference
- school_size_preference — small, large, no_preference
- school_values — traditional, progressive, no_preference
- specific_needs — JSON array of selected needs
- other_text — open text field response
- pricing_tier — 29, 39, 49 (integer)
- report_purchased — boolean
- payment_completed_at — timestamp
- email — hashed email address (text) — never store plain text
- created_at — timestamp
- updated_at — timestamp

---

## Table 11: reports (app data — not ACARA)
Source: Generated after purchase
Update frequency: Real-time

Fields:
- id — primary key UUID
- session_id — foreign key → quiz_sessions.id
- pricing_tier — 29, 39, 49
- stripe_payment_intent_id — Stripe payment reference (text)
- payment_status — pending, completed, refunded
- pdf_generated_at — timestamp
- pdf_storage_path — path to generated PDF in storage
- email_sent_at — timestamp
- created_at — timestamp

---

## Key notes for build

1. ACARA SML ID is the master join key across all tables — never use school name as a join key as names change
2. Always store the calendar_year field — this enables trend charts from day one even with one year of data
3. The icsea field in school_profiles is critical for contextual comparison — "performance relative to similar schools" feature depends on this
4. income_fees_per_student in school_finances is the best available proxy for private school fee estimation until we source direct fee data from school websites
5. students_at_university_pct in senior_secondary_outcomes is a key differentiator — no other platform surfaces this clearly
6. quiz_sessions and reports tables contain no ACARA data — they are entirely app-generated and not subject to ACARA terms
7. Email addresses must be hashed before storage — never store plain text emails (privacy policy requirement)
8. All ACARA data must be stored with encryption at rest — Supabase handles this natively
9. Cloud hosting must be Australia-based — use Supabase ap-southeast-2 (Sydney) region

---

## ETL pipeline notes

Annual update process:
1. Download new annual files from ACARA Data Access Program page
2. Run data cleaning scripts (to be built in Phase 1)
3. Load into Supabase via upsert on acara_sml_id + calendar_year
4. Verify row counts and spot-check key fields
5. Update data freshness timestamp in app settings table

NAPLAN data released: mid-year (approximately June-July)
School Profile, Location, Enrolment data released: approximately March-April each year
VCE/Senior Secondary data: published by VCAA each January — note this is separate from ACARA and sourced from VCAA directly

---

## Data not yet in schema (to add when sourced)

- VCAA VCE school-level results — median study scores, subject participation (source: VCAA annual release, January)
- Google Places ratings and review counts (source: Google Places API, real-time)
- School tour booking links (source: individual school websites, manual curation)
- Independent school fees (source: school websites, manual curation — income_fees_per_student is a proxy until this is built)
- Zone boundary GIS data (source: data.vic.gov.au — availability to be confirmed)
