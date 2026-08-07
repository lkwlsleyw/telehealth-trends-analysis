# Telehealth Trends Analysis

This project examines how telehealth usage in the United States changed across time, geographic location, and age groups. We worked with Medicare telehealth records from 2020–2024 together with a second federal telemedicine survey dataset to explore patterns in adoption and accessibility.

The project combines Python-based data cleaning and exploratory analysis with SQL queries, data visualization, and statistical testing. The analysis focuses on three questions: how telehealth use changed after the COVID-19 surge, whether usage differs between rural and urban areas and across states, and how telehealth usage varies by age.

This was a three-person collaborative project completed for CPSC 368 at the University of British Columbia.

## Research Questions

1. **How has telehealth use changed over time?**  
   Specifically, is there a significant difference in the average percentage of telehealth users between the years 2020–2024?

   Dataset: `medicare_telehealth_cleaned`

2. **Is there a significant difference in the average number of telehealth visits between rural and urban areas? How does usage vary across states?**

   Datasets:
   - `medicare_telehealth_cleaned`
   - `telemedicine_by_state`

3. **Is there a significant difference in the frequency of telehealth use across different age groups? Are younger beneficiaries more likely to use telehealth than older ones?**

   Datasets:
   - `medicare_telehealth_cleaned`
   - `telemedicine_by_age`

## Data

The project uses two main datasets.

### Medicare Telehealth Trends

The Medicare Telehealth Trends dataset contains information on Medicare beneficiaries who used telehealth services between 2020 and 2024. The data includes breakdowns by year, quarter, geographic location, rural/urban classification, age, race, and sex.

This dataset is used primarily to examine:

- telehealth usage over time
- rural and urban differences
- telehealth usage across Medicare age groups

### Telemedicine Use in the Last 4 Weeks

The second dataset provides survey-based estimates of telemedicine usage among U.S. adults. For this project, the data was separated into several subsets, including:

- national estimates
- age groups
- state-level estimates

These data provide an additional perspective beyond the Medicare population and are used mainly for the state-level and age-group analyses.

## Data Preparation

The raw datasets were cleaned and prepared in `dataCleaning.ipynb`.

The preprocessing workflow includes:

- removing variables not needed for the research questions
- handling missing observations
- separating the telemedicine survey data into national, age, and state datasets
- exporting cleaned CSV files
- preparing SQL-compatible versions of the datasets for use in Oracle SQL Plus

The cleaned Medicare dataset contains more than 23,000 observations and is used throughout the exploratory and statistical analysis.

## Analysis

The analysis was carried out using a combination of SQL and Python.

SQL queries were used to aggregate telehealth usage by year, geographic category, state, and age group. Python was used for additional data exploration, visualization, and statistical testing.

For the rural-versus-urban comparison, an independent two-sample Welch's t-test was used to compare average telehealth visit counts.

For the age-group analysis, one-way ANOVA was used to test whether telehealth usage differed across age categories in both datasets.

Exploratory visualizations were also created to examine distributions, yearly trends, geographic differences, and age-group patterns.

## Key Findings

### Telehealth usage over time

The Medicare analysis showed a substantial decline in average telehealth usage after the initial pandemic period. Average usage decreased from approximately **32.4% in 2020 to 13.0% in 2024**.

This pattern suggests that the rapid adoption of telehealth during the COVID-19 period was followed by a gradual decline in subsequent years.

### Rural and urban differences

The analysis found a large difference in average telehealth visit counts between rural and urban observations.

- Rural: approximately **60,346** average telehealth visits
- Urban: approximately **288,016** average telehealth visits

A Welch's two-sample t-test produced a p-value well below 0.05, indicating a statistically significant difference in the visit counts between the two groups.

State-level analysis also showed considerable variation in telemedicine usage. Among the states and jurisdictions examined, the District of Columbia had one of the highest average usage rates, while North Dakota had one of the lowest.

### Age-group differences

The two datasets showed different patterns across age groups.

Within the Medicare data, beneficiaries aged **0–64** had the highest average telehealth usage rate among the Medicare age categories examined.

In the broader survey dataset, usage generally increased with age, with adults aged **80 and above** showing the highest average rate.

