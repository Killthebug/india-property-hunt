# Tracker Spreadsheet — Schema (India)

The skill reads and writes a single `.xlsx` file with two sheets.

## File location

```
[YOUR_HUNT_DIR]/india_property_hunt.xlsx
```

Set `YOUR_HUNT_DIR` in your `config.md`. The skill creates this file on first run if it doesn't exist.

---

## Sheet 1: `Apartments` (1BHK / 2BHK / 3BHK)

| Column | Type | Notes |
|---|---|---|
| Title | Text | Listing title from the platform |
| BHK | Text | 1BHK / 2BHK / 3BHK |
| Platform | Text | NoBroker / Housing.com / 99acres / MagicBricks |
| URL | Hyperlink | Full listing URL — used for deduplication |
| Area | Text | Neighbourhood/locality name |
| Pincode | Text | e.g. 560102 |
| Rent (₹) | Number | Monthly rent in ₹ |
| Deposit (₹) | Number | Security deposit amount |
| Deposit (months) | Number | Deposit expressed as months of rent |
| Maintenance (₹) | Number | Monthly society maintenance |
| Brokerage (₹) | Number | Broker fee (₹0 if direct/NoBroker) |
| Available From | Date | Move-in availability date |
| Furnishing | Text | Fully furnished / Semi-furnished / Unfurnished |
| Area (sqft) | Number | Carpet/super built-up area |
| Water Supply | Text | Cauvery / Borewell / Tanker / Unknown |
| Power Backup | Text | Inverter / Genset / None / Unknown |
| Parking | Text | Car / Bike / Both / None |
| Amenities | Text | Gym, pool, clubhouse, garden, etc. |
| Society Name | Text | Apartment complex / society name |
| Construction Age | Text | New / <5 years / 5-10 years / 10+ years |
| Bachelor Friendly | Text | Yes / No / Unknown |
| Notes | Text | Any extra details |
| Status | Text | See status values below |
| Priority | Text | High / Medium / Low |
| Found On | Date | Date this row was added |

### Status values

| Status | Meaning |
|---|---|
| `NEW 🔴` | Just found, not yet contacted |
| `To Contact` | Shortlisted, ready to message |
| `Contacted` | Outreach message sent |
| `Viewing Booked` | Viewing confirmed |
| `Viewed` | Viewing done |
| `Rejected` | Not suitable or taken |
| `Negotiating` | In price/terms negotiation |
| `Offer Made` | Rental application submitted |
| `Secured ✅` | Agreement signed, deposit paid |

### Row colours

| Priority | Fill colour | Hex |
|---|---|---|
| High | Green | `E2EFDA` |
| Medium | Yellow | `FFFFC7` |
| Low | Red/orange | `FCE4D6` |

---

## Sheet 2: `Villas & Houses` (independent houses, villas)

Same columns as Apartments, with these differences:

| Column | Notes |
|---|---|
| BHK | 3BHK / 4BHK / Villa |
| Bachelor Friendly | Not usually applicable |

Additional columns:
| Column | Notes |
|---|---|
| Plot Area (sqft) | Land area |
| Gated Community | Yes / No |
| Security | 24x7 / None / Unknown |

---

## India-specific column details

### Deposit
Indian landlords typically ask for 6–10 months rent as security deposit.
- 6 months = standard
- 10 months = common in premium areas (Koramangala, Indiranagar)
- Some newer co-living spaces offer 1–2 month deposits

### Maintenance
Society maintenance is **separate from rent** in most cases:
- Mid-range: ₹2,000–₹4,000/month
- Premium gated communities: ₹5,000–₹8,000/month
- Always verify this amount before finalising

### Brokerage
- Via broker: 1 month rent (sometimes split between landlord and tenant)
- NoBroker: ₹0 brokerage
- Direct landlord: ₹0 brokerage

### Water Supply
- **Cauvery** — BWSSB municipal supply, most reliable
- **Borewell** — building's own bore, generally reliable
- **Tanker** — water bought by tanker, expensive and unreliable
- Always check this — it's a daily quality-of-life issue

---

## Deduplication

The skill loads all values from the `URL` column into a Python `set` at the start of each run. Any new listing whose URL already exists in the set is silently skipped.

---

## Manual setup (optional)

```bash
pip install openpyxl
python3 - <<'EOF'
import openpyxl
from openpyxl.styles import PatternFill, Font

wb = openpyxl.Workbook()

apartments_cols = [
    "Title","BHK","Platform","URL","Area","Pincode","Rent (₹)","Deposit (₹)",
    "Deposit (months)","Maintenance (₹)","Brokerage (₹)","Available From",
    "Furnishing","Area (sqft)","Water Supply","Power Backup","Parking",
    "Amenities","Society Name","Construction Age","Bachelor Friendly",
    "Notes","Status","Priority","Found On"
]

villas_cols = apartments_cols.copy()
villa_extra_idx = apartments_cols.index("Amenities") + 1
for col in ["Plot Area (sqft)", "Gated Community", "Security"]:
    villas_cols.insert(villa_extra_idx, col)

for sheet_name, cols in [("Apartments", apartments_cols), ("Villas & Houses", villas_cols)]:
    ws = wb.create_sheet(sheet_name)
    header_fill = PatternFill("solid", fgColor="1F3864")
    header_font = Font(color="FFFFFF", bold=True, name="Arial", size=11)
    for i, col in enumerate(cols, 1):
        cell = ws.cell(row=1, column=i, value=col)
        cell.fill = header_fill
        cell.font = header_font
    ws.freeze_panes = "A2"
    ws.auto_filter.ref = ws.dimensions

if "Sheet" in wb.sheetnames:
    del wb["Sheet"]

import pathlib
path = pathlib.Path.home() / "india-property-hunt" / "india_property_hunt.xlsx"
path.parent.mkdir(parents=True, exist_ok=True)
wb.save(path)
print(f"Created {path}")
EOF
```