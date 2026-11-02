# context.md (Vatsala) — Everything we explored, and the constraints we must respect

Last updated: 2 Nov 2026. This file is the team's single source of truth. If a fact here is used in the pitch, re-check the linked source first.

---

## 1. Hackathon facts & rules (K! Hacks 4.0)

**Organiser:** CEG Tech Forum, College of Engineering Guindy, Anna University, Chennai.
**Format:** Round 1 online idea submission → top 25 teams → Round 2 24-hour offline hackathon.
**Tracks:** Women Empowerment, FinTech, Health Tech, Disaster Management, Environment & Sustainability, Agentic AI.
**Prize pool (from official site):** ₹6,00,000 total: 1st ₹2L, 2nd ₹1.5L, 3rd ₹1L, plus Best Women's Team and Best Coder.
**Showcase:** Top teams present at Kurukshetra 2027.

### Key dates
| Date | What |
|---|---|
| **27 Nov 2026** | Round 1 submission deadline |
| 5–9 Dec | Top 25 announced; **confirm within 2 days** or lose the spot |
| ~11 Dec | Fresh official problem statements released (7 days before) |
| 17 Dec (night) | Accommodation provided |
| **18–19 Dec** | 24-hour finale at Anna University |

⚠️ The rules say Round 1 results come 15–20 days before Round 2, but 5–9 Dec → 18 Dec is only 9–13 days. Plan travel early.

### Rules that constrain us
1. **Engineering students only**; team of 2–4; cross-college allowed; no shuffling.
2. **Round 1 must use the official template; no additions or modifications.**
3. **In the finale, teams must choose from the official problem statements** released ~11 Dec. Our idea must be adaptable.
4. **"No existing projects from previous hackathons; if found without prior disclosure, the team is disqualified."** → see §7.
5. The 2024 edition's rules also said core development must happen during the offline round (the 10 days are for planning/research only). The 4.0 text we have doesn't repeat this, but **assume it applies** and confirm with organisers.
6. Bring your own laptops and components; power and internet are provided.
7. **Judging criteria:** innovation, implementation, impact, business value, feasibility, presentation.
8. Travel is self-funded; food is provided.

### Past editions (for pattern-spotting)
- K! Hacks 2024 (Devfolio, 17–18 Feb 2024): tracks were Assistive Tech, FinTech, Health Tech, Logistics, Space Tech, Sports Tech. Same two-round, top-25 format.
- K! Hacks 2.0 (2025): reported domains included blockchain, fintech, cybersecurity.
- K! Hacks 3.0: tracks not found.
- **Pattern:** Health Tech appears every year; Women Empowerment and Agentic AI are new for 4.0.

---

## 2. Problem evidence (numbers we may use)

| Indicator | Value | Source / note |
|---|---|---|
| Maternal Mortality Ratio, India | ~87 per 1 lakh live births (SRS 2022–24); 88 in 2021–23 | SRS Special Bulletin; progress is slowing (only 1 point drop). SDG target <70 by 2030 |
| Lancet 2026 estimate | 116 per 1 lakh (2023), ~24,700 deaths | Different method from SRS; cite as "independent estimates are higher" |
| State variation | MP ~159 (SRS 2021–23) | High-burden states much worse than average |
| Anaemia, women 15–49 | 57.0% (NFHS-5, 2019–21) | **NFHS-6 reportedly dropped anaemia indicators**, so NFHS-5 is the latest national figure |
| Anaemia, pregnant women | 52.2% (NFHS-5) | Higher in poorest, teenage, tribal, less-educated women |
| Anaemia, women 15–19 | 59.1% (NFHS-5) | Links the adolescent stage to the maternal stage |
| Hygienic menstrual protection, 15–24 | 79.2% (NFHS-6, 2023–24), up from 77.6% | ~1 in 5 still not using hygienic methods; big rural/wealth/education gaps in NFHS-5 |
| ANC coverage | 95.9%; first-trimester ANC 76.2% (NFHS-6) | Women *are* reaching the system; the gap is between visits |
| IFA ≥100 days in pregnancy | 54.9% (NFHS-6) | Adherence reminders matter |
| Institutional deliveries | 90.6% (NFHS-6) | Most births in facilities, so postpartum *after discharge* is the gap |
| C-section rate | 27.2% (NFHS-6), up from 21.5% | More post-surgical recoveries at home |
| Women with own mobile phone | 63.6% (NFHS-6), was 54% | ~1 in 3 still don't, so we need a **shared-phone** design + ASHA channel |
| Women ever used internet | 64.3% (NFHS-6), was 33.3% | Big jump, but intermittent; **offline-first** still needed |
| Spousal violence (ever-married) | 22.3% (NFHS-6) | Supports discreet mode / privacy |

