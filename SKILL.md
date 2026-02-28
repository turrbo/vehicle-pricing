---
name: vehicle-pricing
description: "Analyze vehicle pricing and determine deal quality by comparing against market data from CarGurus, AutoTempest, Cars.com, KBB, Edmunds, and other platforms. Use when the user asks to: (1) Check if a vehicle listing is a good deal, (2) Find fair market price for a specific year/make/model/trim/mileage, (3) Evaluate a vehicle listing URL, (4) Determine what a dealer should pay wholesale to resell at profit, (5) Compare vehicle prices across platforms, (6) Get depreciation forecast or cost of ownership, (7) Check recalls on a vehicle, (8) Value a salvage or rebuilt title vehicle, or any vehicle pricing, valuation, or deal analysis task."
---

# Vehicle Pricing

Analyze vehicle pricing across multiple platforms to determine deal quality, fair market value, dealer wholesale buy prices, depreciation forecasts, cost of ownership, recall status, and market supply conditions.

## Input Modes

1. **Vehicle link**: User provides a URL to a specific listing (CarGurus, AutoTempest, Cars.com, Facebook Marketplace, Craigslist, etc.)
2. **Vehicle details**: User provides Year, Make, Model, Trim, and Mileage
3. **Dealer mode**: Either input above, plus user requests dealer buy price analysis

## Workflow

### Step 1: Gather Vehicle Details

**If user provided a URL:**
1. Use `browser navigate` to open the listing URL
2. Extract: year, make, model, trim, mileage, listed price, seller type, location, VIN (if visible)
3. Take a screenshot for reference

**If user provided vehicle details:**
1. Confirm: year, make, model, trim, mileage
2. If trim is unknown, search for common trims to clarify with user

**If user provided a VIN:**
1. Decode via NHTSA API: `https://vpic.nhtsa.dot.gov/api/vehicles/DecodeVin/{VIN}?format=json`
2. Extract year, make, model, trim, engine details

### Step 2: Research Market Pricing

Search multiple platforms for comparable listings. Read [references/pricing-sources.md](references/pricing-sources.md) for platform-specific URL patterns and search strategies.

Run these searches using the `web-search` skill:
1. `{year} {make} {model} {trim} for sale price` (general market)
2. `site:cargurus.com {year} {make} {model} {trim}` (CarGurus deal ratings)
3. `kbb {year} {make} {model} {trim} fair market value {mileage} miles` (KBB valuation)
4. `edmunds {year} {make} {model} {trim} true market value` (Edmunds TMV)

Construct and visit AutoTempest URL directly:
```
https://www.autotempest.com/results?make={make}&model={model}&minyear={year}&maxyear={year}&maxmiles={mileage+10000}
```
Use `browser navigate` to load results and extract price data.

Collect from each source:
- Number of comparable listings found
- Price range (low to high)
- Median/average price
- Any deal ratings (CarGurus Great/Good/Fair)
- KBB and Edmunds valuations if available

### Step 3: Analyze the Deal

Read [references/deal-analysis.md](references/deal-analysis.md) for the complete deal rating methodology, mileage adjustments, and value factors.

1. Calculate market average from collected comparables
2. Adjust for mileage differences vs comparables
3. Factor in vehicle history if known (1-owner, accident-free, etc.)
4. Rate the deal: Excellent / Good / Fair / Above Market / Overpriced
5. Calculate what price ranges constitute each deal tier

**Salvage/rebuilt title vehicles**: If the vehicle has a non-clean title, read the "Salvage/Rebuilt Title Valuation" section in [references/additional-analysis.md](references/additional-analysis.md) for adjusted pricing methodology. Apply title discount to clean-title market value before rating the deal.

### Step 4: NHTSA Recall Check

Fetch recalls from the free NHTSA API:
```
https://api.nhtsa.gov/recalls/recallsByVehicle?make={make}&model={model}&modelYear={year}
```
Read the "NHTSA Recall Check" section in [references/additional-analysis.md](references/additional-analysis.md) for field extraction and presentation guidance.

Additionally, search `web-search` for `nhtsa complaints {year} {make} {model}` to surface common owner-reported issues.

### Step 5: Market Supply Assessment

Read the "Market Supply Indicator" section in [references/additional-analysis.md](references/additional-analysis.md).

Using listing counts gathered in Step 2:
1. Determine supply level (Flooded / High / Normal / Low / Scarce)
2. Assess negotiation leverage
3. Note days-on-market data if visible from CarGurus listings

### Step 6: Seasonal Pricing Check

Read the "Seasonal Pricing Patterns" section in [references/additional-analysis.md](references/additional-analysis.md).

Based on the current date and vehicle type:
1. Determine if seasonal pricing works for or against the buyer
2. Flag any upcoming timing events (year-end clearance, tax season, holiday sales)
3. Estimate seasonal price impact percentage

### Step 7: Depreciation Forecast

Read the "Depreciation Forecasting" section in [references/additional-analysis.md](references/additional-analysis.md).

1. Determine the vehicle's current age
2. Apply the depreciation rate for that age bracket, adjusted by make/model modifier
3. Project value at 6 months, 1 year, and 2 years
4. Search `web-search` for `{make} {model} depreciation rate resale value` for model-specific context

### Step 8: Cost of Ownership Estimate

Read the "Cost of Ownership Estimate" section in [references/additional-analysis.md](references/additional-analysis.md).

1. Calculate annual depreciation from Step 7
2. Estimate insurance using vehicle category table
3. Calculate fuel cost: search `{year} {make} {model} {trim} mpg` and apply formula
4. Estimate maintenance using vehicle category and age
5. Sum to annual total and cost per mile

### Step 9: Dealer Wholesale Analysis (if requested)

Only perform this step when the user asks for dealer buy price or wholesale value.

Read the "Dealer Wholesale Buy Price Analysis" section in [references/deal-analysis.md](references/deal-analysis.md) for the full cost breakdown formula.

Additional searches for wholesale context:
1. `{year} {make} {model} wholesale value auction` (wholesale market)
2. `kbb {year} {make} {model} trade-in value` (trade-in as wholesale proxy)

Calculate:
- Estimated reconditioning cost (based on vehicle age)
- Recommended max buy price, target buy price, and walk-away price
- Profit potential at different selling price scenarios

### Step 10: Present Results

Use the output templates from [references/deal-analysis.md](references/deal-analysis.md).

**For consumer deal analysis**: Present the Consumer Deal Report with market comparison, deal rating, recall status, market supply, seasonal timing, depreciation forecast, cost of ownership, and recommended price targets.

**For dealer wholesale analysis**: Present the Dealer Buy Report with cost breakdown, recommended buy prices, and profit scenarios.

Always include:
- Sources checked with dates
- Number of comparables found
- Open recalls (if any)
- Market supply level and negotiation leverage
- Seasonal timing impact
- Depreciation projection (6mo / 1yr / 2yr)
- Estimated annual cost of ownership
- Caveats (limited data, regional pricing variations, etc.)
- Recommendation on whether to buy, negotiate, or walk away
