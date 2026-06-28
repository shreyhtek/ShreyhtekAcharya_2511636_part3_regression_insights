# Residual Analysis
## Final Model: Multiple Linear Regression

---

## 1. Predicted vs Actual Sales

Using the full MLR model (R² = 0.8321), predicted and actual sales were compared for all 320 store-month records.

- **Residual = Actual Sales − Predicted Sales**
- **Mean residual:** ≈ ₹0 (expected for OLS regression)
- **Std deviation of residuals:** ≈ ₹42,460

---

## 2. Top 5 Records with Largest Positive Residuals
(Model under-predicted — actual sales were much higher than expected)

| Store ID | Month | Store Type | Region | Actual Sales | Predicted Sales | Residual |
|----------|-------|------------|--------|-------------|-----------------|----------|
| STR-1028 | Apr 2025 | Mall | East | ₹713,611 | ₹600,860 | +₹112,751 |
| STR-1073 | Mar 2025 | Residential | East | ₹813,317 | ₹707,150 | +₹106,167 |
| STR-1019 | Mar 2025 | Residential | East | ₹788,088 | ₹695,490 | +₹92,597 |
| STR-1069 | Apr 2025 | High Street | West | ₹686,738 | ₹595,018 | +₹91,720 |
| STR-1050 | Apr 2025 | Residential | North | ₹735,787 | ₹646,314 | +₹89,472 |

**Business interpretation:** These stores are significantly outperforming what the model predicts. They may have unobserved advantages — strong local management, viral word-of-mouth, unreported promotional activities, or unique catchment areas. These stores should be studied as best-practice examples.

---

## 3. Top 5 Records with Largest Negative Residuals
(Model over-predicted — actual sales were much lower than expected)

| Store ID | Month | Store Type | Region | Actual Sales | Predicted Sales | Residual |
|----------|-------|------------|--------|-------------|-----------------|----------|
| STR-1017 | Mar 2025 | High Street | West | ₹685,379 | ₹844,892 | −₹159,513 |
| STR-1023 | Feb 2025 | Mall | South | ₹627,172 | ₹773,115 | −₹145,943 |
| STR-1012 | Jan 2025 | Residential | West | ₹595,468 | ₹715,299 | −₹119,831 |
| STR-1007 | Feb 2025 | Mall | West | ₹800,452 | ₹913,151 | −₹112,699 |
| STR-1014 | Jan 2025 | High Street | West | ₹463,534 | ₹563,493 | −₹99,959 |

**Business interpretation:** These stores are underperforming relative to what the model expects given their inputs. Possible causes: operational problems, poor local execution, supply chain disruptions, local competition not captured in the data, or data quality issues in the recorded inputs.

Notable: West region stores appear in 3 of the 5 largest negative residuals — this may warrant targeted investigation.

---

## 4. Patterns in Residuals

**Over-predicted (negative residuals):**
- West region stores appear disproportionately — the model may be overestimating the West region premium for certain store types
- High Street stores in West show the worst residuals
- January/February months have more large negative residuals — possible seasonal effect not captured

**Under-predicted (positive residuals):**
- Residential stores in East performing far above expectations in March/April
- Possible spring-season uplift not modelled
- These stores may have specific local demand factors

---

## 5. Model Under/Over-Prediction Patterns

The model tends to **over-predict** West region High Street stores and **under-predict** East region Residential stores performing in Q2. This suggests:

1. The region and store_type dummies may not fully capture local market heterogeneity
2. A seasonal component (month/quarter) should be added to future models
3. Competitor activity data (competitor_distance_km) could improve West region predictions

---

## 6. Residual Distribution Assessment

- Residuals are approximately centred at zero (good sign for OLS)
- Standard deviation of ₹42,460 on a mean sales figure of ₹680,629 = ~6.2% average prediction error
- No evidence of systematic bias across store types as a whole
- Some regional clustering of residuals (West) suggests a potential missing variable

---

## 7. Recommendations Based on Residual Analysis

- Investigate STR-1017, STR-1023, STR-1012, STR-1007, STR-1014 for operational issues
- Study STR-1028, STR-1073, STR-1019 to identify replicable success factors
- Consider adding a `month` or `quarter` variable to the next model iteration
- Explore whether local competitor data or economic indicators explain the West region underperformance