Pitch tip: use **at most three numbers** on the problem slide, e.g., MMR progress slowing, anaemia 57%, and 1 in 3 women without her own phone.

---

## 3. The ASHA reality (hard design constraint)

- India has roughly **one million ASHAs** serving rural populations (per Microsoft Research/Khushi Baby).
- ASHAs receive only about **23 days of basic training** (per Microsoft Research write-up on ASHABot).
- Multiple studies and reports (2024–2026) describe **app fatigue**. Workers juggle around seven apps plus WhatsApp groups and sheets. They enter the same data **twice (paper + app)**, use **personal phones and data at their own cost**, struggle with English menus, and face surveillance-style attendance apps.
- An ASHA program originally focused on maternal and child health now covers **30+ tasks**.

**Design rule derived from this:** *our product must remove work from the ASHA, never add it.* No forms. One ranked list. One-tap actions. A digest that works over plain SMS.

---

## 4. Government digital stack we must fit into (not compete with)

| System | What it is | How we relate |
|---|---|---|
| **JANANI** (launched May 2026) | Upgraded RCH portal: longitudinal records, QR-enabled digital MCH cards, high-risk alerts, due lists, self-registration, nearby facility info; integrates with U-WIN, POSHAN; ABHA/Aadhaar/mobile IDs. ~1.34 crore registrations at launch | **Biggest finding of our research.** It overlaps with reminders and HRP alerts. We position as the **woman-side, offline, voice companion** that *feeds into* JANANI via QR/ABHA, not a parallel record |
| RCH Portal / ANMOL | Worker-side tracking; ANMOL is the ANM tablet app | ASHAs/ANMs keep using these; we hand them a summary, not a new form |
| U-WIN | Digital vaccination registry, self-registration, scheduling | Our vaccine reminders mirror the UIP schedule; link out to U-WIN |
| MCP card | Mother & Child Protection card, the paper bible of ANC, danger signs and vaccines | **Source for our rules file** |
| PMSMA | Assured ANC on the 9th of every month | Built-in reminder |
| ABHA | Health ID | Optional link; never required |
| Kilkari / Mobile Academy | Govt voice-message programme (ARMMAN implements) | Complementary; don't duplicate content |

Note: integrating with live government APIs is not possible in a hackathon. We'll **format** outputs to match the MCP card/JANANI fields and say so honestly.

---

## 5. Competitive landscape (what already exists and what we learn)

### Large, proven programmes
- **Khushi Baby (Rajasthan).** Offline-ready CHIP apps for ASHA/ANM/MO, prioritised due lists, high-risk lists, dashboards. Around 75,000 health workers and 45 million records digitised; expanding to Karnataka and Maharashtra.
  - **ASHABot** (2024–): WhatsApp LLM (GPT-4 based) grounded on ~40 government/UNICEF documents. Hindi, English and Hinglish, with voice notes. If unsure, it routes to nurses, who reply within hours. 869 ASHAs onboarded and 24k+ messages at the time of the report; Udaipur only. Users asked many *social* questions (contraception, child marriage, family conflict).
  - *Lesson:* grounded RAG + expert-in-the-loop + voice works. Sensitive topics come up, so privacy matters.
- **ARMMAN mMitra / Kilkari.** Timed voice calls through pregnancy and infancy; Kilkari is the national programme. With Google (DeepMind), they built models predicting which women will drop out, used to target limited human calls, plus models for best call time slots (pickup up to ~12% better in some slots).
  - *Lesson:* AI is best used to **prioritise scarce human attention**, which is exactly our ASHA ranking.
- **Jacaranda Health PROMPTS (Kenya → Ghana, Nigeria, Eswatini, Tanzania; Nepal).** SMS-based, works on basic phones. Stage-based nudges + two-way helpdesk where AI triages by urgency and nurses respond. Danger-sign messages are escalated to a call. Reported outcomes: more ANC visits and much higher care-seeking for postpartum danger signs. An RCT found improved antenatal danger-sign knowledge but **no improvement in postpartum/neonatal danger-sign knowledge**.
  - *Lesson:* postpartum is the hardest; it is our opportunity. Feature-phone reach matters.
- **mSakhi (IntraHealth).** Older ASHA job-aid app; showed demand for multimedia, intuitive design for low-literacy users.

