# Model Comparison
## Part 3: Business Regression Analysis — Monthly Sales Drivers

---

## Models Compared

### Model 1: Simple Linear Regression — Marketing Spend
- **Dependent Variable:** monthly_sales
- **Independent Variable:** marketing_spend
- **R-Squared:** 0.1672
- **Coefficient:** 2.1296 (each ₹1 more spend → ₹2.13 more sales)
- **P-Value:** < 0.001 (significant)
- **Significant Variables:** marketing_spend
- **Business Usefulness:** Provides a weak baseline — marketing spend matters but alone explains only 16.7% of sales variance. Other factors dominate.
- **Limitations:** Ignores footfall, store type, region, and other critical variables. Risk of omitted variable bias.

---

### Model 2: Simple Linear Regression — Footfall
- **Dependent Variable:** monthly_sales
- **Independent Variable:** footfall
- **R-Squared:** 0.7363
- **Coefficient:** 35.6780 (each additional visitor → ₹35.68 more sales)
- **P-Value:** < 0.001 (highly significant)
- **Significant Variables:** footfall
- **Business Usefulness:** Excellent single predictor — explains 73.6% of variance. Footfall is clearly the dominant driver of monthly sales.
- **Limitations:** Still ignores store type, region, investment levers, and discount effects. Cannot guide marketing or operations decisions beyond "get more visitors."

---

### Model 3: Multiple Linear Regression — Full Model ✅ (RECOMMENDED)
- **Dependent Variable:** monthly_sales
- **Independent Variables:** marketing_spend, footfall, avg_discount_pct, inventory_availability_pct, customer_rating, store_type (dummy), region (dummy)
- **R-Squared:** 0.8321
- **Adjusted R-Squared:** 0.8261
- **Significant Variables:**
  - footfall (p < 0.001) ★★★
  - marketing_spend (p < 0.001) ★★★
  - inventory_availability_pct (p < 0.001) ★★★
  - store_Airport (p < 0.001) ★★★
  - store_Mall (p < 0.001) ★★★
  - customer_rating (p = 0.0046) ★★
  - store_High Street (p = 0.0027) ★★
  - region_South (p = 0.0093) ★★
  - region_West (p = 0.0040) ★★
- **Not Significant:** avg_discount_pct (p = 0.21), region_North (p = 0.38)
- **Business Usefulness:** Highest explanatory power and most actionable. Leadership can use this model to prioritize footfall growth, marketing investment, inventory, customer experience, and store type strategy simultaneously.
- **Limitations:** Regression shows association, not causation. Does not account for seasonal trends, competitor activity, economic conditions, or non-linear relationships. Residual standard deviation of ~₹42,460 means predictions can still be off significantly for individual stores.

---

## Comparison Table

| Criterion | Model 1 (Marketing SLR) | Model 2 (Footfall SLR) | Model 3 (Full MLR) |
|-----------|------------------------|------------------------|---------------------|
| R-Squared | 0.1672 | 0.7363 | **0.8321** |
| Adj R² | N/A | N/A | **0.8261** |
| Significant vars | 1 | 1 | 9 |
| Variables used | 1 | 1 | 11 |
| Actionability | Low | Medium | **High** |
| Recommended | No | Partial | **Yes** |

---

## Winner: Model 3 — Full Multiple Regression

The full MLR model explains 83.2% of variance in monthly sales. It identifies multiple levers leadership can actually act on: increase marketing spend, improve inventory availability, grow footfall, improve customer ratings, and prioritize high-performing store types (Airport > Mall > High Street > Residential) and regions (South, West outperform East).

See `outputs/regression_summary.xlsx` for the full comparison table.
