# DS 4320 Project 2: Predicting Wildfire Risk in Western United States for Crisis Prevention
### Executive Summary
This README contains the materials for DS 4320 Project 2. 

<br>

<br>

| Spec | Value |
|---|---|
| Name | Sharini Rahman |
| NetID | yeh5kr |
| DOI | [Link](https://doi.org/10.5281/zenodo.19343154) |
| Press Release | [Link to Press Release](https://github.com/srahman05/DS-4320-Project-1/blob/eb7e659be1f3539538d978a8510499ee40b31b37/press-release.md) |
| Data | [Link to Data](https://myuva-my.sharepoint.com/:f:/g/personal/yeh5kr_virginia_edu/IgAh42Bkd-YKT4hns9ODTMxhAf_ZPHtqZCuu_OTt-OEreUI?e=OqHScd) |
| Pipeline | [Link to Pipeline Analysis](https://github.com/srahman05/DS-4320-Project-1/tree/ac233e1fecce92b530c35703fe316742ae2f81c8/pipeline-analysis) |
| License | [MIT](https://github.com/srahman05/DS-4320-Project-2/blob/4cf91ab2d6f5c60a9b8e1af2d2ecc78df10ce65b/LICENSE) |


<br>

<br>

## Problem Definition
### General and Specific Problem
* **General Problem:** Wildfires in the western United States have become increasingly frequent and destructive, making it difficult for emergency managers to allocate resources effectively before fires occur.
* **Specific Problem:** This project refines that general problem into a specific question: can we predict the likelihood of a wildfire occurring in a given region based on environmental data?
### Motivation
Wildfires in the western United States have grown significantly in frequency and severity over the past two decades. Early identification of high-risk conditions can help emergency responders allocate resources before a fire starts rather than after. A risk model built on publicly available environmental data could support more proactive decision-making at the local and regional levels.
### Rationale
The general problem of predicting wildfire risk is too broad to solve meaningfully without narrowing the geographic area and defining what "risk" means in measurable terms. Focusing on the western United States makes sense because that region has the most complete historical fire data and the most pressing need. Defining risk as the probability of fire occurrence in a given area based on observable conditions makes the problem concrete and solvable with available data.
### Press Release Headline and Link
[**Seeing Wildfires Coming: Using Data to Get Ahead of the Crisis**](https://github.com/srahman05/DS-4320-Project-1/blob/eb7e659be1f3539538d978a8510499ee40b31b37/press-release.md)

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
This project lives at the intersection of environmental science, public policy, emergency management, and data science. Wildfires are a growing crisis in the western United States driven by climate change, drought, vegetation buildup, and
human activity that have all made fires more frequent and more destructive over time. The consequences go well beyond the flames, as communities are displaced, air quality drops, and property is destroyed. Local governments and emergency responders face hard decisions every fire season about where to send resources, which areas need evacuation plans, and how to prepare before conditions turn dangerous. All of those decisions depend on knowing where fire risk is highest, and right now most agencies do not have reliable tools to answer that question before a fire starts. This project uses publicly available environmental data to build a predictive model of wildfire risk that is meant to support the people making those calls on the ground.

### Background Readings - [Link to Readings](https://myuva-my.sharepoint.com/:f:/g/personal/yeh5kr_virginia_edu/IgAQ1H5BqgXSQp45Rw7MxDSlAef1JKFB9re7gvb6S3XvumY?e=fGQ1x0)

### Readings Table 
| Title | Description | Link |
|-------|--------|------|
| Wildfire Assessment Using ML Algorithms in Different Regions | Compares logistic regression and random forest models for predicting wildfire risk across regions with different climates and terrain, including the western US | [Link](https://myuva-my.sharepoint.com/:b:/g/personal/yeh5kr_virginia_edu/IQBFtfkjl7pYQZputgOX0c-AAfDa8JQXvrtQE6PYHJbRuZY?e=tO3pSY) |
| A Comprehensive Survey of the ML Pipeline for Wildfire Risk Prediction | A broad overview of machine learning approaches for wildfire prediction, covering data sources, model types, and real-world deployment challenges | [Link](https://myuva-my.sharepoint.com/:b:/g/personal/yeh5kr_virginia_edu/IQCUdi8UfS58T7lGyZptoI7oAdWg_TNGOTTg9mYzm0SvGJ8?e=bShp5N) |
| Identifying Key Drivers of Wildfires in the Contiguous US | Uses machine learning to identify the most important environmental and human factors driving wildfire burned area across the United States, with a focus on the West | [Link](https://myuva-my.sharepoint.com/:b:/g/personal/yeh5kr_virginia_edu/IQBg9tbdMSJXT4UuSGp03C4yARWHyELzB1Y03heYNR4Cn8o?e=5vBvH2) |
| Wildfire Risk Prediction: A Review | Reviews data sources, preprocessing methods, and models commonly used in wildfire prediction research, including statistical and deep learning approaches | [Link](https://myuva-my.sharepoint.com/:b:/g/personal/yeh5kr_virginia_edu/IQBep0Tl_x6RR7C0qaaNGkVZAckb1tXZaaIthJPdFG016hc?e=irltFd) |
| Wildfires in the United States 101: Context and Consequences | An accessible overview of wildfire trends, causes, and their economic, environmental, and public health impacts, with a strong focus on the western United States | [Link](https://myuva-my.sharepoint.com/:b:/g/personal/yeh5kr_virginia_edu/IQBkPzKcL408T42M62XX-UuyAb4HEN6qPQR9uBanJGDZWfk?e=GstgQN) |

