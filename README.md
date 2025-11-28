# DSA210 Project-Correlation Analysis: Rising Street Culture Trends vs. Youth Risk Indices in Europe (2004-2024)

## Overview
This project aims to analyze the correlation between the rising popularity of the street culture (proxied by Hip-Hop/Drill music interests, urban fashion interests, TV shows or movies depicting this lifestyle, linguistic habits such as slang adoption, and urban festivals) and changes in the youth risk indices (proxied by youth crime rates, NEET rates, substance abuse, and school exclusions) by focusing on major European economies (UK, France, Germany) by conducting a comparative panel analysis.

First, the street culture trends and youth risk indices will be defined. Street culture in this context contains elements from fashion, music, media, language, and live events. These variables will be assessed as the proxies that show the popularity of the street culture. On the other hand, youth crime rates, NEET (not in education, employment, or training) rates, substance abuse admissions, and school exclusion rates will be the variables that will be assessed as the youth risk indices that are hypothesized to correlate with street culture trends.

The analysis will be conducted to show if there is a significant statistical correlation by data collection of each proxy with an enriched resource basis, EDA to further understand and evaluate the collected data, visualization to depict the data and possible correlation in accordance with the hypothesis, and finally ML model applications for further analysis including socioeconomic controls. This project aims to show an important rising social phenomenon which is affecting all individuals through social media, and make individuals gain insight about this social impact while suggesting predictive work.

## Motivation
In the world we live now, trends diffuse through different generations and regions at a rapid pace, so these diffusing trends are important factors for both the development of individuals and societies. One of the rising trends nowadays is the rising street culture trend as can be seen by the popular culture of newer generations. Therefore, I wanted to work on this critical topic of our generation that affects each individual directly or indirectly, and wanted to analyze if this rising trend correlates with any youth risk indices such as youth crime rates and NEET rates. Since this project outlines a social phenomenon affecting our generation, I defined proxies carefully that possibly alter the correlation the most. By offering predictive insights, this project will be useful for social analysis.

## Plan of the Project

The project will follow a structured Data Science pipeline divided into five key phases:

1.  **Metric Definition & Hypothesis Formulation**
    * **Operationalization:** Define "Street Culture" using five measurable proxies: Music (Drill/Hip-Hop), Fashion (Streetwear), Media (TV/Cinema), Language (Slang), and Events (Festivals).
    * **Risk Metrics:** Define "Youth Risk" using statutory Eurostat metrics: Youth Violent Crime Rates, NEET Rates, Substance Abuse, and School Exclusions.
    * **Hypothesis:** Formulate null and alternative hypotheses focusing on the temporal correlation and potential lag effects between cultural spikes and social risk indicators across the UK, France, and Germany.

2.  **Data Collection**
    * **Culture Data:** Develop Python scripts using `pytrends` to extract monthly Search Volume Indices (SVI) for defined keywords (2004–2024) from Google Search Trends, handling language localization for each country.
    * **Risk Data:** Extract annual socioeconomic and crime datasets from the Eurostat public database, ONS (UK), and National Health services.
    * **Harmonization:** Merge these disparate sources into a single Panel Dataset (Country × Year), resampling monthly culture data to annual means to align with statutory records.

3.  **Data Cleaning & Exploratory Data Analysis (EDA)**
    * **Preprocessing:** Handle missing values (e.g., historical crime data gaps) using linear interpolation and normalize all metrics to a [0,1] scale for direct visual comparison.
    * **Visual Analysis:** Generate Time-Series plots to observe long-term trends and Heatmaps to visualize the intensity of cultural adoption versus risk levels across different regions.

4.  **Hypothesis Testing**
    * **Correlation Analysis:** Conduct Pearson and Spearman correlation tests to evaluate the strength and direction of the relationship between Street Culture and Youth Risk indices.

5.  **Machine Learning & Presentation**
    * **Modeling:** Apply Panel Regression Models to analyze the impact of culture on risk variables while controlling for country-specific heterogeneity (GDP, Inequality, Demographics).
    * **Clustering:** Use K-Means clustering to group years or regions based on "High Risk/High Culture" intensity.
    * **Reporting:** Present findings through a comprehensive report.

## Explanation of the Data

To ensure statistical rigor, this project employs a multi-source enrichment strategy. We combine digital sentiment data (Google Trends) with hard economic & administrative data (Industry Reports, Eurostat, NHS/EUDA) to create a verified Panel Dataset for the UK, France, and Germany (2004–2024).

### 1. Independent Variables: Street Culture Intensity
We quantify "Street Culture" by layering digital curiosity (what people search) with economic consumption (what people buy).

