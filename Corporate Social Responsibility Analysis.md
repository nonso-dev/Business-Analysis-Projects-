# Corporate Social Responsibility Spending and Beneficiaries: Nigerian Banks
## About  
This dataset contains information on corporate social responsibility (CSR) spending by major Nigerian banks, including Zenith Bank, Guaranty Trust Bank (GT Bank), First Bank of Nigeria, Ecobank Nigeria, Wema Bank, Access Bank, United Bank for Africa (UBA), Diamond Bank, Union Bank of Nigeria, and Fidelity Bank from 2015 to 2023. The dataset tracks quarterly CSR expenditures (Q1, Q2, Q3, and Q4) and the number of beneficiaries impacted by these initiatives over several years.

## Table of Contents
- [Introduction](#introduction)
  - [Brief Overview of The Project](#brief-overview-of-the-project)
  - [Purpose of The Analysis](#purpose-of-the-analysis)
  - [Data Sources](#data-sources)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
  - [Data Loading](#1-data-loading)
  - [Handling Missing Values](#2-handling-missing-values)
  - [Changing Month Abbreviations](#3-changing-month-abbreviations-eg-jan-feb-sep-to-full-month-names)
  - [Splitting the Region Column into Two Separate Columns](#4-splitting-the-region-column-into-two-separate-columns)
  - [Other Useful Data Cleaning Processes](#other-useful-data-cleaning-processes)
- [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
  - [Summary Statistics](#summary-statistics)
  - [Data Visualization](#data-visualization)
  - [Correlations and Relationships](#correlations-and-relationships)
    - [CSR Spending by Region](#1-csr-spending-by-region)
    - [Spending Trends Across Banks](#2-spending-trends-across-banks)
    - [Beneficiaries by Region](#3-beneficiaries-by-region)
    - [Spending Trends Across CSR Areas](#4-spending-trends-across-csr-areas-eg-healthcare-education)
- [Analysis of CSR Spending](#analysis-of-csr-spending)
  - [Total CSR Spending](#total-csr-spending)
  - [Spending by Category](#spending-by-category)
  - [Spending by Bank](#spending-by-bank)
  - [Trends over time](#trends-over-time)
- [Analysis of Beneficiaries](#analysis-of-beneficiaries)
  - [Number of beneficiaries](#number-of-beneficiaries)
  - [Impact of CSR initiatives on beneficiaries](#impact-of-csr-initiatives-on-beneficiaries)
- [Conclusion](#conclusion)
  - [Key Findings](#key-findings)
  - [Limitations of The Analysis](#limitations-of-the-analysis)
  - [Recommendations For Future Research](#recommendations-for-future-research)
  
## Introduction
#### Brief Overview of the Project
This project involves analyzing a large dataset containing corporate social responsibility (CSR) spending data from several leading Nigerian banks. The dataset includes information on CSR activities, including total amounts spent across different months and regions, the number of beneficiaries impacted, and distinctions based on quarterly periods. The analysis focuses on identifying spending patterns, regional distributions of beneficiaries, and seasonal variations in CSR activities to provide valuable insights into the social outreach efforts of these financial institutions.

#### Purpose of the Analysis
The purpose of this analysis is to uncover key insights into the CSR efforts of Nigerian banks by exploring:
- **Spending Patterns**: How CSR expenditures vary across different months, quarters, and regions.
- **Beneficiary Impact**: Analyzing the number of beneficiaries in different regions and understanding the correlation between spending and beneficiaries.
- **Seasonal and Regional Trends**: Detecting peaks in spending during key periods such as holidays and summer months, and identifying which regions receive more CSR efforts.
This analysis aims to help stakeholders understand the social outreach strategies of banks and guide future CSR initiatives to achieve maximum social impact.

#### Data Sources
The dataset used for this analysis is *synthetic* but modelled to reflect realistic CSR spending patterns for 10 major Nigerian banks:
- Zenith Bank
- Guaranty Trust Bank (GT Bank)
- First Bank of Nigeria
- Ecobank Nigeria
- Wema Bank
- Access Bank
- United Bank of Nigeria
- Diamond Bank
- Union Bank of Nigeria
- Fidelity Bank

The dataset includes 50,000 records with the following columns:
- **Bank**: The bank responsible for the CSR expenditure.
- **Month**: The month when the CSR activities occurred.
- **Quarter**: The quarter of the year (Q1, Q2, Q3, Q4).
- **Total_Amount_Spent**: The total amount spent on CSR activities during that period.
- **Beneficiaries**: The number of individuals benefiting from the CSR activities.
- **Region**: The region where the CSR activity took place, categorized into North Central (NC), North East (NE), North West (NW), South West (SW), South East (SE), and South South (SS).
---
## Data Cleaning and Preparation
#### 1. Data Loading
- The CSR dataset is first loaded into Excel using the **Import from Text/CSV** option in the **Data** tab. This process imports the raw dataset for analysis.

---

#### 2. Handling Missing Values
**Step 1**: Identify missing values
- To identify missing values in Excel, use conditional formatting:
  - Select the entire dataset.
  - Navigate to the **Home** tab -> **Conditional Formatting** -> **New Rule**.
  - Choose **Format only cells that contain**, and select **Blanks**.
  - Apply a format (e.g., a light red fill) to highlight missing values.

**Step 2**: Handle missing values
- For columns like `Total_Amount_Spent` or `Beneficiaries`, missing values can be imputed using either the average or median.
  - Formula to calculate the average:
    ```excel
    =IF(ISBLANK(C2), AVERAGE(C:C), C2)
    ```
  - This formula replaces missing values in column C (Total Amount Spent) with the average of the column.
  - Similarly, apply this to other numerical columns like `Beneficiaries`.

---

#### 3. Changing Month Abbreviations (e.g., Jan, Feb, Sep) to Full Month Names

**Step 1**: Create a lookup table
- Create a table with abbreviated months and full month names in two columns (e.g., `E1:F12`):
  - Cell `E1`: `Jan`, Cell `F1`: `January`
  - Cell `E2`: `Feb`, Cell `F2`: `February`
  - Continue for all months.

**Step 2**: Use the `VLOOKUP` function to replace abbreviations
- Formula to convert abbreviated months to full names:
  ```excel
  =VLOOKUP(B2, $E$1:$F$12, 2, FALSE)
  ```
  This formula looks up the abbreviated month in column `B` (e.g., "Jan") and returns the full month name from the lookup table.

**Step 3**: Place the full month names in a new column next to the existing month column.

---

#### 4. Splitting the `Region` Column into Two Separate Columns

**Step 1**: Separate `South` and `(SS)` into two columns
- The `Region` column contains values like `South (SS)`. To split this into two columns:
  - Formula to extract the first part (`South`):
    ```excel
    =LEFT(F2, FIND("(", F2)-2)
    ```
**Step 2**: Changing "South" to "South South"
- Some values may be "South," which we want to change to "South South."
  - Formula to change `South` to `South South`
    ```excel
    =IF(H2="South", "South South", H2)
    ```

---

#### Other Useful Data Cleaning Processes

- **Removing duplicates**: To ensure no duplicate records, select the dataset and go to **Data** -> **Remove Duplicates**.
- **Standardizing case**: Ensure consistent capitalization in the `Bank` and `Region` columns by using:
  ```excel
  =PROPER(A2)
  ```
  This formula converts text to title case (capitalizing the first letter of each word).
- **Handling inconsistent entries**: For any inconsistencies in categorical data (e.g., different spellings of the same bank), use the `Find and Replace` feature (`Ctrl + H`) to standardize the names.

---

## Exploratory Data Analysis (EDA)
#### Summary Statistics

Below is a summary of key statistics for the dataset:

| Statistic              | Value                  |
|------------------------|:------------------------:|
| **Total Rows**         | 50,000                 |
| **Total Columns**      | 6                      |
| **Distinct Banks**     | 10                     |
| **Time Period**        | 12 Months              |

#### CSR Spending (₦)

| Metric              | Value              |
|---------------------|:------------------:|
| **Mean (Average)**  | $32,012.72         |
| **Median**          | $30,824.13         |
| **Minimum Spending**| $5,000.35          |
| **Maximum Spending**| $74,991.07         |
| **Standard Deviation** | $16,731.67        |

#### Beneficiaries by Region

| Region               | Total Beneficiaries | Average Beneficiaries per Bank |
|----------------------|:-------------------:|:------------------------------:|
| **South South (SS)** | 11,874,029          | 756                            |
| **South West (SW)**  | 8,582,222           | 754                            |
| **North Central (NC)** | 2,327,957          | 507                            |
| **North West (NW)**  | 2,332,157           | 506                            |
| **North East (NE)**  | 2,273,751           | 501                            |
| **South East (SE)**  | 4,672,951           | 509                            |

---

#### Key Insights
- **Highest Spending:** **Q3** has the highest spending across all banks, likely due to summer activities.
- **Beneficiaries:** The **South-South** region received the highest number of beneficiaries, followed by **South-West**.
- **Spending Patterns:** The spending fluctuates throughout the year, with peak spending during **Q3** and least at **Q2**.
  
---

## Data Visualization
### Total CSR Spending by Bank

- **Description**: This bar chart compares the total CSR spending across different banks, including Zenith Bank, Guaranty Trust Bank (GT Bank), First Bank of Nigeria, Ecobank Nigeria, and others.
- **Purpose**: To clearly compare the banks’ contributions to CSR efforts. This helps identify which financial institutions are investing the most in CSR initiatives.
- **Key Insight**: The chart reveals that **Diamond Bank** and **Zenith Bank** have the **highest** and **lowest** CSR spending respectively. At the same time, other banks like Fidelity Bank contribute less, highlighting differences in CSR commitment.
- **Image**: ![Bank Total Spend (2)](https://github.com/user-attachments/assets/1814cd98-493b-4020-9b91-6faca52734d0)

---

### Yearly Spending by CSR Area (e.g., Healthcare, Education)

- **Description**: A line chart showing how CSR spending is allocated across different areas such as healthcare, education, community development, and environmental initiatives between 2015 and 2023.
- **Purpose**: To highlight which CSR areas are prioritized by the banks. This allows for understanding of which sectors receive the most support and which are underfunded.
- **Key Insight**: The chart shows that **Financial Literacy**, **Education** and **Healthcare** receive the most funding between **2019** and **2021**, while Environment has the lowest total expenses in recent years, reflecting lower priority for environmental-focused initiatives.
- **Image**: ![CSRSpending  by Area (1)](https://github.com/user-attachments/assets/f64321ab-e2b7-48de-bda9-0c332139ee44)

---

### Quarterly CSR Spending Trends

- **Description**: A bar graph illustrating CSR spending trends across the four quarters (Q1, Q2, Q3, and Q4).
- **Purpose**: To identify seasonal spending patterns, such as increased spending during certain quarters. This helps in understanding how CSR funds are distributed over the year.
- **Key Insight**: The graph shows that **Q3** has the highest CSR spending, possibly due to year-end planning or the culmination of annual projects. Spending drops slightly in Q2.
- **Image**: ![CSRSpending by Quaters](https://github.com/user-attachments/assets/aa925f47-b9ec-4bc4-97bc-2d0be6a769e4)

---

### Yearly CSR Spending Trends

- **Description**: A line chart showing the year-over-year changes in CSR spending, demonstrating trends over multiple years.
- **Purpose**: To analyze how CSR spending has grown or decreased over time. This allows for long-term planning and forecasting of CSR initiatives.
- **Key Insight**: The data reveals a **continuous decrease** in CSR spending from **2020** to **2023**, indicating that banks are gradually reducing their corporate social responsibility efforts.
- **Image**: ![Yearly CSRSpends (1)](https://github.com/user-attachments/assets/26841ad7-c435-4c6a-9260-c21e4761fff8)

---

### Beneficiary Distribution by Region

- **Description**: A pie chart representing the distribution of beneficiaries across different regions such as South-South (SS), South-West (SW), North-West (NW), and others.
- **Purpose**: To show where the majority of CSR beneficiaries are located, which helps assess the regional impact of the banks' CSR efforts.
- **Key Insight**: The data shows that the **South-South (SS)** and **South-West (SW)** regions have the highest number of beneficiaries, aligning with the areas receiving the most CSR funding.
- **Image**: ![Region by Beneficiaries](https://github.com/user-attachments/assets/4e333f9e-4da5-4360-a215-bd21d97cfa61)
  
---

## Correlations and Relationships
#### 1. CSR Spending by Region
- **Relationship:** Spending levels might vary by region, revealing trends in how CSR budgets are geographically allocated.
- **Analysis:** Summarize the total spending per region and compare across all regions to identify patterns in how banks prioritize their CSR activities.
- **Insights:**
  - South-South (SS) receive more CSR funding than other regions, followed by South West (SW).
  - Regions with fewer funds and beneficiaries like North-Central may suggest areas for CSR expansion or greater focus.
  
**Example (PivotTable):**  
Summarize Total_Amount_Spent by Region to visualize spending distribution.

#### 2. Spending Trends Across Banks
- **Relationship:** Compare how different banks (e.g., Zenith Bank, GT Bank) allocate their CSR budgets to reveal trends or priorities.
- **Analysis:** Compare the total CSR spending across all banks to identify which banks are more committed to CSR activities.
- **Insights:**
  - Diamond Bank and Ecobank Bank spend the most on CSR.
  - Zenith Bank spends the least on CSR.

**Example (PivotTable):**  
Summarize Total_Amount_Spent by Bank to analyze spending trends.

#### 3. Beneficiaries by Region
- **Relationship:** Investigating the number of beneficiaries in each region compared to CSR spending can highlight how resources are distributed.
- **Analysis:** Compare the number of beneficiaries with CSR spending. This will help assess if certain regions are receiving adequate attention based on their needs.
- **Insights:**
  - South-South (SS) and South West (SW) have more beneficiaries due to higher CSR spending with **11,874,029** and **8,582,222** beneficiaries respectively.
  - Northern regions have fewer beneficiaries due to fewer funds allocated to them.

**Example (PivotTable):**  
Summarize Total_Amount_Spent and Beneficiaries by Region to analyze spending distributions.

#### 4. Spending Trends Across CSR Areas (e.g., Healthcare, Education)
- **Relationship:** The analysis of spending trends across various Corporate Social Responsibility (CSR) areas, such as healthcare, education, environment, and community development, reveals the distinct patterns and priorities of organizations in their philanthropic efforts. By examining the relationship between spending in these areas, we can identify which sectors receive more funding and how this aligns with broader societal needs. 
- **Analysis:** Compare the total CSR spending across all banks to identify which banks are more committed to CSR activities.
- **Insights:**
  - **Healthcare Dominance**: The healthcare sector often receives one of the highest proportions of CSR spending, indicating a strong focus on public health and wellbeing. For example, during a health crisis, such as the COVID-19 pandemic, there is usually a significant spike in healthcare-related expenditures, overshadowing spending in other areas like education or community development. 
  - **Educational Investments**: Education spending tends to remain consistent with a total of **$323,622,057.15**, highlighting the long-term commitment of organizations to enhance educational opportunities, especially in underserved communities.
  - **Impact of External Factors**: Spending trends are highly responsive to current events and societal needs, with notable increases in areas like healthcare during crises.
  - **Emerging Focus Areas**: There is a growing trend towards environmental and community development initiatives, reflecting a shift in organizational priorities towards sustainability and social equity.

**Example (PivotTable):**  
Summarize Total_Amount_Spent and Beneficiaries by Region to analyze spending distributions.

---

## Analysis of CSR Spending
#### Total CSR Spending
The total Corporate Social Responsibility (CSR) spending across all banks in the dataset reflects the collective commitment of these institutions towards various social causes. The overall CSR expenditure is a key indicator of the philanthropic landscape in the banking sector. For the analyzed period, the total CSR spending amounts to **$1,600,635,907.18**. This figure represents the aggregated financial contributions made by all participating banks to address societal challenges.

#### Spending by Category
CSR spending is categorized into various sectors, such as education, healthcare, community development, and environmental initiatives. The distribution of spending across these categories helps to understand where banks focus their philanthropic efforts. The following breakdown highlights the spending trends by category:

- **Education:** $323,622,057.15
- **Healthcare:** $321,990,235.76
- **Community Development:** $319,483,440.72
- **Environmental Initiatives:** $314,098,010.68
- **Financial Initiative:** $321,442,162.88  
This categorization allows for insights into which areas are prioritized and how they align with the broader needs of society.

#### Spending by Bank
A comparative analysis of CSR spending by individual banks reveals differences in their philanthropic strategies and priorities. Below is the total spending for each bank:

- **Zenith Bank**: $155,298,042.75
- **Guaranty Trust Bank (GT Bank):** $160,818,380.10
- **First Bank of Nigeria:** $161,262,241.80
- **Ecobank Nigeria:** $162,222,058.41
- **Wema Bank:** $158,677,861.21
- **Access Bank:** $159,728,720.21
- **United Bank of Nigeria:** $160,696,463.70
- **Diamond Bank:** $163,623,439.51
- **Union Bank of Nigeria:** $160,190,035.87
- **Fidelity Bank:** $158,118,663.62  
This section illustrates the varying levels of commitment from different banks towards CSR initiatives.

#### Trends Over Time
Analyzing the trends in CSR spending over time provides insights into how philanthropic priorities shift in response to societal needs and external factors. The data reveals notable trends:

- **Increase in Healthcare Spending:** A significant rise in healthcare-related expenditures, particularly during periods of public health crises, indicates a reactive approach to immediate societal challenges.
- **Consistent Education Investments:** Education spending remains steady, reflecting a long-term commitment to improving educational access and quality.
- **Low Environmental Spending:** Environmental initiatives received the lowest total spending among all CSR areas, highlighting that while organizations may recognize sustainability challenges, it is currently not a primary focus in their CSR strategies. There has been a declining trend in Environmental Initiatives with **2023** being the year with its lowest allocation. 

Overall, the trends indicate a dynamic and responsive approach to CSR spending, influenced by internal priorities and external circumstances.

---
## Analysis of Beneficiaries
#### Number of Beneficiaries
The number of beneficiaries impacted by CSR initiatives is a key indicator of the reach and effectiveness of the programs implemented by the banks. Across the dataset, the total number of beneficiaries is **32,063,066**, reflecting the wide range of individuals and communities that have been positively affected by these efforts. Notably, CSR spending tends to correlate with the number of beneficiaries, with higher spending areas, such as healthcare and education, reaching a greater portion of the population.

#### Impact of CSR Initiatives on Beneficiaries
While the dataset is synthetic and does not directly provide detailed information on the specific impacts of CSR initiatives, based on the spending patterns and areas of focus, it can be reasonably perceived that:

- **Healthcare**: CSR spending in healthcare likely contributes to improved access to medical services, particularly in underserved regions, where increased healthcare funding may result in better health outcomes and reduced treatment costs.
- **Education**: Investments in education could be providing scholarships, infrastructure improvements, and learning resources, particularly benefiting students in rural or underserved areas. This would align with the significant spending trends in education.
- **Community Development**: Despite being the lowest in terms of CSR spending, community development initiatives may still provide some benefits, such as access to clean water or improved infrastructure, although at a smaller scale compared to healthcare and education efforts. The lower investment in this area suggests it may not be a primary focus for most banks.

Though the dataset does not explicitly provide outcome data, these insights are inferred from the nature of the CSR areas and their relative spending levels.

---

## Conclusion
#### Key Findings
The analysis of the synthetic Corporate Social Responsibility (CSR) dataset reveals several important trends:

- **Healthcare and Education as Priorities:** A large portion of CSR spending is concentrated in healthcare and education, suggesting that banks are prioritizing these areas as part of their social impact strategies.
- **Regional Focus**: The South-South (SS) and South-West (SW) regions received the most attention in terms of beneficiaries, while other regions, such as the North-East (NE) and North-West (NW), saw comparatively fewer CSR efforts.
- **Q3 Dominates CSR Spending:** The analysis shows that Q3 had the highest overall CSR spending compared to other quarters. This trend may be attributed to increased social programs or community outreach activities during this period, which may align with corporate planning cycles or strategic initiatives leading up to the year-end.
- **More Funds Lead to More Beneficiaries:** There is a clear correlation between higher CSR spending and the number of beneficiaries reached. Areas with higher investments, such as healthcare and education, tend to support a larger number of individuals, indicating that greater financial commitment enables broader outreach.
- **Low Focus on Community Development:** Community development initiatives received the lowest total funding among all CSR areas, indicating that it is not a primary focus for the majority of banks in this dataset.

#### Limitations of the Analysis
Several limitations of this analysis should be noted:

- **Synthetic Data**: Since the dataset is synthetic, the results are purely illustrative and do not reflect real-world data. This limits the applicability of the analysis to actual CSR trends and impacts.
- **Absence of Demographic Data:** There was no available data on age, gender, or specific location in the relevant fields of the dataset. This limitation prevented any detailed analysis of the **Beneficiary Demographics**, such as the age or gender distribution of those impacted by CSR initiatives.
- **Lack of Outcome Data:** The dataset does not include direct measures of the effectiveness or outcomes of CSR spending, such as improved health or educational attainment. The impact assessments are inferred based on spending patterns rather than real beneficiary outcomes.
- **Granularity of Categories:** The CSR areas are broad, which limits the depth of analysis. For example, breaking down healthcare into subcategories like primary care, vaccination programs, or hospital infrastructure could provide more detailed insights.

#### Recommendations for Future Research
Based on the analysis, the following recommendations are suggested for future research:

- **Real-World Data Collection:** To enhance the value of the analysis, future research should involve actual CSR data from financial institutions, including detailed outcomes and impact assessments.
- **More Granular Data**: A more granular breakdown of CSR spending categories would allow for deeper insights into which specific initiatives within education, healthcare, or community development are most effective (e.g., "vaccination programs" under healthcare or "scholarships" under education).
- **Longitudinal Analysis:** Incorporating a time-series analysis over several years could help track shifts in CSR priorities and their long-term effects on communities and beneficiaries.
- **Beneficiary Feedback:** Collecting data directly from beneficiaries about how CSR initiatives have impacted their lives would provide a more comprehensive understanding of the social impact.
- **Inclusion of Demographic Data:** Future datasets should include age, gender, and location information to allow for a more detailed demographic analysis of the beneficiaries and a better understanding of the equity and inclusiveness of CSR programs.

