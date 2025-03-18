# smoke-mortality
Methods to create a global dataset of annual wildfire smoke deaths in 2050

These two Jupyter Notebooks allow for the calculation and visualization of global wildfire smoke related annual deaths. The script is currently set up to run RCP 8.5 in the year 2050 and compare this to the modeled estimates of 2000, but there is data in this repo to look at a few different scenarios and time horizons. 

Smoke data is courtesy of Maria Val Martin and is produced in this paper: https://agupubs.onlinelibrary.wiley.com/doi/10.1029/2018GH000144. Population data is taken from https://www.cgd.ucar.edu/sections/iam/modeling/spatial-population at 1/8 degree resolution and using SSP2. Country-level baseline mortality data is taken from the World Bank for the year 2023: https://data.worldbank.org/indicator/SP.DYN.CDRT.IN.

Only one CDO command is run to preprocess the data for this analysis, which makes the population data fit the grid of the smoke data: cdo remapsum,r288x192 ssp2_2050.nc ssp2_2050_matching.nc

This analysis uses the equation from https://agupubs.onlinelibrary.wiley.com/doi/10.1029/2018GH000144 to calculate smoke related deaths. The equation, which is computed at each location is: 
deaths = baseline_mortality * (1-e^(-1.1 * (pm25_concentration))) * population

1.1 is used as the constant following https://ehp.niehs.nih.gov/doi/10.1289/ehp.1104049

To compute the smoke-related deaths, first run country_process, which maps the country-specific data from the Excel file onto the same grid as the smoke data. Next, run smoke_layer, which computes the smoke deaths at each grid cell, produces the figures, and also maps the spatial data to countries and produces .csv files as ouputs.
