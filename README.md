# NC PFAS Intelligence

A geospatial PFAS ("forever chemical") risk tool for North Carolina, built for the Hack-Earth hackathon. Enter a ZIP code, get your local contamination risk level — Low, Medium, or High — based on real EPA and NC DEQ water sampling data.

PFAS data is scattered, technical, and hard to act on. This tries to fix that.

---

## What it does

- Pulls from three public datasets: NC DEQ 2023 sampling data, NC DEQ 2022 PFOA/PFOS data, and EPA UCMR 5 national data
- Cleans and merges everything into a unified county-level risk table
- Applies EPA MCL thresholds (e.g. 4 ppt for PFOA/PFOS) to categorize risk as Low / Medium / High
- Expands to ZIP code level and interpolates risk for ZIPs without direct data
- Generates two maps: a county-level Plotly choropleth and a ZIP-level Folium interactive map
- Runs a Streamlit dashboard with a personal ZIP scanner, compound analysis, and well safety info

---

## Data sources

| Dataset | Source |
|---|---|
| NC DEQ 2023 PWS Sampling | [NC DEQ](https://www.deq.nc.gov) |
| NC DEQ 2022 PFOA/PFOS Data | [NC DEQ](https://www.deq.nc.gov) |
| EPA UCMR 5 | Included as `UCMR5_All_MA_WY.zip` |

---

## Setup

```bash
pip install pandas tabula-py camelot-py[cv] plotly folium geopandas branca streamlit streamlit-folium requests jpype1
```

Unzip `UCMR5_All_MA_WY.zip` before running.

---

## Run

```bash
# In Colab or Jupyter — run nc_pfs.py top to bottom
# Outputs: pfas_nc_clean.csv, pfas_nc_clean.json, pfas_nc_zip_clean.json, pfas_nc_zip_map.html

# To launch the dashboard locally:
streamlit run dashboard.py
```

> **Note:** The ngrok tunnel in the original notebook was for Colab demo purposes only. For local use, just run `streamlit run dashboard.py` directly.

---

## MCL thresholds used

| Compound | EPA Limit |
|---|---|
| PFOA | 4 ppt |
| PFOS | 4 ppt |
| GenX (HFPO-DA) | 10 ppt |
| PFNA | 10 ppt |
| PFHxS | 10 ppt |
| PFBS | 2000 ppt |

---

## Stack

`Python` · `pandas` · `geopandas` · `Plotly` · `Folium` · `Streamlit` · `tabula-py` · `LangChain` (for future semantic search layer)
