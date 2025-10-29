**Stage 1: Project Brief - A/B Test Analysis**

> **Note**: The problem definition and business context presented in this stage are hypothetical and were created specifically to practice professional data analysis workflows and A/B testing methodologies.

**1. Business Problem & Objective**
🎯 **Problem**: The marketing team wants to improve the click-through rate (CTR) of their email campaigns. They are unsure if a new, more direct subject line will perform better than the current one.

**Objective**: To statistically determine if the new email subject line ("Version B") results in a significantly higher click-through rate compared to the original subject line ("Version A"). The analysis will provide a clear, data-driven recommendation on which version to use for all future campaigns.

**2. Key Questions to Answer** 🔍
- What is the click-through rate for the control group (Version A)?
- What is the click-through rate for the test group (Version B)?
- Is the observed difference in click-through rates statistically significant, or could it be due to random chance?
- Based on the results, which email subject line should the company adopt?

**3. Data Source** 📂
- **Source**: A public A/B testing dataset from a source like Kaggle. This typically comes as a single CSV file.
- **Data Structure**: The dataset will contain one row per user who received the email. Key columns will include:
  - `user_id`: A unique identifier for each user
  - `group`: Which version the user saw ('control' for A, 'treatment' for B)
  - `converted` (or clicked): A binary indicator (0 or 1) showing whether the user clicked the link in the email

**4. Key Metrics & Methodology** 📊
- **Primary Metric**: Click-Through Rate (CTR)
  - Formula: `CTR = (Total Number of Clicks / Total Number of Users in Group) * 100`
- **Statistical Methodology**: Chi-Squared Test for Independence (chi2_contingency from the scipy.stats library). This is the appropriate statistical test to compare the proportions of two different groups.
- **Significance Level (Alpha)**: α = 0.05 (5% chance of incorrectly concluding that there is a difference when there isn't one)

**Hypotheses**:
- **Null Hypothesis (H₀)**: There is no significant difference in the click-through rate between Version A and Version B
- **Alternative Hypothesis (H₁)**: There is a significant difference in the click-through rate between Version A and Version B

---

**Stage 2: Data Retrieval (Query)**

Data was downloaded from "AB testing on Ecommerce" Kaggle dataset in the form of "ab_data.csv". Raw data was saved to folder `data/00_raw/` as `raw_ab_data.csv` and loaded into notebooks for analysis.

**Dataset Overview**:
- Total records: 294,482 user interactions
- Columns: user_id, timestamp, group, landing_page, converted
- Data quality: No missing values, no duplicates, clean categorical data entries

---

**Stage 3: Data Cleaning & Preparation (Wrangle)**

**Combined Initial Inspection & Data Cleaning (01_initial_inspection_and_data_cleaning.ipynb)**:
- ✅ **Data Quality Assessment**: No errors in formatting and data entry
- ✅ **Missing Values**: No missing values detected
- ✅ **Duplicates**: No duplicate rows found
- ✅ **Categorical Data**: Consistent entries for 'group', 'landing_page', and 'converted' columns
- ⚠️ **Data Types**: Timestamp column needs formatting (currently in MM:SS.s format)
- **Timestamp Conversion**: Converted timestamp from MM:SS.s format to proper time format using `pd.to_datetime('00:' + timestamp, format='%H:%M:%S.%f').dt.time`
- **Data Validation**: Confirmed data types and format after cleaning
- **Export**: Saved cleaned dataset to `data/01_cleaned/cleaned_ab_data.csv`

---

**Stage 4: Analysis & Insight Generation (Analyze)**

**Comprehensive A/B Testing Analysis (02_analysis_and_visualization.ipynb)**:

**Conversion Rate Analysis**:
- Calculated conversion rates for both control and treatment groups
- Computed confidence intervals using `proportion_confint`

**Statistical Testing**:
- Performed Chi-Squared Test for Independence using `chi2_contingency`
- Created contingency table for conversions vs non-conversions by group
- Applied α = 0.05 significance level

**Data Visualization** (5 key visualizations saved to `outputs/visualizations/`):
- **Main Conversion Rate Comparison**: Bar chart with confidence intervals showing core A/B test results
- **Conversion Funnel**: Visual comparison of total users vs conversions for both groups
- **Statistical Test Results**: Chi-squared test visualization and significance interpretation
- **Complete Dashboard**: Executive summary with all key metrics in one comprehensive view
- **Visualization Summary Report**: Automated summary of all generated visualizations

**Hypothesis Testing**:
- Systematic evaluation of null vs alternative hypotheses
- Clear interpretation of p-value and statistical significance
- Data-driven recommendations based on results

---

**Stage 5: Reporting & Communication (Report)**

**Final Report Generation**:
- **Comprehensive Analysis Report**: Created detailed report in `outputs/REPORT.md`
  - Executive summary of findings and recommendations
  - Detailed statistical results and interpretation
  - Business implications and next steps
  - Visual presentation of key metrics and insights

**Visual Documentation**: 
- **High-Quality Visualizations**: 5 professional charts saved to `outputs/visualizations/`
- **Publication-Ready**: All charts saved in 300 DPI PNG format for reports and presentations

**Excel Dashboard Deliverable**:
- **Interactive Excel File**: `AB_Test_Analysis.xlsx` created and saved in `outputs/` folder
  - **Cleaned Data Sheet**: Complete processed dataset with proper formatting
  - **Analysis Summary**: Statistical test results and conversion metrics
  - **Executive Dashboard**: Stakeholder-ready summary featuring:
    - Conversion rate summary table (Control: 12.04%, Treatment: 11.89%)
    - Statistical significance results (p-value: 0.2177)
    - Clear business recommendation (Maintain current design)
    - Key performance indicators and sample size information
  - **Business Communication**: Designed for easy interpretation by non-technical stakeholders