### Consumer femtech
- **Flo, Clue, Maya, etc.:** polished cycle tracking, mostly urban, English-first, cloud-stored.
- **Flo/Meta case:** the FTC settlement (2021) was over Flo sharing reproductive data. In Aug 2025 a California jury found Meta liable for collecting Flo users' data, and the verdict was upheld in Sept 2025.
  - *Lesson:* **no third-party analytics/ad SDKs**, on-device by default. Privacy can be a selling point.

### Hackathon competitors (expect similar teams)
- **BloomGuard** (GitHub): Next.js + FastAPI maternal tracker with risk engine and clinician view.
- **MaataRaksha** (HF/Streamlit): ML risk predictor for ASHAs on the **UCI Maternal Health Risk dataset** (~1,014 rows, Bangladesh).
- **SwasthyaAI** (GitHub): offline-first PWA for ASHAs; risk ML, voice, scheme checker, FHIR.
- **CodeTantra problem statement:** "Maternal Health Tracker for Rural Areas" with ASHA dashboard, offline sync, family view. This idea is **common**.
- **UP Govt Health Cell hackathon (Jun 2026):** WhatsApp-based pregnancy registration and maternal care. Shows **state demand**, and that judges will have seen this space.

**How we stand out:** (1) life-course from adolescence, (2) deterministic, cited danger-sign rules instead of an ML score on a tiny foreign dataset, (3) closed-loop referral with follow-up, (4) *zero-entry* ASHA design, (5) discreet mode for shared phones, (6) explicit JANANI-complementary positioning.

---

## 6. Technology options explored

| Need | Option | Decision |
|---|---|---|
| App shell | React + Vite PWA (team already knows it from Eunoia) vs. Flutter vs. native Android | **React PWA**: fastest for 24 h, installable, offline via service worker |
| Offline storage | IndexedDB via Dexie | **Dexie** |
| Offline sync | Outbox queue + background sync on reconnect | Build simple custom outbox |
| Safety logic | ML model vs. rules | **Rules (JSON) + tiny engine**; explainable, offline, clinically defensible |
| Online AI | Groq (already in Eunoia; supports tool calling) | **Groq** for the agent and Q&A, grounded on curated docs |
| On-device AI | Gemma 3n / Gemma 4 small models run offline on phones (LiteRT/MediaPipe; Google AI Edge Gallery); community projects already ship offline Indian health assistants with them | **Stretch goal only**: big download, device limits, hard in 24 h |
| Voice | Web Speech API (STT/TTS; quality/offline varies by device and language) + **pre-recorded audio** for critical messages | Both; critical messages never depend on TTS |
| Languages | i18next; Bhashini APIs exist for Indian languages (verify access/terms) | Ship EN + HI + TA; more if time |
| Maps / facilities | Leaflet + OSM tiles online; bundled facility JSON + haversine offline | Both |
| Notifications to ASHA | WhatsApp Business API (approval takes too long), Twilio sandbox, SMS gateway, Telegram bot | **SMS gateway or Twilio sandbox**; show a simulated ASHA phone as backup |
| Backend | Node/Express (Eunoia) + SQLite/Postgres | **Node + SQLite** for the demo |
| QR | qrcode + html5-qrcode | Yes |

---

## 7. The Eunoia repo: audit & disclosure

Repo: https://github.com/neevmodh/eunoia (3 commits, 11 open PRs at time of review).

**What it has (v2.0 per README):** React 18 + Vite + Tailwind client; Node/Express server; Groq LLM (llama-3.3-70b) with 5 system prompts; cycle logging + irregularity stats; "ML" PCOS risk (weighted scoring of 10 symptoms → 0–100); emotional distress keyword scoring; wellness score; myth analyser; learning hub; gamified streaks; anonymous JWT; CSV file storage; admin dashboard; rate limiting, input sanitisation, prompt-injection pattern blocking; emergency keyword detection; helpline list.

**Issues spotted:**
- README contains an unresolved **merge-conflict marker** (`<<<<<<< HEAD`). Fix before linking it anywhere judges might look.
- **CSV storage**: fine for a demo, not for health data (no encryption, concurrency issues).
- **Cloud-only AI**: nothing works offline; roadmap lists "Offline PWA" as future.
- **PCOS "risk score"**: a weighted sum presented as 0–100 risk sounds like a probability it isn't. Reframe it as "pattern worth checking with a doctor".
- **English-first**: Tamil/Telugu/Bengali listed as roadmap only.
- **Targets adolescents**: under DPDP, verifiable parental consent is needed for under-18 users (with possible health-service exemptions). Needs a consent design.
- **Helpline numbers** hard-coded: re-verify every number before the demo (also consider Tele-MANAS for mental health).

