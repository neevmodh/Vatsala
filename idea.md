# Vatsala — idea.md

> **One line:** A voice-first, offline-first women's health companion that walks with a girl from her first period to her baby's first birthday. It flags danger signs with guideline-based rules and closes the loop with her ASHA worker, without adding a single extra form to the ASHA's day.

Track: **Women Empowerment** (secondary fit: Health Tech, Agentic AI)
Event: K! Hacks 4.0, CEG Tech Forum, Anna University. Round 1 deadline **27 Nov 2026**, finale **18–19 Dec 2026**.
Name: **Vatsala** (वत्सला, say it *VAT-sa-laa*). Sanskrit for tender, loving affection, the kind of care a mother gives her child. It is familiar across India and easy to say in Tamil, Hindi and English.
Tagline: **"Vatsala: tender care through every phase, from first period to first birthday."**
Vatsala grows out of our earlier project **Eunoia** (adolescent menstrual wellness); the new name marks the expanded scope into maternal care and the ASHA loop.

---

## 1. The problem, in one paragraph

India's maternal health system has strong *record-keeping* infrastructure. JANANI (launched May 2026) gives health workers and officials longitudinal records, due lists and high-risk alerts. The **woman herself** is still largely on her own **between visits**. When she bleeds at 2 a.m., gets a severe headache in week 34, or has a fever on day 5 after delivery, she often doesn't know it is dangerous, where to go, or who to call. Information reaches her through a mother-in-law, a shared phone, or nothing at all.

The same gap starts years earlier. About one in five young women still don't use a hygienic menstrual method. More than half of women of reproductive age are anaemic (NFHS-5), which carries straight into pregnancy. Menstrual health and maternal health are treated as two separate products, when they are one continuous life stage.

Meanwhile, the ASHA worker, the person who *could* close this loop, is already drowning in apps and double data entry. Any solution that adds work for her will fail.

## 2. What we merge

| From **Eunoia** (our prior repo) | From **Maternal & Menstrual Companion** idea | New in the merge |
|---|---|---|
| Stigma-free menstrual education, myth-vs-fact library | Pregnancy & postpartum tracking | **Life-course continuum**: adolescent → pre-conception → pregnancy → postpartum → back to cycles |
| Cycle tracker & irregularity detection | Checkup & vaccination reminders | **Deterministic danger-sign engine** (rules from the official MCP card and guidelines, not a black-box ML model) |
| AI chat (Groq), emotional-support mode, distress detection | Danger-sign flagging from symptoms | **Closed-loop referral agent**: flag → nearest *capable* facility → notify ASHA → follow up |
| Gamified streaks, wellness score | Nearest-facility referral | **Zero-entry ASHA view**: auto-ranked "today list" pushed by SMS/WhatsApp/voice |
| Admin dashboard | ASHA integration | **Offline-first + voice-first**, works on a shared phone with privacy mode |
| — | Multilingual | **QR handoff** into the government MCP card/JANANI flow instead of competing with it |

What we deliberately **drop or reframe** from Eunoia:
- **PCOS "risk score (0–100)"** becomes a **"pattern worth discussing with a doctor"** card with no percentage. A weighted score presented as a probability overstates what it knows.
- **Gamified points** stay for adolescent learning modules only, never for health logging during pregnancy. No one should "lose a streak" while unwell.
- **Cloud-only AI** stays as an online extra. Every safety-critical path works with zero internet and zero AI.

## 3. Who it's for (personas)

**Priya, 15, Class 10, rural Tamil Nadu.** Shares her mother's phone. Too embarrassed to ask about her irregular periods. Needs private, voice-based answers in Tamil, and to know when "irregular" means "see someone".

**Sunita, 23, first pregnancy, 7 months, Bihar.** Has the MCP card but can't read most of it. Her husband works in another state. Needs to know which symptoms mean *go now*, where the nearest 24×7 delivery point is, and reminders she can *hear*.

**Meena, 29, delivered 5 days ago.** Discharged after 48 hours. Postpartum is when attention drops and many complications appear. Needs day-by-day check-ins for herself, not just the baby.

**Lakshmi, ASHA, 41.** Covers ~1,000 people. Uses 5–7 apps already. Needs *fewer* things to do: one ranked list each morning telling her who needs a visit and why, which she can act on with one tap or a voice note.

## 4. The solution: five modules

### 4.1 Companion (woman-facing app, PWA, works offline)
- **Life-stage mode** switches automatically: *Cycle mode*, *Trying/Pre-conception*, *Pregnancy (week-by-week)*, *Postpartum (day 0–42)*, *Baby (0–12 months)*.
- **Voice-first:** every screen has a large "listen" button. Key safety messages are pre-recorded audio clips so they play offline. Input by tapping pictograms (no typing required) or speaking.
- **Daily 10-second check-in:** "How are you today?" with 3–6 pictogram symptoms relevant to the current stage.
- **Reminders:** ANC visits, IFA/calcium tablets, Td doses, PMSMA day (9th of every month), baby's vaccines. Schedules are loaded from a config file mirroring the MCP card and the UIP schedule.
- **Learn:** Eunoia's education library and myth-buster, re-cut into 60-second audio lessons per stage.