One-way ANOVA results indicated significant differences across age groups in both datasets. The contrast between the two datasets also highlights the importance of population composition and data collection methods when interpreting telehealth usage.

## Technologies

- Python
- SQL
- Oracle SQL Plus
- Jupyter Notebook
- pandas
- Matplotlib
- Seaborn
- SciPy

## Project Files

| Filename/Folder | Description |
|---|---|
| `data/Medicare_Telehealth_Trends_Q2_2024.csv` | Original Medicare telehealth trends dataset |
| `data/Telemedicine_Use_in_the_Last_4_Weeks.csv` | Original survey-based telemedicine dataset |
| `data/medicare_cleaned.csv` | Cleaned Medicare dataset used in the analysis |
| `data/telemedicine_cleaned.csv` | Cleaned telemedicine survey dataset |
| `data/telemedicine_group_By_Age.csv` | Telemedicine data grouped by age |
| `data/telemedicine_group_By_State.csv` | Telemedicine data grouped by state |
| `data/telemedicine_group_National_Estimate.csv` | National-level telemedicine estimates |
| `dataCleaning.ipynb` | Data preprocessing, cleaning, dataset splitting, and SQL preparation |
| `EDAcode.ipynb` | Exploratory data analysis, statistical testing, and visualizations |
| `SQLqueries.ipynb` | SQL queries corresponding to the three research questions |
| `sqlFile/medicare_cleaned.sql` | Oracle SQL script for the cleaned Medicare dataset |
| `sqlFile/telemedicine_groups.sql` | Oracle SQL script for the telemedicine datasets |
| `telehealth_trends_analysis_report.pdf` | Full project report including methodology, results, discussion, and limitations |
| `README.md` | Project overview and documentation |

## Limitations

The two datasets represent different populations and should not be interpreted as directly equivalent.

The Medicare dataset primarily represents older adults and people who qualify for Medicare through disability or other eligibility criteria, so results may not generalize to the entire U.S. population.

The survey dataset covers a broader population but relies on self-reported telemedicine usage. The datasets also cover different time periods and use different measurement approaches.

In addition, some analyses use aggregated observations, which may hide variation within states, time periods, or demographic groups. The rural-versus-urban comparison is based on total telehealth visit counts and does not by itself account for differences in population size or other potential confounding factors.

## How to Run

### Python Analysis

The Python notebooks can be run locally using Jupyter Notebook or JupyterLab.

Required Python packages include:

- pandas
- matplotlib
- seaborn
- scipy

Run the notebooks in the following order:

1. `dataCleaning.ipynb`  
   Cleans the original datasets, creates the analysis-ready CSV files, and separates the telemedicine survey data into the subsets used in the project.

2. `EDAcode.ipynb`  
   Performs the exploratory data analysis, visualizations, and statistical tests.

The raw datasets are already included in the `data/` directory, so the notebooks can be run using the repository's existing folder structure.

### SQL Analysis

The SQL portion of the project was originally run using Oracle SQL Plus through the UBC computing environment.

The Oracle-compatible scripts used to create and populate the database tables are located in:

- `sqlFile/medicare_cleaned.sql`
- `sqlFile/telemedicine_groups.sql`

In the original course environment, the workflow was:

1. Connect to `remote.students.cs.ubc.ca` through SSH using a UBC CWL account.
2. Upload the two SQL files from the `sqlFile/` directory.
3. Log in to Oracle SQL Plus.
4. Run the SQL scripts to create and populate the tables.
5. Execute the queries documented in `SQLqueries.ipynb`.

`SQLqueries.ipynb` is used to organize the SQL queries for the three research questions rather than as a directly executable Python notebook.

## Full Report

The complete methodology, analysis, results, discussion, and references are available in:

[Telehealth Trends Analysis Report](telehealth_trends_analysis_report.pdf)

## Collaboration

This project was completed collaboratively by:

- Heather Lu
- Kaiwei Liu
- Shenglong Chen

The original Git commit history has been preserved in this repository to reflect each contributor's work.
2. Upload 2 files in `sqlFile` folder to your SQL plus server.
3. Login in your account to the SQL plus server.
4. Query according to the SQL query command in the file `SQLqueries.ipynb`.