**Disclosure decision (important):**
- Rule: existing projects without disclosure = disqualification.
- **Plan:** (a) disclose Eunoia openly in the Round 1 submission as prior work by a team member; (b) **write all finale code fresh** during the 24 h; (c) reuse only *non-code* assets prepared during the planning window: education content, myth list, rules JSON, translations, facility data, audio clips, designs. (d) **Email the organisers to confirm** that this approach is acceptable. Keep the reply.

---

## 8. Legal, ethical & safety constraints

1. **Not a medical device; no diagnosis, no dosing.** Output is limited to education, "see someone within X", or "go now". Every screen has a disclaimer. Rules must be reviewed by a doctor/ANM before the finale (ask a faculty member from a medical college or a family doctor).
2. **RED errs toward caution.** Over-referral is acceptable; under-referral is not.
3. **LLM guardrails:** the LLM can't change triage level, can't recommend medicines or doses, and can't answer outside scope. Uncertain → "ask expert" queue.
4. **DPDP Act 2023 + DPDP Rules 2025** (notified 13–14 Nov 2025; phased enforcement, with consent/children obligations from ~May 2027):
   - Notice + specific consent; purpose limitation; erasure on request; breach reporting.
   - Under-18 users need **verifiable parental consent**; tracking/behavioural monitoring of children is restricted, with exemptions for healthcare providers acting to provide health services. For a hackathon, design the consent screens and data minimisation; get legal review before any real deployment.
5. **Mental health:** if distress or self-harm signals appear (Eunoia already detects keywords), show crisis helpline options gently and escalate to the ASHA only with consent unless there's an emergency.
6. **Shared phones and coercive households:** discreet mode, PIN, per-category sharing, no lock-screen notification text revealing pregnancy/period details.
7. **No ads, no third-party analytics, no data sale.**
8. **Accessibility:** large touch targets, pictograms, audio for everything critical, works for low literacy.

---

## 9. Clinical content sources to build the rules file

Primary (Indian, official): **MCP card** (danger signs, ANC/PNC schedule, vaccine schedule), MoHFW ANC and PNC guidelines, Home-Based Newborn Care (HBNC) visit schedule, **UIP immunisation schedule**, RKSK/Menstrual Hygiene Scheme material, Anaemia Mukt Bharat.
Secondary: WHO ANC recommendations, FIGO/RCOG patient leaflets on heavy menstrual bleeding.
**Every rule in `rules.json` must carry a `source` field.** No source, no rule.

---

## 10. Open questions (resolve before 27 Nov)

