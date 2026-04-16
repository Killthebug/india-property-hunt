# India Property Hunt — Fluso Skill

An AI-powered workflow that searches Indian rental platforms daily, tracks listings in a spreadsheet, generates personalised outreach messages, and emails you a formatted summary — fully automatically.

Adapted from the [London Property Hunt](https://github.com/mikepapadim/london-property-hunt-public) for the Indian rental market.

[![GitHub stars](https://img.shields.io/badge/Stars-⭐-yellow)](https://github.com/Killthebug/india-property-hunt)
[![Platform](https://img.shields.io/badge/Platform-India-blue)](https://github.com/Killthebug/india-property-hunt)
[![License](https://img.shields.io/badge/License-MIT-green)](https://github.com/Killthebug/india-property-hunt)

---

## ✨ Features

- 🔍 **Searches 4 platforms** — NoBroker, Housing.com, 99acres, MagicBricks
- 📊 **Smart spreadsheet tracking** — deduplicates by URL, colour-coded by priority
- 🎯 **India-specific priority logic** — power backup, water supply, deposit months, brokerage, bachelor-friendly
- 📝 **Auto-generated outreach** — personalised messages with Indian landlord expectations
- 📧 **Plain-text email summaries** — works with Gmail MCP connector
- 🏠 **Bangalore IT corridor pricing** — pre-researched rental rates by area

---

## 🚀 Quick Start

```bash
git clone https://github.com/Killthebug/india-property-hunt.git
cd india-property-hunt
cp config.example.md config.md
# Edit config.md with your details
```

Then run in Claude Cowork / Fluso:
```
Run the India property hunt skill — search all platforms, update tracker, send email
```

No browser automation, no MCP extensions, no CLI installs needed. Fluso handles everything using its built-in connectors.

---

## How it works with Fluso

1. **Search** — Fluso uses the Exa Search connector to find listings across NoBroker, Housing.com, 99acres, and MagicBricks in one pass
2. **Prioritise** — India-specific logic (power backup, water supply, deposit months, brokerage, bachelor-friendly) ranks every listing HIGH / MEDIUM / LOW
3. **Track** — Python + openpyxl updates a colour-coded spreadsheet (deduplicates by URL)
4. **Outreach** — Personalised `.txt` messages generated for every HIGH priority listing
5. **Email** — Gmail connector sends a plain-text summary straight to your inbox

---

## India vs London

| Feature | London | India |
|---|---|---|
| Platforms | SpareRoom, OpenRent, Rightmove, Zoopla | NoBroker, Housing.com, 99acres, MagicBricks |
| Currency | GBP (£) | INR (₹) |
| Deposit | 1 month | **6–10 months** |
| Brokerage | Often none | **1 month rent** |
| Maintenance | Usually included | **₹2,000–₹8,000/month extra** |
| Furnishing | Furnished/unfurnished | Semi-furnished most common |
| Key metric | Zone/commute | **IT corridor + traffic + water** |

---

## 📁 Repository Structure

```
india-property-hunt/
├── README.md              ← you are here
├── skill.md               ← Fluso skill prompt (drop-in)
├── config.example.md      ← personal config template
├── process_listings.py    ← test processor with sample listings
├── tracker/
│   └── README.md          ← spreadsheet column schema
├── outreach/              ← generated outreach files (gitignored)
├── docs/
│   └── research-notes.md  ← Bangalore market research
└── .gitignore
```

---

## 🏠 Bangalore IT Corridor Pricing (2026)

| Area | 1BHK | 2BHK | 3BHK | Major Employers |
|---|---|---|---|---|
| Electronic City | ₹18-20K | ₹28-35K | ₹45-55K | Dell, HP, Infosys, TCS |
| Whitefield | ₹25-30K | ₹40-50K | ₹55-70K | ITPL, EPIP |
| Marathahalli | ₹20-22K | ₹35-42K | ₹50-60K | RMZ Ecospace, ORR |
| HSR Layout | ₹22-28K | ₹38-45K | ₹55-65K | Startups, Embassy Tech |
| Bellandur | ₹22-28K | ₹38-45K | ₹55-65K | Embassy Tech Village |
| Sarjapur Road | ₹18-22K | ₹30-38K | ₹45-55K | Wipro, Infosys |
| Koramangala | ₹30-35K | ₹48-58K | ₹70-85K | Startups, Divyasree |
| Hebbal | ₹22-28K | ₹38-45K | ₹50-60K | Manyata Tech Park |
| Indiranagar | ₹25-32K | ₹45-60K | ₹65-90K | Metro, premium |

### 💰 Hidden Move-in Costs

| Cost | Typical |
|---|---|
| Security deposit | 6–10 months rent |
| Brokerage | 1 month (₹0 on NoBroker) |
| Maintenance | ₹2K–₹8K/month |
| WiFi | ₹700–₹1,500/month |
| **Total move-in** | **₹3–4L for ₹40K/month 2BHK** |

---

## 🎯 Priority Logic

**Apartments:**
- 🟢 **HIGH** — Primary areas + on budget + furnished + power backup + Cauvery water + no brokerage
- 🟡 **MEDIUM** — Secondary areas on budget, or primary with minor flags
- ⚪ **LOW** — Late availability, outer areas, unfurnished, high deposit, water issues

**India-specific checks on every listing:**
- ⚡ Power backup (inverter/genset)
- 💧 Water supply (Cauvery > borewell > tanker)
- 💰 Deposit months (≤6 preferred)
- 🤝 Brokerage amount
- 👤 Bachelor-friendly
- 🏗️ Construction age

---

## 📧 Email Summary Format

Every run sends a plain-text email with:
- HIGH/MEDIUM/LOW counts
- Each HIGH listing with ready-to-send outreach message
- MEDIUM condensed cards
- LOW/SKIP bullet list
- Backlog of uncontacted HIGH listings
- Stats + days until move-in

---

## ⚙️ Requirements

### For Fluso (recommended)
- [Claude Cowork](https://claude.ai) — the agentic workspace where this skill runs
- **Exa Search** connector — for finding listings across rental platforms
- **Gmail** connector — for sending email summaries (plain text)
- **Python 3 + openpyxl** — for spreadsheet operations (pre-installed in Fluso)

### For Claude Code (legacy)
> The original London version required Claude Code + Claude in Chrome MCP for browser automation. This India version is designed for **Fluso** and uses web search connectors instead — no browser automation, no MCP extensions, no Chrome dependency.
- Claude Code CLI
- Gmail connector
- Python 3 + openpyxl

---

## 🔌 Fluso Connectors Used

| Connector | Purpose | Required? |
|---|---|---|
| **Exa Search** | Search NoBroker, Housing.com, 99acres, MagicBricks | ✅ Yes |
| **Gmail** | Send plain-text email summaries | ✅ Yes |
| Google Calendar | Schedule recurring runs | Optional |
| GitHub | Push tracker to repo | Optional |
| Google Drive | Store tracker in the cloud | Optional |

---

## 📋 Adapting for Your Search

Edit `config.md` — the only file you need to change:

| Field | Example |
|---|---|
| Name | Jaipal |
| Age | 29 |
| Profile | Tech startup co-founder |
| Target areas | HSR Layout, Bellandur, Koramangala |
| Budget (2BHK) | ₹45,000 pcm |
| Max deposit | 6 months |
| Move-in | 1 June 2026 |
| Email | you@gmail.com |

---

## 💡 Tips for Indian Rentals

1. **Documents ready** — Aadhaar, PAN, salary slip, offer letter
2. **NoBroker first** — saves ₹40K+ brokerage
3. **Be fast** — good apartments go in 24–48 hours
4. **Check society rules** — bachelor restrictions, non-veg, pets
5. **Negotiate deposit** — some accept instalments
6. **Visit twice** — morning for noise, evening for parking
7. **Ask about maintenance** — always clarify what's extra
8. **Negotiate lock-in** — try for 6-month break clause

---

## 🤖 About Claude Cowork & Fluso

**Claude Cowork** is Anthropic's agentic workspace for running AI skills, workflows, and automations end-to-end.
**Fluso** is the personal Agentic Workspace Manager that orchestrates Claude Cowork skills with connected apps.

This skill was built to work natively with Fluso — it uses Fluso's connector system (Exa Search, Gmail) instead of browser automation, making it faster, more reliable, and zero-config.

---

*Built for [Claude Cowork](https://claude.ai) · Powered by [Fluso](https://fluso.ai)*
*Adapted from [London Property Hunt](https://github.com/mikepapadim/london-property-hunt-public) · April 2026*
