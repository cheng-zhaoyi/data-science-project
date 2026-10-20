# Global Land Temperature Analysis (1750–2015)

A reproducible data-science project analysing more than two and a half centuries of global land surface temperature data to quantify the warming trend and test whether the rate of warming has accelerated in recent decades.

\---

## Research / Business Question

**Has the Earth's land surface warmed over the last \~265 years, and has the rate of warming accelerated in recent decades?**

Understanding the long-term trend and its rate of change matters because the impact of climate change on agriculture, water resources, infrastructure and public health depends not only on how much the planet warms, but on how fast it warms.

## Dataset \& Usage Rights

* **Dataset:** Global Land Temperatures by Month (`GlobalTemperatures.csv`)
* **Source:** Berkeley Earth, published on Kaggle (public dataset)
* **Record:** monthly global averages, January 1750 – December 2015 (3,192 rows)
* **Key columns:** `dt`, `LandAverageTemperature`, `LandAverageTemperatureUncertainty`, `LandMaxTemperature`, `LandMinTemperature`, `LandAndOceanAverageTemperature`, and their uncertainties.
* **Usage:** public dataset released for analysis; no PII, API keys or restricted data.

The data file is included under `data/`.

## Methods \& Tools

* **Language / libraries:** Python 3.12 with `pandas`, `numpy`, `matplotlib`.
* **Cleaning:** parse dates, sort by time, drop the 12 rows (0.4%) with missing land temperature.
* **Aggregation:** monthly → annual means; comparison of decade averages.
* **Anomaly:** temperature anomaly computed against the standard **1961–1990** reference period.
* **Trend estimation:** ordinary least‑squares linear regression for decadal‑rate comparison.
* **Period comparison:** full record (1750–2015) vs early (1900–1975) vs recent (1975–2015).

## Key Findings

|Finding|Result|
|-|-|
|Warming over the whole record|**≈ +1.1 °C** (1750 → 2015)|
|Trend, full record|**+0.047 °C / decade**|
|Trend, 1900–1975|+0.063 °C / decade|
|Trend, 1975–2015|**+0.272 °C / decade** (≈ **4.3×** faster)|
|Warmest year / decade|**2015** (9.83 °C) / **2010s** (≈ 9.6 °C)|
|Coldest year|1752 (5.78 °C)|
|Land vs land+ocean|Land-only warming exceeds combined warming (ocean buffering)|

The recent warming acceleration and the fact that the 2010s are the warmest decade on record are the two most salient results.

## Limitation

The pre-1900 record relies on sparse, Northern-Hemisphere-biased station coverage, so early values carry higher uncertainty; the global land average also hides strong regional variability (e.g. urban heat islands). A simple linear trend does not capture short-term variability from El Niño events or volcanic eruptions.

Reproduce the Analysis

## Improvement after peer review

Following classmate review feedback, the original linear trend line was replaced with a second‑order quadratic polynomial curve to visualise accelerated warming behaviour. An annotation was added to mark the highest‑temperature year in the dataset. Code and visual output are committed as a separate git change.

## Reproduce the Analysis

```bash
# 1. Clone / enter the project directory
cd .data-science-project

# 2. Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate        

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run the standalone script (regenerates ./plots and prints all key numbers)
python analysis.py
```

Both entry points read `data/GlobalTemperatures.csv` and write figures to `plots/`.

## Project Structure

```
.data-science-project/
├── analysis.ipynb         
├── requirements.txt       
├── data/
│   └── GlobalTemperatures.csv
└── plots/                 
      ├── 01\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\_global\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\_land\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\_trend.png
      ├── 02\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\_decadal\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\_land\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\_temperature.png
      ├── 03\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\_temperature\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\_anomaly.png
      └── 04\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\_seasonal\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\_climatology.png
```



