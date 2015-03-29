#Code Book

*Data Set:* calories_bmi_gdp.csv

##Data Sources:

All data from www.gapminder.org. File [cleaningData.Rmd](https://github.com/tybyers/Udacity_datavis_project/blob/master/data/cleaningData.Rmd) contains the code for how I cleaned and combined the five data sets.

GDP/capita(US$, inflation-adjusted): https://spreadsheets.google.com/pub?key=0AkBd6lyS3EmpdHo5S0J6ekhVOF9QaVhod05QSGV4T3c&gid=0

Body Mass Index (BMI), men, Kg/m2: https://spreadsheets.google.com/pub?key=0ArfEDsV3bBwCdF9saE1pWUNYVkVsNU1FdW1Yem81Nmc&gid=0

Sugar per person (g per day): https://spreadsheets.google.com/pub?key=phAwcNAVuyj2sdmdhX9zuKg&gid=0

Food supply (kilocalories / person / day): https://spreadsheets.google.com/pub?key=0ArfEDsV3bBwCdGlYVVpXX20tbU13STZyVG0yNkRrZnc&gid=0

World Regions: https://spreadsheets.google.com/pub?key=phT4mwjvEuGBtdf1ZeO7_PQ&gid=1

##Data Variables

 * *Country* -- Country of the world
 * *Year* -- Data from years 1980-2007.  Note only data from 1990-2007 used for this visualization.
 * *Calories Per Day* -- Daily food supply, in Calories, average across both genders.
 * *Body Mass Index* -- Average Male Body Mass Index
 * *GDP Per Capita* -- Gross Domestic Product per Capita
 * *Region* -- Region of the world, as defined by gapminder.org.  Regions: America, East Asia & Pacific, Europe & Central Asia, Middle East & North Africa, Sub-Saharan Africa, South Asia.
 * *GDP.sqrt* -- Square root of GDP per capita.  Used to encode the size of the bubbles in the visualization.