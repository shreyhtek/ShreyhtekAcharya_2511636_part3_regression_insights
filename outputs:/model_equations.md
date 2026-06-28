# Model Equations
## Part 3: Business Regression Analysis

---

## 1. Simple Regression Equations

### Model 1: Marketing Spend → Monthly Sales
```
monthly_sales = 560,777.35 + 2.1296 × marketing_spend
```
**Coefficient explanation:**
- **Intercept (560,777.35):** Estimated baseline sales when marketing spend = 0. Not practically meaningful on its own.
- **marketing_spend (2.1296):** For every ₹1 increase in marketing spend, monthly sales increase by approximately ₹2.13, holding all else constant.
- **R² = 0.1672** — marketing spend alone explains 16.7% of the variation in monthly sales.
- **P-value < 0.001** — statistically significant.

**Business language:** Spending more on marketing is associated with higher sales, but marketing spend alone is a weak predictor. Other factors play a much larger role.

---

### Model 2: Footfall → Monthly Sales
```
monthly_sales = 446,410.58 + 35.6780 × footfall
```
**Coefficient explanation:**
- **Intercept (446,410.58):** Estimated baseline sales when footfall = 0.
- **footfall (35.6780):** Each additional customer visiting the store is associated with ₹35.68 more in monthly sales.
- **R² = 0.7363** — footfall alone explains 73.6% of the variation in monthly sales.
- **P-value < 0.001** — highly statistically significant.

**Business language:** Store foot traffic is by far the strongest single predictor of monthly sales. Strategies that drive footfall (promotions, location improvements, events) are likely to have the biggest impact on revenue.

---

## 2. Multiple Regression Equation

### Model 3: Full Model (RECOMMENDED)

```
monthly_sales = 49,912.80
              + 1.2004  × marketing_spend
              + 34.0032 × footfall
              − 45,708.55 × avg_discount_pct
              + 3,001.99 × inventory_availability_pct
              + 13,627.39 × customer_rating
              + 41,880.25 × store_Airport
              + 18,092.55 × store_High_Street
              + 29,086.17 × store_Mall
              + 6,184.51  × region_North
              + 18,685.41 × region_South
              + 18,110.86 × region_West
```

---

## 3. Explanation of Each Coefficient

| Variable | Coefficient | P-Value | Meaning |
|----------|-------------|---------|---------|
| Intercept | 49,912.80 | 0.30 (NS) | Baseline when all inputs = 0; not directly interpretable |
| marketing_spend | +1.2004 | < 0.001 *** | Each ₹1 more marketing spend → ₹1.20 more sales |
| footfall | +34.0032 | < 0.001 *** | Each additional visitor → ₹34.00 more sales |
| avg_discount_pct | −45,708.55 | 0.21 (NS) | Not statistically significant in this model |
| inventory_availability_pct | +3,001.99 | < 0.001 *** | Each 1% more inventory availability → ₹3,002 more sales |
| customer_rating | +13,627.39 | 0.005 ** | Each 1-point rating increase → ₹13,627 more sales |
| store_Airport | +41,880.25 | < 0.001 *** | Airport stores earn ₹41,880 more than Residential stores |
| store_High Street | +18,092.55 | 0.003 ** | High Street stores earn ₹18,093 more than Residential |
| store_Mall | +29,086.17 | < 0.001 *** | Mall stores earn ₹29,086 more than Residential |
| region_North | +6,184.51 | 0.38 (NS) | Not significantly different from East region |
| region_South | +18,685.41 | 0.009 ** | South stores earn ₹18,685 more than East region |
| region_West | +18,110.86 | 0.004 ** | West stores earn ₹18,111 more than East region |

*NS = Not Significant | ** p<0.01 | *** p<0.001*

---

## 4. Dummy Variable Explanation

**What are dummy variables?**
Dummy variables convert categorical text values into 0/1 numbers so regression can use them.

### store_type Dummies
- **Reference category: Residential** (dropped to avoid perfect multicollinearity)
- `store_Airport = 1` if the store is an Airport store, else 0
- `store_High Street = 1` if High Street store, else 0
- `store_Mall = 1` if Mall store, else 0
- When all three = 0, the store is Residential (the baseline)

**Why not use all 4 categories?** Including all 4 would create perfect multicollinearity (the "dummy variable trap") — if Airport=0, High Street=0, Mall=0, it's always Residential. We avoid this by dropping one category as the reference.

### region Dummies
- **Reference category: East** (dropped)
- `region_North`, `region_South`, `region_West` = 1 if store is in that region, else 0
- Coefficients show how much each region earns *above or below* the East baseline

---

## 5. Final Model Selected

**Selected Model: Model 3 — Full Multiple Linear Regression**

**Reason for selection:**
- Highest R² (0.8321) and Adjusted R² (0.8261) — explains 83.2% of monthly sales variance
- Includes 9 statistically significant predictors — all actionable
- Provides leadership with multiple levers to improve performance (not just "get more footfall")
- Dummy variables allow store type and region strategy to be quantified
- The improvement from SLR-Footfall (R²=0.74) to MLR (R²=0.83) is meaningful and justified by the additional significant variables

**Model 3 is recommended for business decision-making with the caveat that it shows association, not causation.**
