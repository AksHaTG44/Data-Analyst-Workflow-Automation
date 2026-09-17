# Data Analyst Workflow Automation

An end-to-end data analytics workflow that collects job-market and developer-survey data from multiple sources, cleans and normalizes it, and analyzes it to identify which programming languages, databases, and development tools are most in demand.


---

## Problem Statement

A global IT and business consulting firm needs to anticipate future skill requirements to stay competitive and to advise clients on hiring and training. The organization requires a data-driven answer to three questions:

1. Which programming languages are currently most in demand?
2. Which database technologies are most in demand?
3. Which IDEs and development tools are most widely used?

The challenge is that no single source answers these questions. Relevant signals are scattered across job postings, developer surveys, and training-portal content, in different formats (REST API responses, HTML pages, Excel files, CSV files, and a relational database). The work below consolidates those sources into a single analyzable dataset and extracts the trends from it.

---

## Data Sources

| Source | Format | Collection method |
| --- | --- | --- |
| Jobs API (job postings by location and technology) | JSON over REST | `requests` against a Flask-served Jobs API |
| Programming language salary table | HTML | Web scraping with BeautifulSoup |
| Stack Overflow Developer Survey (worldwide respondents) | CSV | Direct load from IBM Cloud Object Storage |
| Survey data for visualization module | SQLite database | SQL queries via `sqlite3` |

---

## Workflow

**1. Data Collection**
Job-posting counts were retrieved from a REST API and written to Excel. A programming-language salary table was scraped from an HTML page and exported to CSV. The developer survey dataset was loaded directly from cloud storage.

**2. Data Wrangling**
Duplicate records were identified and removed. Missing values were quantified column by column; categorical gaps such as `WorkLoc` were imputed with the modal value. Compensation fields were normalized to a single annual basis so that respondents reporting weekly, monthly, and yearly pay could be compared directly.

**3. Exploratory Data Analysis**
Distributions were examined for compensation and age, including median compensation overall and by respondent group. Outliers were detected using the interquartile-range method and removed. A correlation matrix was used to assess relationships between numeric features such as age, work week hours, and converted compensation.

**4. Data Visualization**
The cleaned data was queried from a SQLite database with SQL and visualized to show distribution (histograms, box plots), relationship (scatter and bubble plots), composition (stacked charts, pie charts), and comparison (bar and line charts) across demographic and technology dimensions.

---


## Tech Stack

- **Language:** Python 3
- **Data manipulation:** pandas, NumPy
- **Data collection:** requests (REST APIs), BeautifulSoup + html5lib (web scraping)
- **Database:** SQLite, SQL (`sqlite3`, `pandas.read_sql_query`)
- **Visualization:** Matplotlib, Seaborn
- **File formats:** Excel (openpyxl), CSV, JSON, SQLite
- **Environment:** Jupyter Notebook

---

## Repository Structure

```
.
├── Collecting_Jobs_data_Using_API-Questions(2).ipynb   # API data collection
├── Web-Scraping-Lab(1).ipynb                           # HTML scraping to CSV
├── M1ExploreDataSet-lab(1).ipynb                       # Initial dataset exploration
├── M2DataWrangling-lab(1).ipynb                         # Deduplication, imputation, normalization
├── M3ExploratoryDataAnalysis-lab(1).ipynb               # Distributions, outliers, correlation
├── M4DataVisualization-lab(1).ipynb                     # SQL queries and visualizations
├── job-postings(1).xlsx                                 # API output: postings by technology
├── job-postings2.xlsx                                   # API output: postings by location
└── popular-languages.csv                                # Scraped language salary data
```

---

## Running the Project

```bash
git clone https://github.com/AksHaTG44/Data-Analyst-Workflow-Automation.git
cd Data-Analyst-Workflow-Automation

python3 -m venv venv
source venv/bin/activate          # Windows: venv\Scripts\activate

pip install pandas numpy requests beautifulsoup4 html5lib openpyxl matplotlib seaborn jupyter

jupyter notebook
```

Run the notebooks in order: API collection → web scraping → M1 → M2 → M3 → M4. The survey datasets are fetched from remote URLs at runtime, so an internet connection is required. The Jobs API notebook depends on a locally running Flask API provided by the course environment.

---


---

## Author

**Akshat Goyal** — B.E. Computer Engineering, Thapar Institute of Engineering and Technology, Patiala

- GitHub: [AksHaTG44](https://github.com/AksHaTG44)
- LinkedIn: [akshatgoyal44](https://linkedin.com/in/akshatgoyal44)