### 4.2 Danger-sign engine (the safety core)
- A **rules file (JSON)** encoding red flags per life stage, for example bleeding in pregnancy, severe headache with blurred vision, convulsions, fever after delivery, reduced fetal movement after 28 weeks, soaking a pad in under an hour, and thoughts of self-harm.
- Three outputs only: **GREEN** (self-care + learn), **AMBER** (see ASHA/ANM within 24–48 h), **RED** (go to facility now / call 108).
- It runs **on-device, offline, in milliseconds**, and every result shows *which rule fired*. That makes it explainable to a judge, a doctor and the woman herself.
- The LLM is **never** allowed to downgrade a RED.

### 4.3 Care Navigator agent (Agentic AI layer)
This agent is triggered by AMBER/RED or by a question the woman asks. Tools:
1. `find_facility(stage, severity, location)`: nearest facility that can actually handle it (e.g., a First Referral Unit with C-section and blood for RED in late pregnancy, not just the nearest sub-centre). Works offline from a bundled district facility file.
2. `notify_asha(woman_id, flag, summary)`: sends a short message to her ASHA (SMS/WhatsApp/voice). Queued offline and sent on reconnect.
3. `schedule_followup(hours)`: "Did you reach the hospital?" check-in after N hours. If there's no answer, it escalates to the ASHA.
4. `explain(rule, language)`: plain-language, voice explanation of *why* this matters.
5. `check_schemes(profile)`: points her to entitlements she may be missing, such as maternity benefit and free delivery services, so she knows care is free.
6. `ask_expert(question)`: questions the system can't answer confidently go to an ANM/nurse queue. This is the expert-in-the-loop pattern ASHABot uses.

Guardrails: tool calls are logged and the RED path is deterministic. The agent writes messages *for humans*. It never diagnoses or prescribes.

### 4.4 ASHA "Today" view (zero data entry)
- One screen. It is auto-ranked: **RED flags awaiting follow-up**, then **missed ANC/vaccines**, then **postpartum home-visit days due**, then **new registrations**.
- Each row has one-tap actions: *Visited*, *Called*, *Referred*, *Couldn't reach*. A voice note is optional.
- A daily summary is also pushed as **one SMS/WhatsApp message** with an audio version, so the ASHA doesn't even have to open the app.
- **QR scan:** the ASHA or ANM scans the woman's QR to link records and to read a structured summary card formatted like the MCP card. No retyping.

### 4.5 Privacy & shared-phone safety
- All data lives **encrypted on the device** by default. Sync to the ASHA is opt-in, per category ("share pregnancy data with my ASHA: yes; share period data: no").
- **Discreet mode:** the app icon and name can look like a generic "Notes/Calendar" app, with a PIN for the sensitive sections. This matters for adolescents and for women in controlling households.
- **No ad or analytics SDKs.** This is a direct lesson from the Flo/Meta case.
- Minors: designed for DPDP Act rules (verifiable parental consent for under-18s; a health-services exemption may apply). See context.md.

## 5. Why this beats what exists

| Existing | What it does well | Gap we fill |
|---|---|---|
| **JANANI / RCH / ANMOL / U-WIN** (Govt) | System of record for workers and officials; high-risk alerts; QR MCH cards | Woman-side, between-visit support; voice and offline for her; menstrual and adolescent stage. **We plug into it via QR rather than compete.** |
| **Khushi Baby CHIP + ASHABot** | Offline worker apps at state scale; WhatsApp LLM bot with nurse fallback for ASHAs | ASHABot answers *ASHAs'* questions; we serve the *woman* and push triaged work *to* the ASHA |
| **ARMMAN Kilkari / mMitra** | Massive scale voice calls; AI to predict dropout and best call time | One-way content; no symptom triage or referral loop |
| **Jacaranda PROMPTS** (Kenya, Ghana, etc.) | SMS two-way helpdesk; AI triage by urgency; strong evidence | Africa-focused; needs a staffed helpdesk; no menstrual/adolescent stage |
| **Flo, Clue, Maya, etc.** | Polished cycle tracking | English/urban; cloud data; no referral; privacy scandals |
| **Typical hackathon projects** (BloomGuard, MaataRaksha, SwasthyaAI…) | ASHA dashboard + ML risk on a public dataset | Usually trained on the small UCI dataset (Bangladesh, ~1,000 rows); add ASHA *work*; pregnancy-only; no closed loop |

**Our edge in one sentence:** we're the only concept in this list that spans *first period → postpartum*, keeps safety logic *deterministic and offline*, and **reduces** the ASHA's workload instead of adding to it.