* **Layer A: Digital Interest (The Google Trends Index)**
    * **Source:** Google Trends API (`pytrends`).
    * **Metric:** Normalized Search Volume Index (0-100).
    * **Pillar 1 (Audio):** Interest in "Drill", "Grime", "Deutschrap", "Rap Français".
    * **Pillar 2 (Visual):** Interest in "Streetwear", "Tech Fleece", "Trapstar", "Corteiz".
    * **Pillar 3 (Narrative):** Interest in culture-defining media (e.g., "Top Boy", "Validé").
    * **Pillar 4 (Language):** Interest in slang definitions (e.g., "Roadman meaning", "Talahon").
    * **Pillar 5 (Events):** Interest in urban festivals (e.g., "Wireless Festival").

* **Layer B: Economic Validation**
    * **Source:** Annual Music Industry Reports from **BPI** (UK), **SNEP** (France), and **BVMI** (Germany).
    * **Metric:** Annual Market Share (%) of Hip-Hop/Rap.
    * **Role:** This serves as a verification variable to verify that rising search volumes correlate with actual market dominance and financial consumption.

### 2. Dependent Variables: Youth Risk Indices
We measure youth risk indices using statutory data on Crime, Economic Activity, and Public Health.

* **Metric A: Youth Violent Crime Rate (Legal Risk)**
    * **Source:** **Eurostat** (Table `crim_off_cat`) and **ONS** (UK Crime Survey).
    * **Metric:** Recorded offences for "Robbery" and "Serious Assault" per 100,000 inhabitants.
    * **Role:** Proxies the prevalence of gang-related physical violence.

* **Metric B: NEET Rate (Socioeconomic Risk)**
    * **Source:** **Eurostat** (Table `edat_lfse_20`).
    * **Metric:** Percentage of population aged 15-29 Not in Employment, Education, or Training.
    * **Role:** Proxies social disengagement and the rejection of traditional economic pathways.

* **Metric C: Substance Abuse Admissions (Health Risk)**
    * **Source:** **EUDA** (European Union Drugs Agency) & National Health Services.
    * **Metric:** Drug-induced death rates or hospital admissions for age groups 15-24.
    * **Role:** Adds a biological/health dimension to the "Risk" definition.

* **Metric D: School Exclusion & Suspension Rates (Educational Risk)**
    * **Source:** National Ministry of Education Reports (Department for Education (UK), DEPP (France)).
    * **Metric:** Permanent exclusions and fixed-period suspensions per 1,000 pupils.
    * **Role:** Serves as a "Early Warning" indicator of behavioral deterioration.

### 3. Control Variables (Socioeconomic Context)
To isolate the specific impact of Street Culture on youth risk, we must control for macro-economic factors.

* **Control A: Real GDP per Capita** (Source: Eurostat `sdg_08_10`) - Controls for economic recessions.
* **Control B: Income Inequality (Gini Coefficient)** (Source: Eurostat `tessi190`) - Controls for social stratification.
* **Control C: Youth Population Density** (Source: Eurostat `demo_pjangroup`) - Controls for demographic shifts.

### Data Harmonization
* **Frequency Alignment:** Digital data (Monthly) will be resampled to Annual Means to match the granularity of the "Hard Data" (Industry Reports and Eurostat).
* **Geographic Alignment:** Post-Brexit UK data will be stitched from national sources (ONS/BPI) to maintain continuity with EU datasets.

## Hypothesis
The study focuses on the correlation between observed data rather than implying direct causation.

* **Null Hypothesis ($H_0$):** There is no statistically significant correlation between the rising popularity of Street Culture metrics and the prevalence of Youth Risk Indices (Crime/NEET/Health) in the UK, France, and Germany over the analysis period.
* **Alternative Hypothesis ($H_1$):** There is a statistically significant positive linear correlation (with potential lag effects) between the rising popularity of Street Culture metrics and the prevalence of Youth Risk Indices, even when controlling for socioeconomic factors.

## Steps of The Analysis
To reproduce the data, data_collection.ipynb must be seen. Explanations and comments explain the structure of the data.

To gain more insight about the data and understand the descriptive statistics, eda_visualisation.ipynb must be seen. Visualisation of data and the depiction of the descriptive statistics further explain the data before hypothesis testing. All of the metrics are included and depicted.

To reproduce the hypothesis testing, hypothesis_test.ipynb must be seen. Correlation coefficients and p-values are taken into consideration as H0 is rejected.

## Findings
As can be seen from hypothesis_test.ipynb, all three major economies of Europe UK, Germany and France show a significant correlation between street culture metrics and the youth risk indices which is further proven by the p-values. So as a result of the work that has been done until now, a significant correlation is detected.

## Limitations and Future Work
While the analysis establishes a strong correlation, several limitations must be acknowledged:
1.  **Proxy Limitations:** "Violence with Injury" is a broad category. A more granular dataset specifically for "Knife Crime" across all EU nations would improve precision.
2.  **Imputation:** Due to gaps in European school exclusion data, some years rely on interpolation or cross-country averages, which may smooth out local anomalies.
3.  **Causality vs. Correlation:** While Lag Analysis suggests a "leading indicator" effect, we cannot strictly prove causality without controlling for unobserved variables (e.g., changes in police funding or social media algorithms).

