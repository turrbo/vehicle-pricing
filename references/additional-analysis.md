# Additional Analysis Reference

## Depreciation Forecasting

### Average Annual Depreciation by Vehicle Age
| Year of Ownership | Depreciation from Previous Year |
|---|---|
| Year 1 (new) | 20-25% |
| Year 2 | 12-15% |
| Year 3 | 10-12% |
| Year 4 | 8-10% |
| Year 5 | 7-9% |
| Years 6-8 | 5-7% per year |
| Years 9-12 | 3-5% per year |
| Years 13+ | 1-3% per year (floor effect) |

### Depreciation Modifiers
Some vehicles depreciate faster or slower than average:

**Slower depreciation (retain value well):**
- Toyota Tacoma, 4Runner, Land Cruiser: -30% from average depreciation
- Jeep Wrangler/Gladiator: -35% from average depreciation
- Porsche 911, Honda Civic/CR-V: -20% from average depreciation
- Trucks (F-150, Silverado, RAM) in good condition: -15% from average

**Faster depreciation:**
- Luxury sedans (BMW 5/7, Mercedes E/S, Audi A6/A8): +20-40% faster than average
- Electric vehicles (non-Tesla): +15-25% faster (battery concerns, rapid tech changes)
- Nissan, Mitsubishi, Chrysler sedans: +10-20% faster than average
- High-mileage luxury: +25-35% faster

### Forecasting Formula
```
Future Value = Current Market Value x (1 - Annual Depreciation Rate)^years

For a used vehicle, determine current age then apply rates for future years.

Example: 2021 vehicle (4 years old), current value $25,000
  6-month forecast: $25,000 x (1 - 0.09)^0.5 = ~$23,850
  1-year forecast:  $25,000 x (1 - 0.09)^1   = ~$22,750
  2-year forecast:  $25,000 x (1 - 0.08)^2   = ~$21,160
```

### Search Strategy for Depreciation Context
Use `web-search` to search:
- `{make} {model} depreciation rate` for model-specific data
- `{make} {model} resale value retention` for brand reputation context

## Cost of Ownership Estimate

### Annual Cost Components

#### Insurance Estimates by Category
| Vehicle Category | Annual Insurance Estimate |
|---|---|
| Economy sedan (Civic, Corolla) | $1,200-$1,800 |
| Mid-size sedan (Camry, Accord) | $1,400-$2,000 |
| Compact SUV (RAV4, CR-V) | $1,500-$2,200 |
| Full-size SUV (Tahoe, Expedition) | $1,800-$2,800 |
| Truck (F-150, Silverado) | $1,600-$2,400 |
| Luxury sedan (3 Series, C-Class) | $2,000-$3,200 |
| Luxury SUV (X5, GLE) | $2,200-$3,600 |
| Sports car (Mustang, Camaro) | $2,000-$3,500 |
| Electric (Tesla Model 3/Y) | $1,800-$2,800 |

Note: These are rough national averages. Actual rates vary heavily by driver age, location, driving record, and coverage level. Present these as estimates only.

#### Fuel Cost Calculation
```
Annual Fuel Cost = (Annual Miles / Combined MPG) x Price Per Gallon

Default assumptions if user doesn't specify:
- Annual miles: 12,000
- Gas price: search current national average via web-search, or use $3.50/gal as fallback
- MPG: search "{year} {make} {model} {trim} mpg" via web-search
```

#### Maintenance Cost Estimates by Category
| Vehicle Category | Annual Maintenance (years 1-5) | Annual Maintenance (years 6-10) |
|---|---|---|
| Japanese economy (Toyota, Honda) | $400-$600 | $600-$1,000 |
| Japanese mid-size | $500-$800 | $700-$1,200 |
| American truck/SUV | $600-$900 | $900-$1,500 |
| Korean (Hyundai, Kia) | $400-$650 | $650-$1,100 |
| European mainstream (VW) | $700-$1,000 | $1,000-$1,800 |
| European luxury (BMW, MB, Audi) | $1,000-$1,800 | $1,500-$3,000 |
| Electric vehicles | $300-$500 | $400-$700 |

#### Total Cost of Ownership Formula
```
Annual Cost of Ownership =
  Depreciation (from forecasting section)
+ Insurance estimate
+ Fuel cost
+ Maintenance estimate
+ Registration/taxes (estimate ~1-2% of vehicle value annually)

5-Year Total Cost = Sum of annual costs over 5 years
Cost Per Mile = 5-Year Total / (annual miles x 5)
```

### Search Strategy
Use `web-search` to search:
- `{year} {make} {model} cost of ownership` for model-specific data
- `{year} {make} {model} common problems maintenance` for reliability context
- `{year} {make} {model} mpg fuel economy` for fuel cost accuracy

## Seasonal Pricing Patterns

### Monthly Price Trends
| Season | Vehicles That Get Cheaper | Vehicles That Get More Expensive |
|---|---|---|
| **Winter (Dec-Feb)** | Convertibles (-5-10%), RWD sports cars (-3-7%), motorcycles (-10-15%) | 4WD/AWD trucks and SUVs (+3-8%), snow-capable vehicles |
| **Spring (Mar-May)** | 4WD trucks/SUVs (cooling from winter premium) | Convertibles (+5-8%), sports cars (+3-5%) |
| **Summer (Jun-Aug)** | Most segments slightly elevated (peak buying season) | Convertibles (peak), Jeep Wranglers (peak) |
| **Fall (Sep-Nov)** | Current model year (new models arriving, -3-8%), summer vehicles cooling | Trucks pre-winter (+2-5%) |

