# Deal Analysis Reference

## Retail Deal Evaluation

### Rating Scale
Use this rating scale when presenting deal quality to the user:

| Rating | Criteria |
|--------|----------|
| **Excellent Deal** | 10%+ below market average, clean history, low miles for year |
| **Good Deal** | 5-10% below market average |
| **Fair Deal** | Within 3-5% of market average |
| **Above Market** | 3-10% above market average |
| **Overpriced** | 10%+ above market average |

### Market Average Calculation
To determine market average:
1. Collect 5-15 comparable listings (same year, make, model, similar trim and mileage)
2. Exclude obvious outliers (salvage titles, rebuilt, very high/low mileage anomalies)
3. Calculate median price (more robust than mean for vehicle pricing)
4. Adjust for mileage differences: approximately $0.05-0.15/mile depending on vehicle class
5. Adjust for trim level differences when exact trim matches are limited

### Mileage Adjustment Guidelines
| Vehicle Class | Cost per Mile Above/Below Average |
|--------------|----------------------------------|
| Economy (Civic, Corolla) | $0.05-0.08/mile |
| Mid-size (Camry, Accord) | $0.07-0.10/mile |
| Luxury (BMW 3, Mercedes C) | $0.10-0.15/mile |
| Trucks (F-150, Silverado) | $0.08-0.12/mile |
| SUV (RAV4, CR-V) | $0.07-0.10/mile |
| Premium SUV (X5, GLE) | $0.12-0.18/mile |

### Key Factors Affecting Value
- **1-owner vehicle**: +2-5% value
- **Accident-free**: +3-8% value
- **Full service records**: +2-4% value
- **Salvage/rebuilt title**: -30-50% value
- **Frame damage history**: -40-60% value
- **Flood damage**: -50-70% value
- **Remaining factory warranty**: +3-7% value
- **Popular color (white, black, silver)**: +1-3% value

## Dealer Wholesale Buy Price Analysis

### Dealer Cost Structure
A dealer reselling a vehicle has these costs:
1. **Acquisition cost** (what they pay for the vehicle)
2. **Reconditioning**: $500-$2,500 (inspection, repairs, detail, photos)
3. **Pack fee**: $200-$500 (overhead allocation per unit)
4. **Floorplan interest**: $100-$300/month (financing cost of holding inventory)
5. **Advertising**: $200-$500 per vehicle
6. **Target front-end gross profit**: $1,500-$3,500

### Dealer Buy Price Formula
```
Max Dealer Buy Price = Expected Retail Price - Reconditioning - Pack - Profit Target - Risk Buffer

Typical breakdown:
  Expected Retail Price (market average from comparables)
- Reconditioning:     $800 - $2,000
- Pack fee:           $300 - $500
- Target profit:      $1,500 - $3,000
- Risk/holding cost:  $300 - $800
= Max Buy Price
```

### Reconditioning Cost Estimates by Vehicle Age
| Age | Typical Recon Cost |
|-----|-------------------|
| 0-3 years | $500-$1,000 |
| 4-7 years | $1,000-$1,800 |
| 8-12 years | $1,500-$2,500 |
| 13+ years | $2,000-$3,500+ |

### Quick Wholesale Estimate
When detailed analysis is not possible:
- **Rough wholesale** = 70-80% of average retail listing price
- **Rough dealer buy** = 60-75% of average retail listing price
- Higher-demand vehicles (trucks, popular SUVs) closer to 80%
- Lower-demand vehicles (sedans, luxury) closer to 65-70%

### Profit Margin Context for Users
- **Franchise dealers**: Target $1,500-$3,500 front-end gross, higher on trucks/SUVs
- **Independent dealers**: Target $2,000-$5,000 gross, higher risk tolerance
- **Wholesale flippers**: Target $500-$1,500 per unit, volume-based
- **Auction-to-retail**: Most dealers want minimum $2,000 spread after all costs

## Output Template

### Consumer Deal Report
```
## Vehicle Pricing Analysis: {Year} {Make} {Model} {Trim}

### Target Vehicle
- **Year/Make/Model**: {details}
- **Trim**: {trim}
- **Mileage**: {mileage}
- **Listed Price**: {price} (if provided)

### Market Comparison
- **Listings found**: {count} comparable vehicles
- **Price range**: ${low} - ${high}
- **Market average**: ${median}
- **Sources checked**: {list of platforms}

### Deal Rating: {RATING}
{Explanation of how listed price compares to market, with percentage above/below}

### What Would Be a Good Deal
- **Great deal**: Below ${X}
- **Good deal**: ${X} - ${Y}
- **Fair deal**: ${Y} - ${Z}

### Key Considerations
- {Relevant factors: mileage, history, market trends, seasonal factors}

### NHTSA Recalls
- {List any open recalls, or "No open recalls found"}

### Market Supply
- **Supply level**: {Flooded/High/Normal/Low/Scarce} ({count} listings found nationally)
- **Negotiation leverage**: {High/Moderate/Low}
- {Context on what supply level means for this purchase}

### Seasonal Timing
- {Current seasonal impact on this vehicle type, if applicable}
- {Recommendation: buy now vs wait}

### Depreciation Forecast
- **Current value**: ${amount}
- **6-month projected value**: ${amount} ({percent}% loss)
- **1-year projected value**: ${amount} ({percent}% loss)
- **2-year projected value**: ${amount} ({percent}% loss)

### Estimated Annual Cost of Ownership
- **Depreciation**: ${amount}/year
- **Insurance**: ${amount}/year (estimate)
- **Fuel**: ${amount}/year ({mpg} MPG, {annual_miles} miles/year)
- **Maintenance**: ${amount}/year
- **Total annual cost**: ${amount}/year
- **Cost per mile**: ${amount}
```

### Dealer Buy Report
```
## Dealer Wholesale Analysis: {Year} {Make} {Model} {Trim}

### Estimated Market Values
- **Average retail listing**: ${amount}
- **KBB Trade-In Value**: ${amount} (if found)
- **Estimated wholesale/auction**: ${amount}

### Recommended Dealer Buy Price
- **Maximum buy price**: ${amount}
- **Target buy price**: ${amount}
- **Walk-away price**: ${amount} (minimum margin threshold)

### Cost Breakdown
- Expected retail:     ${amount}
- Reconditioning:     -${amount}
- Pack/overhead:      -${amount}
- Target profit:      -${amount}
- Risk buffer:        -${amount}
- = Max buy price:    ${amount}

### Profit Potential
- **Best case** (sell at market avg): ${amount} gross
- **Realistic** (sell 5% below avg): ${amount} gross
- **Worst case** (sell 10% below avg): ${amount} gross
```
