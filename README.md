# Weather vs. Ride-Hailing: A Statistical Analysis

A data-driven investigation into **how weather conditions affect the pricing and availability of Uber & Lyft rides** in Boston. Built with R, this project applies statistical analysis and visualization techniques to a real-world Kaggle dataset to quantify the relationship between atmospheric variables and ride economics.

---

## Research Question

**"How do weather conditions affect the pricing and availability of cab rides?"**

Ride-hailing platforms like Uber and Lyft use dynamic pricing — the assumption is that adverse weather should drive surge pricing and reduce availability. This project puts that hypothesis to the test with real data.

---

## Key Findings

| Variable Tested | Effect on Price | Effect on Availability |
|---|---|---|
| Temperature | Slight negative correlation (higher temp = marginally lower fare) | No significant effect |
| Rainfall | No significant effect — median prices stable across all levels | No significant effect |
| Atmospheric Pressure | Not tested against price | No clear relationship |
| Cloud Cover | No correlation with pricing | Not tested directly |

**Conclusion:** Contrary to popular belief, **no strong correlation was found** between weather conditions and cab pricing or availability in this dataset. The slight negative slope between temperature and price was not pronounced enough to establish a meaningful trend. The limited dataset scope (one week in Boston) likely constrained the ability to detect effects that may exist over longer periods or more extreme weather variation.

---

## Tech Stack

| Technology | Purpose |
|---|---|
| **R** | Core statistical programming language |
| **R Markdown** | Reproducible analysis with embedded code and narrative |
| **dplyr** | Data wrangling — filtering, joining, aggregation |
| **tidyverse** | End-to-end data science workflow |
| **ggplot2** | Statistical visualizations — scatter plots, boxplots, regression overlays |

---

## Data Source

- **Dataset:** [Uber and Lyft Price Prediction](https://www.kaggle.com/code/annieiachien/uber-and-lyft-price-prediction/input) (Kaggle)
- **Files:** `cab_rides.csv` (ride data) + `weather.csv` (atmospheric conditions)
- **Scope:** Boston, MA — one week of ride-hailing and weather observations

---

## Methodology

### 1. Data Cleaning
- Selected key variables: `time_stamp`, `price`, `surge_multiplier` from ride data
- Removed location redundancies and null values from weather data
- Standardized both datasets for merging

### 2. Data Wrangling
- Converted timestamps from Unix format to `POSIXct` datetime objects
- Rounded timestamps to the nearest hour to align ride and weather observations
- Built a custom `weather_hourly_fn()` function to compute hourly aggregates:
  - Mean temperature, rainfall, humidity, cloud cover, wind speed, and pressure
- Aggregated ride data by hour (ride count + average price)
- Performed a `left_join` to merge weather and ride datasets on the hourly timestamp

### 3. Exploratory Analysis & Visualization
- **Temperature vs. Ride Availability** — scatter plot colored by rainfall level
- **Atmospheric Pressure vs. Availability** — scatter plot colored by temperature
- **Rainfall vs. Price** — boxplot showing price distributions across rainfall levels
- **Multi-variable Price Analysis** — scatter plot mapping temperature to price, with cloud cover (point size) and rainfall (color) as additional dimensions

---

## Visualizations Produced

| Plot | Variables | Insight |
|---|---|---|
| Scatter + regression | Temperature vs. Availability (color: rainfall) | Flat regression line — no temperature effect |
| Scatter | Pressure vs. Availability (color: temperature) | Even distribution — no pressure effect |
| Boxplot | Rainfall level vs. Price | Stable medians — rainfall doesn't shift pricing |
| Multi-dimensional scatter | Temperature vs. Price (size: clouds, color: rain) | Weak negative slope — not statistically significant |

---

## Project Structure

```
weatheranalysis/
├── STAT 184_Final Project.Rmd   # Full R Markdown analysis (code + narrative + plots)
└── README.md
```

---

## Getting Started

```r
# Install required packages
install.packages(c("dplyr", "tidyverse", "ggplot2"))

# Open the R Markdown file in RStudio and knit to PDF
# Or render from command line:
rmarkdown::render("STAT 184_Final Project.Rmd")
```

**Data setup:** Download the [Kaggle dataset](https://www.kaggle.com/code/annieiachien/uber-and-lyft-price-prediction/input) and place `cab_rides.csv` and `weather.csv` in the project directory.

---

## Limitations & Future Work

- **Scope:** One week of Boston data — broader geographic and temporal coverage could reveal stronger effects
- **Weather variation:** Limited extreme weather events during the observation period
- **Future directions:** Expand to multi-city data, longer time ranges, and include event-based features (holidays, sports games) that may interact with weather to amplify pricing effects

---

## About

Demonstrates proficiency in statistical computing, data wrangling with dplyr, multi-variable visualization with ggplot2, and hypothesis-driven exploratory analysis on real-world datasets.
