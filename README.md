**Name**: Muhammad Usman Sohail

**Project Title**: Digitech Offerings AI/ML internship Week 03

**Dataset used**: [House Prices - Advanced Regression Techniques](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/data)

**Top 5 key findings**:
* **Total square footage is the strongest engineered predictor**: `TotalSF`, constructed by summing basement, first-floor, and second-floor areas, correlates with SalePrice at r ≈ 0.78, outperforming every individual floor area column in the raw dataset and confirming that domain-informed feature creation adds measurable signal beyond what the raw data expresses.
* **SalePrice is significantly right-skewed and requires transformation**: the original distribution carries a skewness of 1.88, driven by a small number of luxury properties pulling the upper tail; Box-Cox transformation reduces this to -0.01, making the target variable suitable for linear modelling and substantially improving residual normality.
* **Overall quality has a compounding, non-linear effect on price**: median SalePrice rises steeply and variance widens sharply from quality tier 7 onward, meaning the relationship between quality and price is not linear but accelerating, and a simple coefficient cannot fully capture it without interaction terms or a tree-based model.
* **Kitchen quality is a reliable proxy for whole-home price tier**: despite being a single-room attribute, Excellent-rated kitchens appear almost exclusively in the top price quartile, suggesting buyers treat kitchen quality as a signal of overall renovation standard rather than evaluating it in isolation.
* **Multicollinearity is a significant concern in the raw feature set**: GarageArea and GarageCars share r = 0.88, and TotalSF correlates strongly with both GrLivArea and 1stFlrSF; retaining all three in any linear model would inflate coefficient variance and destabilise predictions, making the multicollinearity removal step in feature selection essential rather than optional.

**Top 3 features engineered**:
1. **`TotalSF`** *(TotalBsmtSF + 1stFlrSF + 2ndFlrSF)*: the single most impactful engineered feature, correlating with SalePrice at r ≈ 0.78 and ranking among the top 2 predictors in the entire feature set. By aggregating all usable square footage into one column it expresses the unit buyers and appraisers actually price against, a relationship that is obscured when floor areas are left as separate columns.

2. **`QualCond`** *(OverallQual × OverallCond)*: captures the multiplicative interaction between build quality and physical condition, two attributes that compound rather than add when determining value. A high-quality, well-maintained home commands a premium that neither column expresses individually, and encoding their product makes this relationship directly available to linear models without requiring them to discover it from data alone.

3. **`TotalBaths`** *(FullBath + 0.5×HalfBath + BsmtFullBath + 0.5×BsmtHalfBath)*: consolidates four separate bathroom count columns into a single weighted metric that reflects the real-estate convention of valuing full bathrooms at twice a half-bath. This reduces dimensionality while preserving the hierarchy, and the resulting feature correlates more strongly with SalePrice than any individual bathroom column does on its own.

**Tools Used**:
| Tool/Library | Version | Purpose |
| ------------ | ------- | ------- |
| Python | 3.12 | Core programming language |
| Pandas | 2.0+ | Data loading, manipulation, feature creation, and get_dummies encoding |
| NumPy | 1.24+ | Numerical transformations, log/sqrt operations, polynomial fitting, and array operations |
| Matplotlib | 3.7+ | Histograms, scatter plots, bar charts, box plots, line charts, and the 6-chart dashboard |
| Seaborn | 0.12+ | Box plots, heatmaps, pair plots, FacetGrid, and statistical visualization |
| Scikit-learn | 1.3+ | StandardScaler, MinMaxScaler, RobustScaler, LabelEncoder, OneHotEncoder, train/test split, and feature selection |
| SciPy | 1.11+ | Box-Cox transformation and Pearson correlation statistics |

**Visualization dashboard**<img width="2379" height="2720" alt="week3_dashboard" src="https://github.com/user-attachments/assets/d5606e55-b1fd-4f90-a837-60cbccb7cd48" />
