# Oregon Libraries & High School Graduation Rates

An interactive GIS analysis of the relationship between public library access and four-year high school graduation rates across all 36 Oregon counties, using 2024–25 Oregon Department of Education data.

**[View Live Map →](https://[your-username].github.io/oregon-library-graduation/)**

---

## Overview

**Research question:** Do counties with more libraries tend to have higher high school graduation rates?

This project joins three datasets — Oregon county boundaries, the Oregon State Library directory, and ODE cohort graduation and dropout statistics — into a single enriched GeoJSON and renders them as an interactive Leaflet map with a correlation scatter plot.

**Short answer:** The relationship is not linear. Raw library count correlates weakly with graduation rate (Pearson r ≈ 0.08), partly because larger urban counties (e.g., Multnomah, 48 libraries, 78.9%) and very small rural counties (e.g., Crook, 2 libraries, 97.8%) both skew the analysis in opposite directions. Socioeconomic context, student demographics, and school district characteristics are likely stronger predictors.

---

## Map Features

- **County choropleth** — counties shaded by 4-year graduation rate (red → green, 6-class RdYlGn scale)
- **Library count bubbles** — proportional circles at county centroids sized by total library count
- **Individual library points** — 360 library locations color-coded by type (Public, Academic, Special, Tribal, Volunteer)
- **County info panel** — click any county to see: graduation rate vs. state average, year-over-year change, dropout rate, library breakdown, and demographic graduation rates (with suppressed values shown as "—")
- **Correlation scatter plot** — libraries vs. graduation rate with Pearson r and OLS trendline; toggle between raw library count and libraries per 1,000 enrolled students
- **Layer toggles** — independently show/hide choropleth, count bubbles, and library points

---

## Key Findings (2024–25)

| Metric | Value |
|---|---|
| Statewide 4-year graduation rate | 83.0% |
| Graduation rate range across counties | 56.7% (Grant) – 97.8% (Crook) |
| Total libraries statewide | 360 |
| Libraries by county (range) | 1 (Sherman, Wheeler) – 48 (Multnomah) |
| Statewide dropout rate | 2.86% |
| Dropout rate range | 0.0% (Sherman) – 16.24% (Wheeler) |

**Notable patterns:**
- **Wheeler County** (1 library, 60.2% grad rate, 16.24% dropout) is the most distressed county by all three metrics
- **Grant County** has the lowest graduation rate (56.7%) and highest dropout rate outside Wheeler (10.3%), with only 2 libraries
- **Crook and Morrow counties** defy the pattern: 2 and 4 libraries respectively, yet 97.8% and 96.8% graduation rates — the highest in the state
- **Multnomah County** (Portland metro) has by far the most libraries (48) but a below-average graduation rate (78.9%), reflecting the complexity of urban education systems
- **Libraries per 1,000 students** is highly variable in small rural counties (Gilliam: 20.62, Sherman: 14.09) due to small enrollment, making raw library density a poor standalone predictor

---

## Data Sources

| Dataset | Source | Year | License |
|---|---|---|---|
| County graduation & dropout rates | [Oregon Department of Education — Graduation Rates](https://www.oregon.gov/ode/reports-and-data/students/Pages/Graduation-Rates.aspx) | 2024–25 | Public domain |
| Oregon Library Directory | [State Library of Oregon — Library Statistics Program](https://www.oregon.gov/library/libdev/Pages/library-data.aspx) | March 2026 | Public domain |
| Oregon County Boundaries | [Oregon Geospatial Data Library (GEO)](https://geo.oregon.gov/) | 2015 | Public domain |

---

## Methodology

**Unit of analysis:** Oregon county (n = 36)

**Graduation rate:** The *4-year cohort graduation rate* counts students who earned an Oregon diploma within four years of entering ninth grade, divided by the adjusted cohort (entrants minus transfers out, plus transfers in). This is the standard ODE metric and excludes extended diplomas and GED completers from the numerator.

**Student group:** All analyses use the "All Students" aggregate unless noted in the demographic breakdown panel. Demographic subgroup rates are suppressed by ODE when the cohort is fewer than 10 students, displayed as "—" in the map.

**Library count:** Sum of all library features in the Oregon Library Directory for each county, regardless of type (public, academic, special, tribal, volunteer). Libraries per 1,000 students uses the dropout file's "Fall Membership" (enrolled students) as the denominator.

**Spatial join:** County boundaries joined to library and education data using normalized county name string matching (plain county name, case-insensitive).

**Correlation:** Pearson r computed client-side over the 36 county data points displayed in the scatter plot. Counties with suppressed graduation data are excluded (none in 2024–25).

---

## Repository Structure

```
oregon-library-graduation/
├── index.html                              # Interactive map (Leaflet + Chart.js)
├── oregon_counties_enriched.geojson        # County polygons + joined statistics
├── process_data.py                         # Data processing script (generates above)
├── Oregon_Library_Directory_20260325.geojson  # Library point features (source)
├── Oregon_Counties_map_20260325.geojson    # County boundary polygons (source)
├── cohortmediafile2024-2025.xlsx           # ODE cohort graduation rates (source)
├── dropouttables2024-2025.xlsx             # ODE dropout rates (source)
└── README.md
```

---

## Tools & Libraries

- [Leaflet.js](https://leafletjs.com/) 1.9.4 — web mapping
- [Chart.js](https://www.chartjs.org/) 4.4 — scatter plot with OLS trendline
- [CartoDB Positron](https://carto.com/basemaps/) — basemap tiles
- [openpyxl](https://openpyxl.readthedocs.io/) — Excel parsing in Python

---

## Attribution

- Oregon Department of Education — graduation and dropout statistics
- State Library of Oregon — library directory data
- Oregon Geospatial Enterprise Office — county boundary data