# Boston Crime Story

An interactive data story on shooting-related incidents in Boston (2023–2024),
built from the city's open crime data. A Google Colab notebook pulls and
aggregates the raw incident records into small CSV summaries, and two
self-contained HTML pages render them as interactive [Plotly.js](https://plotly.com/javascript/)
charts that surface where and when shootings happen.

## What it shows

- **Shootings by district** — a bar chart of incident counts per police district,
  highlighting which areas report the most shootings.
- **Shootings by hour** — a line chart of incident counts by hour of day,
  revealing time-of-day patterns.
- **Linked drill-down (bonus)** — in `asst3_bonus.html`, clicking a district bar
  updates the hourly chart to show that district's own time-of-day pattern,
  driven by the combined `district_hour.csv` dataset.

## Data

Source: [Boston Open Data Portal](https://data.boston.gov/dataset) (crime incident reports).

The notebook filters to shooting-related incidents from 2023–2024 and writes
three aggregated CSVs used by the charts:

| File | Contents |
| --- | --- |
| `district.csv` | Shooting count per police district (`DISTRICT, count`) |
| `hour.csv` | Shooting count per hour of day, 0–23 (`HOUR, count`) |
| `district_hour.csv` | Counts per district × hour, for the linked drill-down (`DISTRICT, HOUR, count`) |

## Tech stack

- **Python / Google Colab** + **pandas** — pull the records from the Open Data
  Portal and aggregate them into the CSVs above.
- **Plotly.js** — interactive bar and line charts, loaded from a CDN.
- Plain **HTML/CSS** — no build step; the pages load the CSVs at runtime with
  `Plotly.d3.csv(...)`.

## Running it

Because the pages fetch the CSV files over HTTP at runtime, serve the folder
rather than opening the HTML directly from disk (a `file://` page is blocked
from reading the CSVs by the browser):

```bash
cd boston_crime_story
python3 -m http.server
```

Then open <http://localhost:8000/asst3.html> (or `asst3_bonus.html`) in your browser.

To regenerate the CSVs, open `Boston_Crime_API_Assignment.ipynb` in Google Colab
or Jupyter and run all cells.

## Files

- `asst3.html` — the two-chart data story (district bar + hourly line).
- `asst3_bonus.html` — the interactive linked version (click a district to update the hourly chart).
- `district.csv`, `hour.csv`, `district_hour.csv` — aggregated datasets.
- `Boston_Crime_API_Assignment.ipynb` — Colab notebook that assembles the datasets.

## Credits

- Data: Boston Open Data Portal
- Charts: Plotly.js
- Page styling assisted by Google Gemini

## Status

Complete — a finished course assignment ("asst3"), including the bonus interactive chart.
