# DS 4320 Project 2: Predicting Wildfire Risk in Western United States for Crisis Prevention
### Executive Summary
This README contains the materials for DS 4320 Project 1, which focuses on predicting air quality conditions at the county level to help government agencies issue timely alerts and allocate resources more effectively. The dataset was constructed from four publicly available government sources: EPA AirData daily summaries for AQI, nitrogen dioxide, and ozone across all US counties from 2020 to 2025, and the EPA National Emissions Inventory onroad mobile emissions file for 2020, which estimates vehicle emissions at the county level from sources like passenger cars, trucks, and buses on public roadways. The data is organized using the relational model across four tables. The pipeline loads this data using DuckDB, prepares it for analysis, and applies a machine learning model to predict air quality outcomes. All data, code, and documentation are linked below.

<br>

<br>

| Spec | Value |
|---|---|
| Name | Sharini Rahman |
| NetID | yeh5kr |
| DOI | [Link](https://doi.org/10.5281/zenodo.19343154) |
| Press Release | [Link to Press Release](https://github.com/srahman05/DS-4320-Project-1/blob/eb7e659be1f3539538d978a8510499ee40b31b37/press-release.md) |
| Data | [Link to Data](https://myuva-my.sharepoint.com/:f:/g/personal/yeh5kr_virginia_edu/IgBRa3z0DhIIT7WJeHvw6uEUAaD6VxoHnCiSf18yM_InRrI?e=GZw09j) |
| Pipeline | [Link to Pipeline Analysis](https://github.com/srahman05/DS-4320-Project-1/tree/ac233e1fecce92b530c35703fe316742ae2f81c8/pipeline-analysis) |
| License | [MIT](https://github.com/srahman05/DS-4320-Project-1/blob/cc5a4a19480b9613e8bbe429a9660bba0b6087cd/LICENSE) |


<br>

<br>

## Problem Definition
### General and Specific Problem
* **General Problem:** The general problem is that air pollution causes serious health risks and cities often do not have enough warning before dangerous air quality conditions occur.
* **Specific Problem:** Can we predict when a city will experience a pollution spike (a day where AQI or pollutant concentration exceeds a harmful threshold) based on recent air quality readings? Without reliable early warning, city officials cannot take action in time to protect residents.
### Rationale
The general problem of air pollution is very broad and includes policy, industrial regulation, and long-term climate trends. I narrowed the focus to predicting short-term pollution spikes because that is a problem where a data-driven model can provide direct value. Using past pollutant readings and data, a model can flag upcoming bad air days before they happen. This refinement makes the project realistic in scope and directly useful to city planners who need to issue warnings on short notice.
### Motivation
Poor air quality is linked to respiratory illness, cardiovascular disease, and premature death. Cities that can predict bad air days in advance can take steps to protect their residents, such as issuing health advisories, restricting vehicle traffic, or alerting sensitive populations like the elderly and children. A predictive model could give city officials a one to two day window to act, which could reduce health impacts and emergency response costs.
### Press Release Headline and Link
[**A New Prediction Tool Could Give Counties Early Warning Before Dangerous Air Quality Days Occur**](https://github.com/srahman05/DS-4320-Project-1/blob/eb7e659be1f3539538d978a8510499ee40b31b37/press-release.md)