## 6. Demo story (what judges will see in 5 minutes)

1. **Priya (cycle mode, Tamil voice):** logs "bleeding 9 days". The engine returns AMBER with the reason shown, and she hears a 30-second explanation. She switches on discreet mode.
2. **Sunita (week 34, Hindi, airplane mode on):** taps "headache" + "blurry vision". The screen turns RED in under a second. The navigator shows the nearest FRU (not the sub-centre) with distance and a "Call 108" button. The ASHA notification is *queued*.
3. **Turn Wi-Fi on:** the queued alert syncs. The ASHA phone buzzes with SMS: *"Sunita, 34 wks, RED: headache+vision, referred to CHC X, follow up by 6 pm."*
4. **ASHA Today view:** Sunita is at the top. One tap: *Called*. The 4-hour follow-up timer shows.
5. **Meena (postpartum day 5):** reports fever. RED. The same loop runs. Then the scheme checker reminds her that delivery care at government facilities is free.
6. **Close:** "Every RED in this demo fired from a rule you can read. No internet was needed until the alert had to leave the phone."

## 7. Impact (to state carefully in the pitch)

We will *not* claim lives saved from a hackathon prototype. We will claim measurable, testable proxies:
- **Time-to-recognition** of a danger sign (seconds, on device)
- **Referral appropriateness** (right facility level for the flag)
- **Loop closure rate** (% of RED flags with an ASHA action logged within X hours)
- **ASHA minutes saved per day** (no duplicate entry; one ranked list)
- **Reach:** works on shared phones, offline, in local voice

Evidence that this model works elsewhere: Jacaranda reports that mothers who got danger-sign messages were far more likely to seek care for postpartum danger signs. ARMMAN/Google showed AI can target limited human follow-up to those most likely to drop out. Cite these as *analogous evidence*, not as our results.

## 8. Business / sustainability model (judging criterion: business value)

- **Primary buyer:** State NHMs and district health societies. They are already funding digital RCH tools and running hackathons for exactly this (e.g., UP Health Cell's 2026 WhatsApp pregnancy-registration hackathon).
- **Model:** open-source core (digital public good) + paid implementation/hosting/support per district (SaaS-style, priced per active beneficiary).
- **CSR channel:** corporates funding maternal health and menstrual hygiene programmes (Schedule VII eligible).
- **NGO channel:** organisations running adolescent or maternal programmes get a white-label version.
- **Never:** selling user data or ads.

## 9. Feasibility in 24 hours (what's real vs. mocked in the demo)

| Real in demo | Mocked / simulated (said honestly) |
|---|---|
| PWA installable, fully offline after first load | WhatsApp Business API: use SMS gateway or Twilio sandbox, or a simulated ASHA phone |
| Rules engine with 25–40 rules, 3 languages | Facility data for one demo district only |
| Offline facility finder (bundled JSON + distance) | JANANI integration: QR summary *formatted* for it, no live API |
| Queue-and-sync to backend | On-device LLM: stretch goal only |
| ASHA Today view + SMS | Expert queue answered by a teammate playing "ANM" |
| Online AI Q&A grounded on curated docs | — |

## 10. Risks & how we handle them

| Risk | Mitigation |
|---|---|
| Wrong medical advice | Rules sourced from MCP card/guidelines and reviewed by a clinician before the finale; LLM can't override; disclaimers; RED always errs toward "go" |
| Alert fatigue for ASHAs | Rank, deduplicate, cap daily pushes; AMBER batched into the daily digest, only RED pushed instantly |
| Privacy on shared phones | Discreet mode, PIN, on-device encryption, granular sharing |
| "Another app" rejection by ASHAs | Zero-entry design; SMS digest works without opening the app |
| Overlap with JANANI | Position as the citizen-side companion feeding *into* the official system |
| Problem statements change on 11 Dec | Modular design; see the mapping table in the implementation plan |

## 11. Round 1 submission: suggested content for the template slides

*(Use the official template exactly; don't add or remove slides. Map these into whatever sections it has.)*

- **Problem:** the between-visit gap + menstrual-to-maternal continuum + ASHA overload. Three numbers max (see context.md §2).
- **Solution:** one diagram: Woman's phone (offline rules) → Care Navigator agent → ASHA Today list → facility, with a QR arrow into JANANI.
- **Novelty:** life-course span, deterministic safety core, zero-entry ASHA design, discreet mode.
- **Tech:** PWA + IndexedDB + rules engine + LLM agent with tools + SMS + QR.
- **Feasibility:** what we build in 24 h (table in §9).
- **Impact & business:** proxies in §7, state NHM/CSR model in §8.
- **Prior work disclosure:** "Vatsala builds on our earlier open-source project Eunoia (link); all finale code will be new." See context.md §7.
