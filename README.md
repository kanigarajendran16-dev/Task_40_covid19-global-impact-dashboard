# 🦠 COVID-19 Global Impact Dashboard

> **Did faster vaccination rollouts lead to a bigger drop in COVID-19 deaths?**
> An end-to-end analytics project: cleaning messy real-world time-series data, engineering new metrics, and presenting findings in an interactive dashboard.

Built as part of my **Veda Technology** data analytics internship (Day 40 project).

---

## 🔗 Quick Links

| Item | Link |
|---|---|
| 📓 Google Colab Notebook | `PASTE_YOUR_COLAB_LINK_HERE` |
| 📊 Interactive Dashboard (HTML) | [`dashboard/covid_dashboard.html`](dashboard/covid_dashboard.html) |
| 📄 Executive Summary (1-page PDF) | [`reports/executive_summary.pdf`](reports/executive_summary.pdf) |

---

## 🎯 Objective

Analyse publicly available COVID-19 data (cases, deaths, vaccinations by country and date) to find out whether countries that vaccinated their population faster saw a bigger fall in deaths, and present the results so that a **non-technical viewer** can compare countries and time periods at a glance.

---

## 💡 What makes this project different

Instead of a generic cases-and-deaths dashboard, this project answers **one focused question** using custom metrics:

| Custom metric | Definition |
|---|---|
| **Rollout Speed** | Percentage points of population vaccinated per day, between 1% and 30% first-dose coverage |
| **Death Change %** | Avg deaths per million in the 90 days *after* reaching 30% vs the 90 days *before* rollout started |
| **Resilience Index (0-100)** | Own score: 40% rollout speed + 40% death drop + 20% low peak deaths |

---

## 🧰 Tools & Libraries

- **Python**: Pandas, NumPy
- **Visualisation**: Plotly (interactive), Matplotlib (PDF report)
- **Environment**: Google Colab
- **Data source**: [Our World in Data - COVID-19 dataset](https://ourworldindata.org/covid-cases)

---

## 🔄 Analytics Pipeline

1. **Load**: download the OWID dataset (with a manual-upload fallback)
2. **Clean**: remove aggregate rows (World, continents, income groups), drop countries below 1M population, forward-fill cumulative columns, set missing daily values to 0, clip negative data corrections
3. **Engineer metrics**: 7-day rolling averages, cases/deaths per million, case fatality rate (CFR), doubling time
4. **Analyse**: rollout speed vs death change, rank correlation, Resilience Index
5. **Visualise**: 3 interactive charts combined into one HTML dashboard
6. **Communicate**: auto-generated insights and a 1-page executive summary PDF

---

## 📋 Cleaning Assumptions (documented)

| # | Assumption |
|---|---|
| A1 | Aggregates (World, Asia, EU, income groups) are removed so only real countries are compared |
| A2 | Missing continent/population values are filled within each country |
| A3 | Only countries with population > 1 million are kept (small populations give noisy per-million values) |
| A4 | Cumulative columns are forward-filled; missing daily values = 0; negative daily values (reporting corrections) = 0 |
| A5 | Missing vaccination % before a country's rollout began = 0% |
| A6 | Case fatality rate is calculated only after 100 total cases and capped at 20% to avoid early-outbreak spikes |
| A7 | Death change % is clipped to the range -100% to +300% to stop extreme outliers dominating the correlation |

---

## 📊 Dashboard Features

- **Country comparison**: pick a metric (cases/million, deaths/million, CFR, doubling time) from a dropdown, click legend items to show/hide countries, and drag the range slider to zoom into any time period
- **Speed vs deaths scatter**: bubble size = population, colour = continent, with trend line and hover details
- **Resilience Index ranking**: best 12 vs lowest 12 countries

---

## 🔍 Key Insights

> ⚠️ *Replace these with the real numbers printed by Cell 10 of your notebook.*

1. Correlation between rollout speed and change in deaths: **`X.XX`** across **`N`** countries.
2. Faster-rollout countries changed deaths/million by a median of **`X%`** vs **`Y%`** for slower countries.
3. Highest Resilience Index: **`Country A`**. Lowest: **`Country B`**.
4. Per-million normalisation makes large and small countries fairly comparable.
5. **Limitation:** variants (e.g. Omicron), age structure and testing differences also affect deaths, so this shows *association, not causation*.

---

## 🚀 How to Run

1. Open the notebook in Google Colab (link above) or upload `notebook/COVID19_Global_Impact_Dashboard.ipynb` to [colab.research.google.com](https://colab.research.google.com)
2. Click **Runtime → Run all**
3. The data downloads automatically (1-2 minutes). If the download fails, upload `owid-covid-data.csv` when prompted
4. Outputs (`covid_dashboard.html`, `executive_summary.pdf`, cleaned CSVs) download automatically

**Run locally:**
```bash
pip install -r requirements.txt
jupyter notebook notebook/COVID19_Global_Impact_Dashboard.ipynb
```

---

## 📁 Repository Structure

```
covid19-global-impact-dashboard/
├── notebook/
│   └── COVID19_Global_Impact_Dashboard.ipynb
├── dashboard/
│   └── covid_dashboard.html
├── reports/
│   └── executive_summary.pdf
├── data/
│   └── cleaned_country_results.csv
├── requirements.txt
├── .gitignore
└── README.md
```

---

## ⚠️ Limitations

- Observational analysis: correlation does not prove vaccines caused the drop in deaths
- Reporting quality and testing rates differ by country
- Countries that never reached 30% coverage, or have too little data, are excluded from the rollout analysis

---

## 🙌 Acknowledgements

- Data: [Our World in Data](https://ourworldindata.org/) (Mathieu et al., 2020)
- Internship: Veda Technology

---

## 👤 Author

**YOUR NAME** · [LinkedIn](https://linkedin.com/in/YOUR_ID) · [GitHub](https://github.com/YOUR_USERNAME)
