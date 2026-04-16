# India Property Hunt — Fluso Skill

> **How to use:** This is a drop-in skill for [Claude Cowork](https://claude.ai) / [Fluso](https://fluso.ai).
> Install it in your workspace `skills/` directory and Fluso auto-detects it.
> Before running, fill in your personal details in `config.md` (copy from `config.example.md`).
> All `[PLACEHOLDER]` values below are read from your config file.

---

## Skill prompt (Fluso reads this automatically)

```
You are running [YOUR_NAME]'s India property hunt. Do this automatically — no user present. Complete all steps fully.

## WHO IS [YOUR_NAME]
- [YOUR_AGE]yo [YOUR_PROFESSION]
- Work: [YOUR_WORK_LOCATION]
- Preferred office areas: [PREFERRED_OFFICE_AREAS]
- Best areas: [LIST_TARGET_AREAS]
- Move-in: ~[MOVE_IN_DATE] ([FLEXIBLE_DATES])
- Tenant profile: [YOUR_PROFILE_DESCRIPTION]
- Diet: [DIETARY_PREFERENCE] (check building allows it)
- Budget: 1BHK ≤₹[BUDGET_1BHK], 2BHK ≤₹[BUDGET_2BHK], 3BHK ≤₹[BUDGET_3BHK]
- Max deposit: [MAX_DEPOSIT_MONTHS] months
- Brokerage: [BROKERAGE_ACCEPTABLE]

## WHAT TO SEARCH FOR

### TYPE A — Apartments (1BHK, 2BHK, 3BHK)
- **CRITICAL: Must have power backup (inverter/genset). Skip if no backup mentioned.**
- **CRITICAL: Check water supply — Cauvery preferred, borewell acceptable, tanker = flag LOW.**
- **Furnishing:** [ACCEPTED_FURNISHING]. Semi-furnished preferred.
- **Bachelor-friendly:** [BACHELOR_FRIENDLY]. Some societies don't allow bachelors — skip these.
- **Maintenance:** Max ₹[MAX_MAINTENANCE]/month. Must be mentioned in listing or noted as "Unknown".
- **Deposit:** Max [MAX_DEPOSIT_MONTHS] months. 10-month deposits = flag LOW.
- **Brokerage:** [BROKERAGE_ACCEPTABLE]. If listing is via broker, note the cost.

**BHK filter — MANDATORY:**
- 1BHK → ADD ✅
- 2BHK → ADD ✅
- 3BHK → ADD ✅
- 4BHK+ → SKIP ❌ (unless looking for family)

**Age/construction filter:**
- New construction / <5 years → HIGH ✅
- 5-10 years → MEDIUM
- 10+ years → LOW unless renovated

Search NoBroker (zero brokerage):
[NOBROKER_URLS — one per area per BHK type]

Search Housing.com:
[HOUSING_URLS]

Search 99acres:
[NINE9ACRES_URLS]

Search MagicBricks:
[MAGICBRICKS_URLS]

For each listing, extract:
- Title, BHK type, area (sqft), rent (₹), deposit, maintenance
- Furnishing, water supply, power backup, parking
- Society name, amenities (gym, pool, clubhouse)
- Proximity to metro, office areas
- Brokerage amount (if any)
- Owner vs broker listing

### TYPE B — Villas / Independent Houses
- Budget: up to ₹[VILLA_BUDGET]
- Prefer gated communities with security
- Must have parking

### TYPE C — PG / Co-living (optional)
- Budget: up to ₹[PG_BUDGET]/month
- Check what's included (food, laundry, WiFi)

## TRACKER

File: [YOUR_HUNT_DIR]/india_property_hunt.xlsx
- Apartments → sheet: `Apartments`
- Villas/Houses → sheet: `Villas & Houses`

Deduplication: skip if URL already exists in the sheet.
New rows: Status = `NEW 🔴`, Found On = today's date

Priority for apartments:
- HIGH: [PRIMARY_AREAS] + ≤₹budget + available by ~[MOVE_IN_DATE] + semi/fully furnished + power backup + Cauvery/borewell + no brokerage + ≤6 month deposit
- MEDIUM: [SECONDARY_AREAS] within budget and timing, OR prime area with minor flags (unfurnished, 10-month deposit, brokerage)
- LOW: late availability, [TERTIARY_AREAS], unfurnished, high deposit, water issues, old construction

Priority for villas:
- HIGH: Gated community + primary areas + ≤ budget + furnished + amenities
- MEDIUM: Secondary areas within budget
- LOW: Late availability or outer areas

Row fill colours: HIGH = E2EFDA, MEDIUM = FFFFC7, LOW = FCE4D6

## EMAIL — PLAIN TEXT (Fluso Gmail connector supports plain text)

[YOUR_NAME] may only have their phone. Email must be fully actionable without opening any other file.

Use Fluso's Gmail connector (GMAIL__SEND_EMAIL) to send the email, To: [YOUR_EMAIL]
Note: The Gmail connector only supports plain text body. Do NOT send HTML — it renders as raw markup.
Subject: 🏠 India Property Hunt — {DATE} — {N} new listings

Plain text body sections:

**A — Header:** Date, run, platforms. Bold-style counts:
🟢 HIGH: N | 🟡 MEDIUM: N | ⚪ LOW: N | 📋 TOTAL: N

**B — 🟢 HIGH New Today:** For EVERY HIGH listing, a card with:
- Title | BHK | Area | ₹rent | Deposit | Maintenance | Furnishing | Water | Power | Platform
- URL as clickable link
- Green box with ready-to-send message (<100 words, personalised):
  "Hi, [one specific sentence about this listing — location, amenities, proximity to office, etc.]. I'm [YOUR_NAME], [YOUR_AGE], [YOUR_PROFESSION]. [YOUR_PROFILE_SUMMARY]. Looking to move ~[MOVE_IN_DATE]. I can provide salary slips, Aadhaar, and references. Happy to arrange a viewing."

**C — 🟡 MEDIUM New Today:** Title | Area | BHK | Price | short outreach

**D — ⚪ LOW/SKIP:** Bullet list with reason

**E — 🔁 Backlog:** Up to 8 uncontacted HIGH listings from tracker where Status = NEW 🔴, Found On ≠ today

**F — Stats:** Totals, area breakdown, deposit estimate, days until move-in
"⚠️ X days to [MOVE_IN_DATE]. Upfront cost estimate: ₹Y for deposit + rent + maintenance. Message at least 5 listings today."

## OUTREACH FILES
Save .txt files for HIGH priority to [YOUR_HUNT_DIR]/outreach/
Filename format: outreach_{platform}_{area}_{listing_id}.txt

## SUCCESS CRITERIA
- Both sheets updated, no 4BHK+ added, no buildings that don't allow bachelors added
- Power backup and water supply verified or flagged for every listing
- Outreach files saved for HIGH priority
- Email sent (always, even if zero new)
- Maintenance amount noted (or "Unknown")
- Deposit amount noted
- Brokerage noted (₹0 or amount)
```

---

## Notes on the placeholders

| Placeholder | Example value | Where to set |
|---|---|---|
| `[YOUR_NAME]` | Jaipal | config.md |
| `[YOUR_AGE]` | 29 | config.md |
| `[YOUR_PROFESSION]` | Co-founder & Head of Operations | config.md |
| `[YOUR_WORK_LOCATION]` | Remote / Hybrid | config.md |
| `[LIST_TARGET_AREAS]` | HSR Layout, Bellandur, Koramangala, Indiranagar | config.md |
| `[MOVE_IN_DATE]` | 1 June 2026 | config.md |
| `[YOUR_PROFILE_DESCRIPTION]` | tech startup co-founder, clean, non-smoker, vegetarian | config.md |
| `[BUDGET_1BHK]` | 28000 | config.md |
| `[BUDGET_2BHK]` | 45000 | config.md |
| `[BUDGET_3BHK]` | 65000 | config.md |
| `[MAX_DEPOSIT_MONTHS]` | 6 | config.md |
| `[BROKERAGE_ACCEPTABLE]` | No (prefer NoBroker/direct) | config.md |
| `[YOUR_EMAIL]` | you@gmail.com | config.md |
| `[YOUR_HUNT_DIR]` | ~/india-property-hunt | config.md |
| `[GMAIL_ACCOUNT_INDEX]` | 0 (first account) | config.md |