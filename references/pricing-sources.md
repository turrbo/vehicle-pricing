# Pricing Sources Reference

## Platform Search Strategies

### CarGurus
- **Search URL**: `https://www.cargurus.com/Cars/inventorylisting/viewDetailsFilterViewInventoryListing.action`
- **Deal Ratings**: Great Deal, Good Deal, Fair Deal, High Price, Overpriced
- **Best approach**: Use `web-search` skill to search `site:cargurus.com {year} {make} {model} {trim} for sale` then use `browser` to visit result pages and extract deal ratings and prices.
- **Key data**: Deal rating badge, listed price, estimated market value, days on market, mileage

### AutoTempest (Aggregator)
- **Search URL**: `https://www.autotempest.com/results`
- **Query params**: `make`, `model`, `minyear`, `maxyear`, `minmiles`, `maxmiles`, `minprice`, `maxprice`, `zip`, `radius`, `trim`, `sort`
- **Example**: `https://www.autotempest.com/results?make=toyota&model=camry&minyear=2020&maxyear=2020&maxmiles=50000`
- **Aggregates from**: eBay Motors, Cars.com, TrueCar, Carvana, Cars & Bids, and others
- **Best approach**: Construct URL directly from vehicle details and use `browser navigate` to load results. Extract price range, listing count, and individual listing prices.

### Cars.com
- **Search URL**: `https://www.cars.com/shopping/results/`
- **Best approach**: Use `web-search` skill to search `site:cars.com {year} {make} {model} {trim} for sale` then use `browser` to visit listings.
- **Key data**: Listed price, dealer name, mileage, location

### CarFax
- **Search URL**: `https://www.carfax.com/cars-for-sale`
- **Best approach**: Use `web-search` skill to search `site:carfax.com {year} {make} {model} for sale`.
- **Key data**: Price, history report summary (1-owner, accident-free, service records)

### KBB (Kelley Blue Book)
- **Pricing tool**: `https://www.kbb.com/whats-my-car-worth/` and `https://www.kbb.com/{make}/{model}/{year}/`
- **Best approach**: Use `web-search` skill to search `kbb {year} {make} {model} {trim} price value` to find KBB fair market range, private party value, and trade-in value.
- **Key data**: Fair Purchase Price, Fair Market Range, Private Party Value, Trade-In Value
- **KBB condition definitions**:
  - Excellent: <15% of vehicles qualify, flawless cosmetic/mechanical
  - Very Good: minor cosmetic issues, great mechanical
  - Good: some cosmetic/mechanical wear, most common rating
  - Fair: noticeable issues, needs minor repairs

### Edmunds
- **Pricing tool**: `https://www.edmunds.com/appraisal/` and `https://www.edmunds.com/{make}/{model}/{year}/`
- **Best approach**: Use `web-search` skill to search `edmunds {year} {make} {model} {trim} true market value price` to find TMV pricing.
- **Key data**: True Market Value (TMV), Private Party price, Trade-In value, invoice vs MSRP (new)

## VIN Decoding (Free API)
- **NHTSA vPIC API**: `https://vpic.nhtsa.dot.gov/api/vehicles/DecodeVin/{VIN}?format=json`
- Use to extract year, make, model, trim, engine, body style from a VIN
- Free, no authentication required

## Wholesale/Auction Sources (Dealer Only)

### Manheim MMR (Manheim Market Report)
- Industry-standard wholesale pricing benchmark
- Based on actual auction transaction data
- Not publicly accessible (dealer credentials required)
- Use `web-search` to find recent Manheim MMR references or auction results for specific vehicles

### ADESA CarValue
- Wholesale pricing tool with three metrics: Wholesale Price, Retail Price, Retail-Bid Spread
- Based on 50M+ transaction data points
- Not publicly accessible (dealer credentials required)

### Estimating Wholesale Without Direct Access
When Manheim/ADESA data is unavailable, estimate wholesale value using:
1. KBB Trade-In Value as a baseline (closest public proxy to wholesale)
2. Subtract 5-15% from KBB Trade-In for auction-level wholesale
3. Cross-reference with recent auction results found via web search
4. Check `web-search` for "{year} {make} {model} wholesale value" or "{year} {make} {model} auction price"
