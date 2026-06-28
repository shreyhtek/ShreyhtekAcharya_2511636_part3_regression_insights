Part 3: Regression Insights — Monthly Sales Drivers


1. Business Problem Summary

A retail chain wants to understand which factors drive monthly sales performance across 80 stores. Leadership is considering actions such as increasing marketing spend, improving inventory, changing discounting strategy, reallocating staff, and prioritising certain store types or regions. The goal is to use regression analysis to identify the most important predictors and provide a data-backed recommendation.


2. Dataset Description

AttributeDetailFiledata/business_regression_data.xlsxRows320 (80 stores × 4 months: Jan–Apr 2025)Columns14Dependent Variablemonthly_salesMissing Valuescompetitor_distance_km (6), customer_rating (8) — imputed with median

Columns:
store_id, month, region, store_type, marketing_spend, footfall, avg_discount_pct, staff_count, inventory_availability_pct, competitor_distance_km, holiday_flag, customer_rating, monthly_sales, monthly_profit


3. Dependent and Independent Variables

Dependent Variable: monthly_sales

Numerical Independent Variables:


marketing_spend
footfall
avg_discount_pct
staff_count
inventory_availability_pct
competitor_distance_km
customer_rating


Categorical Independent Variables:


region (East, North, South, West)
store_type (Residential, High Street, Airport, Mall)
holiday_flag (0/1 binary)


Variables not used in final model:


store_id (identifier, not a predictor)
month (not encoded; no strong linear trend observed)
monthly_profit (derived from sales; would cause leakage)
staff_count (low correlation with sales; not included in final model)



4. Regression Approach

Three models were built:


SLR-1: marketing_spend → monthly_sales (R²=0.167)
SLR-2: footfall → monthly_sales (R²=0.736)
MLR Full: marketing_spend + footfall + avg_discount_pct + inventory_availability_pct + customer_rating + store_type dummies + region dummies → monthly_sales (R²=0.832)


All models use Ordinary Least Squares (OLS) linear regression. Statistical significance evaluated at α = 0.05.


5. Dummy Variable Approach

Dummy variables were created for two categorical fields:

store_type (4 categories → 3 dummies):


Reference category: Residential
Dummies created: store_Airport, store_High Street, store_Mall


region (4 categories → 3 dummies):


Reference category: East
Dummies created: region_North, region_South, region_West


Dropping one category per group prevents perfect multicollinearity (the dummy variable trap). Coefficients represent the difference in monthly sales compared to the reference category, holding all other variables constant.

See analysis/regression_workbook.xlsx Sheet 3 for the full dummy variable table.


6. Model Comparison Summary

ModelR-SquaredAdj R²Significant PredictorsRecommended?SLR-1: Marketing Spend0.1672N/Amarketing_spendNoSLR-2: Footfall0.7363N/AfootfallPartialMLR: Full Model0.83210.82619 variablesYes


7. Final Model Selected

Model 3: Full Multiple Linear Regression

Selected because it has the highest explanatory power (R²=0.8321), the most significant predictors (9 variables at p<0.05), and provides the most actionable business guidance.

Key equation:

monthly_sales = 49,913 + 1.20×marketing_spend + 34.00×footfall
              + 3,002×inventory_availability_pct + 13,627×customer_rating
              + 41,880×store_Airport + 29,086×store_Mall
              + 18,093×store_High_Street + 18,685×region_South
              + 18,111×region_West + ...


8. Business Recommendation

Top priorities for leadership:


Grow footfall — strongest sales driver (₹34/visitor, p<0.001)
Fix inventory gaps — ₹3,002 more sales per 1% improvement (p<0.001)
Invest in marketing — positive ROI at ₹1.20 return per ₹1 spent (p<0.001)
Improve customer ratings — ₹13,627 per 1-point increase (p=0.005)
Prioritise Airport and Mall stores for investment (+₹42K and +₹29K vs Residential)
Do not rely on discounts — avg_discount_pct not significant (p=0.21)


Investigate underperforming stores: STR-1017, STR-1023, STR-1012 have the largest negative residuals and may have operational issues. STR-1028, STR-1073 are outperforming expectations and represent best-practice opportunities.


9. Assumptions and Limitations


Correlation ≠ Causation: The model shows association only. Controlled experiments are needed to confirm causal direction.
Missing variables: 16.8% of variance unexplained — likely seasonal effects, competitor activity, local economic factors.
No seasonal control: Data covers only Jan–Apr 2025; seasonal trends may not be captured.
Missing data imputed: competitor_distance_km and customer_rating missing values filled with median — may introduce small bias.
Individual store residuals up to ₹160K — model is appropriate for strategic guidance, not precise store-level forecasting.
Discount significance may be limited by range — avg_discount_pct may not vary enough across stores to detect a real effect.



10. Screenshots Included

FileContentscreenshots/simple_regression_output.pngSLR-2 (Footfall) output tablescreenshots/multiple_regression_output.pngFull MLR results with coefficients and p-valuesscreenshots/residuals_preview.pngPredicted vs actual with top positive/negative residualsscreenshots/model_comparison_preview.pngSide-by-side model comparison table


