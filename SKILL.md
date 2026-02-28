---
name: vehicle-pricing
description: "Analyze vehicle pricing and determine deal quality by comparing against market data from CarGurus, AutoTempest, Cars.com, KBB, Edmunds, and other platforms. Use when the user asks to: (1) Check if a vehicle listing is a good deal, (2) Find fair market price for a specific year/make/model/trim/mileage, (3) Evaluate a vehicle listing URL, (4) Determine what a dealer should pay wholesale to resell at profit, (5) Compare vehicle prices across platforms, or any vehicle pricing, valuation, or deal analysis task."
---

# Vehicle Pricing

Analyze vehicle pricing across multiple platforms to determine deal quality, fair market value, and dealer wholesale buy prices.

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

### Step 4: Dealer Wholesale Analysis (if requested)

Only perform this step when the user asks for dealer buy price or wholesale value.

Read the "Dealer Wholesale Buy Price Analysis" section in [references/deal-analysis.md](references/deal-analysis.md) for the full cost breakdown formula.

Additional searches for wholesale context:
1. `{year} {make} {model} wholesale value auction` (wholesale market)
2. `kbb {year} {make} {model} trade-in value` (trade-in as wholesale proxy)

Calculate:
- Estimated reconditioning cost (based on vehicle age)
- Recommended max buy price, target buy price, and walk-away price
- Profit potential at different selling price scenarios

### Step 5: Present Results

Use the output templates from [references/deal-analysis.md](references/deal-analysis.md).

**For consumer deal analysis**: Present the Consumer Deal Report with market comparison, deal rating, and recommended price targets.

**For dealer wholesale analysis**: Present the Dealer Buy Report with cost breakdown, recommended buy prices, and profit scenarios.

Always include:
- Sources checked with dates
- Number of comparables found
- Caveats (limited data, regional pricing variations, etc.)
- Recommendation on whether to buy, negotiate, or walk away
