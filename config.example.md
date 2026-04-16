# Property Hunt — Personal Config (India)

> Copy this file to `config.md` and fill in your details.
> `config.md` is gitignored — your personal info stays local.

---

## About you

```
YOUR_NAME=Jaipal
YOUR_AGE=29
YOUR_PROFESSION=Co-founder & Head of Operations (Prem AI)
YOUR_PROFILE_DESCRIPTION=tech startup co-founder, clean, non-smoker, vegetarian, hybrid WFH, professional
YOUR_PROFILE_SUMMARY=Clean, tidy, reliable — co-founder at an AI startup, hybrid WFH, permanent role
```

## Work

```
YOUR_WORK_LOCATION=Remote / Hybrid (office in Berlin)
YOUR_WORK_POSTCODE=560001
PREFERRED_OFFICE_AREAS=ORR, Whitefield, Manyata Tech Park
```

## Target areas

List your areas in priority order, comma-separated.
The skill will use these to set priority tiers and generate search URLs.

```
PRIMARY_AREAS=HSR Layout, Bellandur, Koramangala, Indiranagar
SECONDARY_AREAS=Sarjapur Road, Marathahalli, Whitefield, Electronic City
TERTIARY_AREAS=Hebbal, JP Nagar, Jayanagar, Yelahanka
```

## Budget

```
BUDGET_1BHK=28000
BUDGET_2BHK=45000
BUDGET_3BHK=65000
MAX_DEPOSIT_MONTHS=6
MAX_MAINTENANCE=5000
BROKERAGE_ACCEPTABLE=No
```

## Property preferences

```
PROPERTY_TYPES=1BHK, 2BHK, 3BHK
PREFERRED_FURNISHING=Semi-furnished
ACCEPTED_FURNISHING=Semi-furnished, Fully furnished, Unfurnished
MIN_BHK=1
MAX_BHK=3
NEW_CONSTRUCTION_PREFERRED=Yes
GATED_COMMUNITY_PREFERRED=Yes
```

## Dates

```
MOVE_IN_DATE=1 June 2026
MOVE_IN_MONTH=June
FLEXIBLE_DATES=Yes, can do mid-May or late June
```

## India-specific requirements

```
WATER_SUPPLY=Cauvery preferred
POWER_BACKUP=Required
VEGETARIAN_BUILDING_OK=Yes
BACHELOR_FRIENDLY=Yes
PET_FRIENDLY=No
NEAR_METRO=Preferred but not required
MAX_COMMUTE_MINUTES=45
```

## Email

```
YOUR_EMAIL=jpsinghgoud@gmail.com
```

Fluso will use the Gmail connector to send summaries to this address.
No account index needed — Fluso handles multi-account routing automatically.

## File paths

```
YOUR_HUNT_DIR=~/india-property-hunt
```

The skill will:
- Read/write `$YOUR_HUNT_DIR/india_property_hunt.xlsx`
- Save outreach files to `$YOUR_HUNT_DIR/outreach/`

Make sure the directory exists before running:
```bash
mkdir -p ~/india-property-hunt/outreach
```

---

## Platform search URLs

### NoBroker (zero brokerage — preferred platform)

```
NOBROKER_1BHK_URLS=
  https://www.nobroker.in/property/sale/bangalore/multiple?searchIntent=rent&bedroomNum=1&cityName=Bangalore&localityNames=HSR%20Layout,Bellandur,Koramangala
  https://www.nobroker.in/property/sale/bangalore/multiple?searchIntent=rent&bedroomNum=1&cityName=Bangalore&localityNames=Indiranagar,Sarjapur%20Road

NOBROKER_2BHK_URLS=
  https://www.nobroker.in/property/sale/bangalore/multiple?searchIntent=rent&bedroomNum=2&cityName=Bangalore&localityNames=HSR%20Layout,Bellandur,Koramangala
  https://www.nobroker.in/property/sale/bangalore/multiple?searchIntent=rent&bedroomNum=2&cityName=Bangalore&localityNames=Indiranagar,Sarjapur%20Road,Marathahalli

NOBROKER_3BHK_URLS=
  https://www.nobroker.in/property/sale/bangalore/multiple?searchIntent=rent&bedroomNum=3&cityName=Bangalore&localityNames=HSR%20Layout,Bellandur,Koramangala
```

### Housing.com

```
HOUSING_1BHK_URLS=
  https://housing.com/rent/1bhk-apartments-in-bangalore

HOUSING_2BHK_URLS=
  https://housing.com/rent/2bhk-apartments-in-bangalore
```

### 99acres

```
NINE9ACRES_URLS=
  https://www.99acres.com/property-in-bangalore-ffid?bed_type=1&listing_type=rent
```

### MagicBricks

```
MAGICBRICKS_URLS=
  https://www.magicbricks.com/property-for-rent-in-bangalore-real-estate
```

---

## Notes

- You can update this file any time — just re-run the skill and it picks up changes
- NoBroker eliminates brokerage entirely — always search there first
- In Bangalore, 10km commute = 60-90 min in peak traffic. Prioritise proximity to office.
- Security deposit is the biggest upfront cost (6-10 months). Budget ₹3-4L for move-in.
- Maintenance is separate from rent in most societies — always ask.