# DS 4320 Project 2: Predicting Wildfire Risk in Western United States for Crisis Prevention
### Executive Summary
This repository contains the materials for DS 4320 Project 2, which focuses on predicting wildfire risk in California and Nevada using historical fire and weather data. The project uses a MongoDB Atlas database of over 272,000 wildfire records merged with daily weather observations from 34 NOAA stations spanning 1992 to 2020. A data creation pipeline processes and loads the data into a document database, and a separate analysis pipeline applies machine learning to predict the likelihood of fire occurrence based on historical wildfire and weather data. All code, metadata, documentation, and background readings are organized in this repository. 

<br>

<br>

| Spec | Value |
|---|---|
| Name | Sharini Rahman |
| NetID | yeh5kr |
| DOI | [Link](https://doi.org/10.5281/zenodo.19645044) |
| Press Release | [Link to Press Release](https://github.com/srahman05/DS-4320-Project-2/blob/21df76162a905ac9de22636d7d5f90da8b30a3a1/press-release.md) |
| Pipeline | [Link to Pipeline Analysis](https://github.com/srahman05/DS-4320-Project-2/tree/e1f0d4107abc7563f664b557841063855fced4bf/pipeline%20analysis) |
| License | [MIT](https://github.com/srahman05/DS-4320-Project-2/blob/4cf91ab2d6f5c60a9b8e1af2d2ecc78df10ce65b/LICENSE) |


<br>

<br>

## Problem Definition
### General and Specific Problem
* **General Problem:** Wildfires in the western United States have become increasingly frequent and destructive, making it difficult for emergency managers to allocate resources effectively before fires occur.
* **Specific Problem:** This project refines that general problem into a specific question: can we predict the likelihood of a wildfire occurring in the western United States (California and Nevada) based on historical wildfire and weather data?

### Motivation
Wildfires in the western United States have grown significantly in frequency and severity over the past two decades. Early identification of high-risk conditions can help emergency responders allocate resources before a fire starts rather than after. A risk model built on publicly available environmental data could support more proactive decision-making at the local and regional levels.

### Rationale
The general problem of predicting wildfire risk is too broad to solve meaningfully without narrowing the geographic area and defining what "risk" means in measurable terms. Focusing on the western United States makes sense because that region has the most complete historical fire data and the most pressing need. Defining risk as the probability of fire occurrence in a given area based on observable conditions makes the problem concrete and solvable with available data.

### Press Release Headline and Link
[**Seeing Wildfires Coming: Using Data to Get Ahead of the Crisis**](https://github.com/srahman05/DS-4320-Project-2/blob/21df76162a905ac9de22636d7d5f90da8b30a3a1/press-release.md)

## Domain Exposition
### Terminology
| Term | Definition |
|------|------------|
| Wildfire Risk | The likelihood that a wildfire will occur in a given area based on environmental and human factors |
| Fuel Aridity | How dry the vegetation and organic matter in an area is, which affects how easily a fire can start and spread |
| Fuel Load | The amount of burnable material (trees, grass, shrubs, debris) available in a given area |
| Vapor Pressure Deficit (VPD) | A measure of how dry the atmosphere is; higher VPD means drier air, which dries out vegetation and increases fire risk |
| Wildland-Urban Interface (WUI) | Areas where homes and businesses sit directly next to wildland vegetation, making them especially vulnerable to wildfires |
| Random Forest (RF) | A machine learning model that combines many decision trees to make predictions; widely used in wildfire risk modeling |
| Burn Severity | A measure of how much damage a fire caused to soil and vegetation in a given area |

### Background Summary
This project lives at the intersection of environmental science, public policy, emergency management, and data science. Wildfires are a growing crisis in the western United States driven by climate change, drought, vegetation buildup, and human activity that have all made fires more frequent and more destructive over time. The consequences go well beyond the flames, as communities are displaced, air quality drops, and property is destroyed. Local governments and emergency responders face hard decisions every fire season about where to send resources, which areas need evacuation plans, and how to prepare before conditions turn dangerous. All of those decisions depend on knowing where fire risk is highest, and right now most agencies do not have reliable tools to answer that question before a fire starts. This project uses publicly available environmental data to build a predictive model of wildfire risk that is meant to support the people making those calls on the ground.

### Background Readings - [Link to Readings](https://myuva-my.sharepoint.com/:f:/g/personal/yeh5kr_virginia_edu/IgAQ1H5BqgXSQp45Rw7MxDSlAef1JKFB9re7gvb6S3XvumY?e=fGQ1x0)

### Readings Table 
| Title | Description | Link |
|-------|--------|------|
| Wildfire Assessment Using ML Algorithms in Different Regions | Compares logistic regression and random forest models for predicting wildfire risk across regions with different climates and terrain, including the western US | [Link](https://myuva-my.sharepoint.com/:b:/g/personal/yeh5kr_virginia_edu/IQBFtfkjl7pYQZputgOX0c-AAfDa8JQXvrtQE6PYHJbRuZY?e=tO3pSY) |
| A Comprehensive Survey of the ML Pipeline for Wildfire Risk Prediction | A broad overview of machine learning approaches for wildfire prediction, covering data sources, model types, and real-world deployment challenges | [Link](https://myuva-my.sharepoint.com/:b:/g/personal/yeh5kr_virginia_edu/IQCUdi8UfS58T7lGyZptoI7oAdWg_TNGOTTg9mYzm0SvGJ8?e=bShp5N) |
| Identifying Key Drivers of Wildfires in the Contiguous US | Uses machine learning to identify the most important environmental and human factors driving wildfire burned area across the United States, with a focus on the West | [Link](https://myuva-my.sharepoint.com/:b:/g/personal/yeh5kr_virginia_edu/IQBg9tbdMSJXT4UuSGp03C4yARWHyELzB1Y03heYNR4Cn8o?e=5vBvH2) |
| Wildfire Risk Prediction: A Review | Reviews data sources, preprocessing methods, and models commonly used in wildfire prediction research, including statistical and deep learning approaches | [Link](https://myuva-my.sharepoint.com/:b:/g/personal/yeh5kr_virginia_edu/IQBep0Tl_x6RR7C0qaaNGkVZAckb1tXZaaIthJPdFG016hc?e=irltFd) |
| Wildfires in the United States 101: Context and Consequences | An accessible overview of wildfire trends, causes, and their economic, environmental, and public health impacts, with a strong focus on the western United States | [Link](https://myuva-my.sharepoint.com/:b:/g/personal/yeh5kr_virginia_edu/IQBkPzKcL408T42M62XX-UuyAb4HEN6qPQR9uBanJGDZWfk?e=GstgQN) |

## Data Creation
### Data Acquisition Process
The primary dataset is the USFS Fire Occurrence Database, downloaded from the Forest Service Research Data Archive. It contains 2.1 million wildfire records spanning 1992 to 2020, with each record including the fire location, size in acres, cause classification, discovery date, and containment date. This dataset is considered the authoritative federal record of wildfire occurrences in the United States and was downloaded as a SQLite file.

The secondary dataset is daily weather observations from NOAA's Global Historical Climatology Network (GHCN), accessed through NOAA's Climate Data Online portal. I selected 34 stations located primarily in California and Nevada because these stations had the most complete records over the 1992 to 2020 time range. Each station provides daily readings for temperature, precipitation, snowfall, and wind speed. Both datasets are publicly available at no cost and require no special access permissions. After merging, the combined dataset is stored in a MongoDB Atlas cluster in a collection called `fires` inside the `wildfires` database.

### Code Table
| File | Description | Link |
|------|-------|------|
| data-creation.ipynb | Loads the USFS SQLite file, filters to CA and NV, reads and cleans the NOAA weather CSV, computes monthly weather averages by state, merges with fire records, builds nested documents, and inserts into MongoDB | [Link](https://github.com/srahman05/DS-4320-Project-2/blob/a8bc1f89c091af3fcad723c02da517cbaf07b561/data-creation.ipynb) |

### Rationale
The most significant judgment call in this project was how to match fire records to weather data. Each fire has a latitude and longitude, but weather stations are sparse and unevenly distributed, so matching each fire to its nearest station on the exact date would lead to many missing values. I chose to average all station readings within a state by month instead, with the trade-off of completeness over exact geographic location. This means all fires in California in June 2015, for example, receive the same weather values. This is a limitation for local analysis but is reasonable for statewide or yearly trend analysis.

I also chose to filter the dataset to California and Nevada only. These two states have the most complete weather station coverage in the NOAA pull and account for a large share of western wildfires, making them a reasonable scope for this project. Expanding to other western states would require additional weather data to maintain the same match quality.

### Bias Identification
The NOAA weather stations are not evenly distributed across CA and NV. They are concentrated in certain regions, meaning the monthly averages may not accurately represent weather conditions at the actual fire location. The USFS fire database also mainly only has fires on federally managed land, so fires on private or state land may be underrepresented. Smaller fires (size class A, under 0.25 acres) are less consistently reported across agencies and years, meaning the dataset likely undercounts small fire occurrences in earlier years. Finally, cause classification depends on human judgment at the time of reporting and may be inconsistently applied. 

### Bias Mitigation
The geographic bias in weather station coverage can be partially accounted for by including the match method field in each document, which makes it clear that weather values are state-level monthly averages rather than local measurements. Analyses that require exact weather conditions should treat these values as approximate. The underrepresentation of small fires can be mitigated by filtering analyses to fires above a certain size threshold (for example, size class C and above) where reporting is more consistent. Cause classification uncertainty can be handled by grouping causes into broader categories. 

## Metadata
### Implicit Schema
All documents in the fires collection should follow this structure. Fields marked required must be present in every document. Optional fields may be absent if the data is unavailable, but the field name and data type must remain consistent when they are included.

**Top-level fields (all required)**
- fire_id: integer, unique identifier from the USFS database
- name: string, name of the fire (may be null if unnamed)
- state: string, two-letter state code, always uppercase (e.g. "CA")
- county: string, FIPS county code
- year: integer, four-digit year of discovery
- month: integer, month of discovery (1 to 12)
- cause: string, general cause category from NWCG classification
- size_acres: float, fire size in acres
- size_class: string, single letter size classification (A through G)
- location: nested object, always contains latitude and longitude as floats
- weather: nested object, always contains all weather fields listed below

**Nested location fields (required)**
- latitude: float
- longitude: float

**Nested weather fields (required)**
- avg_temp_f: float, monthly average temperature in Fahrenheit
- avg_tmax_f: float, monthly average high temperature in Fahrenheit
- avg_tmin_f: float, monthly average low temperature in Fahrenheit
- avg_precip_in: float, monthly average daily precipitation in inches
- avg_snow_in: float, monthly average daily snowfall in inches
- avg_wind_mph: float, monthly average wind speed in mph
- match_method: string, always "state_month_average"

### Data Summary
| Property | Value |
|----------|-------|
| Database | wildfires |
| Collection | fires |
| Total documents | 272,091 |
| States covered | CA, NV |
| Year range | 1992 to 2020 |
| Weather stations used | 34 |
| Documents with full weather data | 272,091 (100%) |
| Top-level fields per document | 10 |
| Nested sub-documents | 2 (location, weather) |

### Data Dictionary
| Field | Data Type | Description | Example |
|-------|-----------|-------------|---------|
| fire_id | integer | Unique fire ID from USFS database | 10423 |
| name | string | Name assigned to the fire | "VALLEY" |
| state | string | Two-letter state code | "CA" |
| county | string | FIPS county code | "63" |
| year | integer | Year the fire was discovered | 2015 |
| month | integer | Month the fire was discovered | 6 |
| cause | string | General cause from NWCG classification | "Natural" |
| size_acres | float | Total area burned in acres | 76067.0 |
| size_class | string | USFS size classification A through G | "G" |
| location.latitude | float | Latitude of fire origin | 38.56 |
| location.longitude | float | Longitude of fire origin | -119.91 |
| weather.avg_temp_f | float | Mean daily temp for that state and month | 60.81 |
| weather.avg_tmax_f | float | Mean daily high temp for that state and month | 74.75 |
| weather.avg_tmin_f | float | Mean daily low temp for that state and month | 46.94 |
| weather.avg_precip_in | float | Mean daily precipitation for that state and month | 0.003 |
| weather.avg_snow_in | float | Mean daily snowfall for that state and month | 0.0 |
| weather.avg_wind_mph | float | Mean daily wind speed for that state and month | 10.74 |
| weather.match_method | string | Method used to join weather to fire record | "state_month_average" |

### Uncertainty Table
| Field | Mean | Std Dev | Min | Max | Notes |
|-------|------|---------|-----|-----|-------|
| size_acres | 120.42 | 3480.71 | 0.00 | 589,368 | Highly right-skewed; median is only 0.20 acres, meaning most fires are very small |
| weather.avg_temp_f | 56.76 | 10.32 | 22.73 | 74.03 | State-level average introduces geographic uncertainty for fires far from stations |
| weather.avg_tmax_f | 72.30 | 10.14 | 33.52 | 88.61 | Same geographic limitations as avg_temp_f |
| weather.avg_tmin_f | 46.23 | 7.71 | 15.00 | 60.00 | Same geographic limitations as avg_temp_f |
| weather.avg_precip_in | 0.03 | 0.04 | 0.00 | 0.41 | Very low values overall; CA and NV are arid states |
| weather.avg_snow_in | 0.00 | 0.00 | 0.00 | 0.27 | Nearly zero across all records given the warm seasons when fires occur |
| weather.avg_wind_mph | 8.27 | 1.54 | 3.43 | 12.45 | Low variance likely due to station averaging smoothing out extreme wind events |