### Key Timing Events
- **Year-end clearance (Nov-Dec)**: New car deals push used prices down 2-5%
- **Tax refund season (Feb-Apr)**: Demand spike, prices rise 2-5% especially for $10-20k vehicles
- **Memorial Day / July 4th / Labor Day**: Dealer promotions, slight buyer advantage
- **End of month**: Dealers more motivated to hit quotas, better negotiation window

### How to Apply
Determine the current month and vehicle type, then flag:
- If pricing is seasonally elevated: warn user they may get a better deal by waiting
- If pricing is seasonally depressed: note the timing advantage
- Include the estimated seasonal impact percentage in the analysis

## NHTSA Recall Check

### API Endpoint
```
https://api.nhtsa.gov/recalls/recallsByVehicle?make={make}&model={model}&modelYear={year}
```
- Free, no authentication required
- Returns JSON with all recalls for that vehicle

### Key Fields to Extract
- `NHTSACampaignNumber`: Unique recall ID
- `Component`: What part is affected
- `Summary`: Description of the defect
- `Consequence`: What could happen if not fixed
- `Remedy`: How it gets fixed
- `ReportReceivedDate`: When the recall was issued

### How to Present
- List any open recalls with component, summary, and remedy
- Note whether recalls are safety-critical vs minor
- Flag if multiple recalls exist (may indicate systemic quality issues for that model year)
- Remind user to verify recall completion via CARFAX or dealer service records if buying used

### NHTSA Complaints (Supplemental)
Search `web-search` for `nhtsa complaints {year} {make} {model}` to find common owner-reported issues that may not have resulted in formal recalls but affect reliability and value.

## Salvage/Rebuilt Title Valuation

### Title Types and Value Impact
| Title Status | Value vs Clean Title |
|---|---|
| **Clean** | 100% (baseline) |
| **Rebuilt/Reconstructed** | 50-70% of clean title value |
| **Salvage** | 40-60% of clean title value |
| **Flood/Water damage** | 30-50% of clean title value |
| **Lemon/Buyback** | 60-75% of clean title value |
| **Junk/Parts only** | 20-35% of clean title value |

### Salvage/Rebuilt Pricing Methodology
1. Calculate clean title market value using standard workflow
2. Apply title discount from table above
3. Additional adjustments:
   - **Type of damage matters**: Cosmetic-only damage (hail, minor collision) retains more value than structural/frame damage
   - **Quality of repair**: Professional rebuild with documentation worth more than unknown repair quality
   - **Insurance difficulty**: Some insurers won't cover salvage/rebuilt titles, or charge 20-40% more
   - **Resale difficulty**: Harder to sell, smaller buyer pool, factor in longer time to sell
   - **Financing limitations**: Many lenders won't finance salvage titles; rebuilt titles may have higher rates

### Special Considerations for Dealer Mode
- Dealers buying salvage/rebuilt should apply steeper discounts (additional 10-15% off)
- Reconditioning costs are typically higher and less predictable
- Longer average days on lot (45-90 days vs 30-45 for clean title)
- Some dealers avoid entirely; others specialize in this segment

### Search Strategy
- `web-search` for `{year} {make} {model} salvage value` or `rebuilt title value`
- Check if specific state has rebuilt title inspection requirements

## Market Supply Indicator

### How to Assess Supply
Count listings found across platforms during the pricing research phase:

| Listings Found (National) | Supply Level | Negotiation Leverage |
|---|---|---|
| 500+ | Flooded | High - many options, strong buyer position |
| 200-500 | High supply | Moderate-High - plenty of alternatives |
| 50-200 | Normal supply | Moderate - standard negotiation |
| 15-50 | Low supply | Low - fewer options, seller has advantage |
| <15 | Scarce | Very Low - limited choices, expect to pay market or above |

### How Supply Affects Strategy
- **Flooded market**: Recommend aggressive negotiation, walk-away power is high, no rush
- **High supply**: Good negotiation position, can be selective on condition/history
- **Normal supply**: Standard approach, moderate room to negotiate
- **Low supply**: Act faster on good deals, less room to negotiate, consider expanding search radius
- **Scarce**: If deal is fair, recommend acting quickly; waiting may mean fewer/worse options

### Search Strategy
The listing count from AutoTempest is the best single indicator since it aggregates multiple platforms. Also note:
- `web-search` for `{year} {make} {model} for sale` and note total results referenced
- If a specific trim is scarce but the model isn't, note that distinction
- Regional supply may differ from national (use zip/radius on AutoTempest)

### Days on Market Context
If days-on-market data is visible on listings (CarGurus shows this):
- **<15 days**: Fresh listing, less negotiation leverage
- **15-30 days**: Normal, moderate leverage
- **30-60 days**: Aging, good leverage for negotiation
- **60+ days**: Stale listing, strong leverage, seller likely motivated
