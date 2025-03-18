# Global Wildfire Smoke Mortality Analysis

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Jupyter Notebook](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)

## 📋 Table of Contents
- [Overview](#overview)
- [Data Sources](#data-sources)
- [Methodology](#methodology)
- [Repository Structure](#repository-structure)
- [Usage Instructions](#usage-instructions)
- [References](#references)

## 🔍 Overview

These Jupyter Notebooks enable the calculation and visualization of global wildfire smoke-related annual deaths. The analysis is configured to compare RCP 8.5 projections for 2050 with modeled estimates from 2000, though the repository contains data for examining various scenarios and time horizons.

## 📊 Data Sources

- **Smoke Data**: Provided by Maria Val Martin, as published in [this paper](https://agupubs.onlinelibrary.wiley.com/doi/10.1029/2018GH000144)
- **Population Data**: Sourced from [UCAR's Spatial Population Database](https://www.cgd.ucar.edu/sections/iam/modeling/spatial-population) at 1/8 degree resolution using SSP2 scenario
- **Mortality Data**: Country-level baseline mortality data from the [World Bank (2023)](https://data.worldbank.org/indicator/SP.DYN.CDRT.IN)

## 🧮 Methodology

The analysis employs the equation from [Val Martin et al. (2018)](https://agupubs.onlinelibrary.wiley.com/doi/10.1029/2018GH000144) to calculate smoke-related deaths. At each geographic location:

```
deaths = baseline_mortality * (1-e^(-1.1 * (pm25_concentration))) * population
```

The constant 1.1 is used following [Burnett et al. (2012)](https://ehp.niehs.nih.gov/doi/10.1289/ehp.1104049).

Only one CDO command is used to preprocess the data, making the population data fit the grid of the smoke data:

```bash
cdo remapsum,r288x192 ssp2_2050.nc ssp2_2050_matching.nc
```

## 📁 Repository Structure

This repository contains two primary notebooks:

1. **`country_process.ipynb`**: Maps country-specific data from the Excel file onto the same grid as the smoke data
2. **`smoke_layer.ipynb`**: Computes smoke deaths at each grid cell, produces visualizations, and maps spatial data to countries

## 🚀 Usage Instructions

To compute smoke-related deaths:

1. Create a `data` directory and add all required data files
2. First run `country_process.ipynb`, which maps country-specific data onto the smoke data grid
3. Then run `smoke_layer.ipynb`, which:
   - Computes smoke deaths at each grid cell
   - Produces visualizations
   - Maps spatial data to countries
   - Generates CSV output files

## 📚 References

- Val Martin, M., et al. (2018). [Wildfire impacts on surface smoke and air quality over global scales](https://agupubs.onlinelibrary.wiley.com/doi/10.1029/2018GH000144)
- Burnett, R. T., et al. (2012). [An integrated risk function for estimating the global burden of disease attributable to ambient fine particulate matter exposure](https://ehp.niehs.nih.gov/doi/10.1289/ehp.1104049)
- [World Bank Mortality Data](https://data.worldbank.org/indicator/SP.DYN.CDRT.IN)
- [UCAR Spatial Population Database](https://www.cgd.ucar.edu/sections/iam/modeling/spatial-population)