- [ ] Organisers: is disclosed prior work + fresh code acceptable? Can we prepare data/content assets in advance?
- [ ] Clinician reviewer for the rules file: who?
- [ ] Which demo district for facility data? (Pick one with public facility lists; Chennai/Kancheepuram is convenient for live judges.)
- [ ] SMS route for the demo: Twilio sandbox vs. local gateway vs. simulated phone?
- [ ] Languages: confirm EN + HI + TA; any team member fluent for voice recording?
- [x] Name decided: **Vatsala** (वत्सला, Sanskrit: tender, motherly affection). The prior project stays **Eunoia**; the disclosure in §7 should say "Vatsala builds on Eunoia v2; the finale build is a new codebase".
- [ ] Clash check for "Vatsala" on Play Store, GitHub, Devfolio, Unstop and trademark search (it is also a common personal name, so app clashes are possible).
- [ ] Does the template allow a link to a demo video/Figma? (Don't add slides if not.)

---

## 11. Decision log

| # | Decision | Why |
|---|---|---|
| D1 | Track = Women Empowerment (pitch Agentic AI layer as a highlight) | Track is new and less crowded than Health Tech; agentic referral loop shows AI depth |
| D2 | Rules engine, not ML risk score, for triage | Explainable, offline, clinically defensible; avoids the tiny-dataset trap competitors fall into |
| D3 | Complement JANANI via QR, don't replicate records | Govt launched JANANI in May 2026; judges may know it |
| D4 | ASHA side is zero-entry | Strong evidence of app fatigue |
| D5 | PWA over native | 24 h constraint; team's existing React skills |
| D6 | Fresh code at finale; disclose Eunoia | Hackathon rule on prior projects |
| D7 | On-device LLM only as stretch | Download size, device variability, time |
| D8 | Product name = **Vatsala**; prior project = Eunoia | Easy to say across Tamil/Hindi/English; warm, caring meaning; separate name makes the "new codebase" story clear while Eunoia is disclosed as prior work |

---

## 12. Source links (re-verify before quoting)

- K! Hacks 4.0 site: https://k-hacks.kurukshetraceg.org.in/
- Unstop listing: https://unstop.com/hackathons/k-hacks-40-anna-university-au-chennai-1772496
- K! Hacks 2024 (Devfolio, rules pattern): https://k-hacks.devfolio.co
- Eunoia repo: https://github.com/neevmodh/eunoia
- JANANI launch (May 2026): https://ommcomnews.com/india-news/govt-launches-janani-platform-to-strengthen-maternal-child-healthcare/
- MMR SRS 2022–24 (~87): https://newsable.asianetnews.com/india/indias-maternal-mortality-ratio-sees-massive-86-decline-since-1990-articleshow-6lfwi2m
- Lancet 2026 estimate coverage: https://www.indiatodayne.in/lifestyle/story/india-cuts-maternal-deaths-sharply-but-progress-slows-globally-lancet-study-1367020-2026-03-29
- NFHS-6 key findings: https://medicaldialogues.in/amp/news/health/india-sees-progress-in-maternal-and-child-health-immunisation-and-nutrition-nfhs-6-finds-171705 and https://kgs.live/current-affairs/daily-current-affairs/posts/national-family-health-survey-–-6
- NFHS-6 anaemia indicators dropped: https://english.gujaratsamachar.com/news/national/missing-health-data-in-nfhs-6-raise-concerns-about-accountability-31969407411.html
- NFHS-5 anaemia: https://www.downtoearth.org.in/health/anaemia-in-women-and-children-on-the-rise-assam-fares-worst-nfhs-5-80357 ; https://pubmed.ncbi.nlm.nih.gov/37888841/
- NFHS-5 menstrual hygiene gaps: https://www.tribuneindia.com/news/health/about-50-per-cent-of-women-aged-15-24-years-still-use-cloth-for-menstrual-protection-national-family-health-survey-5-393865
- Women's phone/internet NFHS-6: https://www.thenewsminute.com/news/womens-internet-use-nearly-doubles-but-access-gaps-remain
- Khushi Baby: https://www.khushibaby.org/pages/maternal-reproductive-health ; https://devex.shorthandstories.com/how-digital-record-keeping-is-strengthening-community-health-care-in-india/index.html
- ASHABot (Microsoft Research): https://www.microsoft.com/en-us/research/?p=1141120
- ARMMAN + Google: https://blog.google/intl/en-in/company-news/making-every-call-count-how-ai-is-supporting-mothers-in-india/ ; https://armman.org/?p=1770
- Jacaranda PROMPTS: https://gavi.org/news/document-library/prompts-ai-enabled-messaging-improve-delivery-and-uptake-immunisation ; https://poverty-action.org/impact-digital-health-platform-maternal-and-newborn-care-kenya ; https://solve.mit.edu/solutions/111012
- ASHA digital burden: https://newlinesmag.com/reportage/indias-digital-health-push-is-overworking-its-front-line-women/ ; https://www.preprints.org/manuscript/202507.1082 ; https://www.deccanherald.com/india/karnataka/ashas-overworked-not-paid-on-time-says-study-1181115.html
- Flo/Meta privacy: https://natlawreview.com/article/jury-finds-meta-liable-collecting-private-reproductive-health-data ; https://www.business-humanrights.org/en/latest-news/usa-courts-find-meta-violated-privacy-law-over-alleged-collection-of-flo-period-tracking-app-users-data/
- DPDP Rules 2025: https://www.biometricupdate.com/202511/india-notifies-its-sweeping-digital-personal-data-protection-rules ; https://www.amsshardul.com/insight/enforcement-of-the-dpdp-act-and-notification-of-the-dpdp-rules/
- Gemma on-device: https://blog.google/intl/en-in/company-news/gemma-fied-putting-the-power-of-our-most-capable-family-of-open-models-into-the-hands-of-every-indian-developer/ ; https://www.datacamp.com/tutorial/gemma-3n
- Competitor hackathon projects: https://github.com/zkkhan01/BloomGuard ; https://huggingface.co/maitry30/maataraksha-maternal-risk ; https://gh.r-mj.com/Sanss25/SwasthyaAI
- UP Govt maternal hackathon (2026): https://transform.up.gov.in/assets/hackathon/Organisation_Plan.pdf
