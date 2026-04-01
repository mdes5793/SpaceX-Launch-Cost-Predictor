# SpaceX Launch Cost Predictor

Predicting whether the Falcon 9 first stage will successfully land — a key factor in estimating launch cost. SpaceX advertises Falcon 9 launches at \$62 million compared to \$165 million+ from other providers, largely because the first stage is reusable. By predicting landing success, we can estimate whether a launch will achieve cost savings through booster recovery.

This project walks through the full data science lifecycle: data collection, wrangling, exploratory analysis, interactive visualization, and machine learning classification.

## Project Structure

| # | Notebook / File | Description |
|---|----------------|-------------|
| 01 | `01-eda-sqllite.ipynb` | Load SpaceX launch data into SQLite and run SQL-based exploratory queries |
| 02 | `02-spacex-data-wrangling.ipynb` | Data wrangling and creation of binary landing outcome labels |
| 03 | `03-spacex-data-webscraping.ipynb` | Scrape Falcon 9 launch records from Wikipedia |
| 04 | `04-spacex-data-collection-api.ipynb` | Collect and enrich launch data via the SpaceX REST API |
| 05 | `05-eda-dataviz.ipynb` | Visual EDA and feature engineering with Matplotlib and Seaborn |
| 06 | `06-launch-site-viz-folium.ipynb` | Interactive launch site maps with Folium |
| 07 | `07-spacex-dash-plotly-app.py` | Interactive Dash/Plotly dashboard for launch records |
| 08 | `08-spacex-ml-prediction.ipynb` | ML pipeline — SVM, Decision Tree, Logistic Regression, KNN with GridSearchCV |

## Data Pipeline

```
SpaceX API / Wikipedia Scraping
        │
        ▼
  dataset_part_1.csv   ← Raw enriched launch data
        │
        ▼
  dataset_part_2.csv   ← Wrangled data with binary Class label
        │
        ▼
  dataset_part_3.csv   ← Feature-engineered (one-hot encoded) for ML
```

Additional datasets:
- `spacex_web_scraped.csv` — output of Wikipedia scraping
- `spacex_launch_dash.csv` — curated dataset for the Dash dashboard

## Tech Stack

| Category | Tools |
|----------|-------|
| Data Collection | `requests`, `BeautifulSoup`, SpaceX API v4 |
| Data Processing | `pandas`, `numpy`, `sqlalchemy`, `sqlite3` |
| Visualization | `matplotlib`, `seaborn`, `plotly`, `folium` |
| Dashboard | `dash` (Plotly Dash) |
| Machine Learning | `scikit-learn` (SVM, Decision Tree, Logistic Regression, KNN) |
| Notebooks | Jupyter / `ipykernel`, `ipython-sql`, `prettytable` |

## Getting Started

### Prerequisites

- Python 3.10+

### Installation

```bash
git clone https://github.com/your-username/SpaceX-Launch-Cost-Predictor.git
cd SpaceX-Launch-Cost-Predictor
pip install -r requirements.txt
```

### Running the Notebooks

Open the notebooks in order (01 through 08) using Jupyter or any compatible IDE:

```bash
jupyter notebook
```

### Running the Dashboard

```bash
python 07-spacex-dash-plotly-app.py
```

The dashboard will start at `http://127.0.0.1:8050` and provides:
- A dropdown to filter by launch site
- A pie chart showing success rates
- A payload range slider
- A scatter plot of payload mass vs. landing outcome, colored by booster version

## Key Findings

- **Launch site matters** — KSC LC-39A has the highest success rate among all sites.
- **Payload mass correlates with outcome** — heavier payloads tend to have different success profiles across booster versions.
- **Landing success has improved over time** — later flights show significantly higher landing success rates as SpaceX iterated on recovery techniques.
- **Best ML model** — classification models are tuned via GridSearchCV; Decision Tree and SVM achieve competitive accuracy on the test set.

## License

This project is for educational purposes.
