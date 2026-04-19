# Seeing Wildfires Coming: Using Data to Get Ahead of the Crisis

## Hook
Right now, somewhere in California or Nevada, the conditions for a catastrophic wildfire are quietly building. Dry air, rising temperatures, and months without rain are stacking up, and most emergency teams will not know how bad it is until a fire is already burning. This project uses over 30 years of fire and weather data to change that, giving responders a way to see high risk conditions coming before the flames do.

## Problem Statement
Wildfire seasons in the western United States have grown longer and more destructive over the past two decades. In 2022 alone, just over 20,000 fires burned approximately 5.8 million acres across western states. The costs are enormous, with direct damages, firefighting expenses, and economic disruption reaching hundreds of billions of dollars each year. Despite this, many local governments and emergency agencies still rely on reactive decision making, mobilizing resources only after a fire has already started. Without a way to identify high risk windows in advance, evacuation planning, crew deployment, and equipment staging all happen under pressure and often too late.

## Solution Description
This project builds a wildfire risk prediction model trained on 272,000 fire records from California and Nevada spanning 1992 to 2020. It uses monthly weather patterns including temperature, precipitation, and wind speed to estimate how likely a large fire is to occur. The model found that summer months, especially June through August, carry significantly higher risk than the rest of the year. For emergency managers, this means knowing months in advance when to have crews staged, equipment ready, and evacuation plans reviewed. The goal is not to predict exactly where a fire will start, but to tell local governments when and where to be prepared.

## Chart
The chart below shows the average predicted probability of a large wildfire for each month of the year based on the model's output. Risk climbs steadily from spring, peaks in August, and drops off through the fall and winter. For emergency responders, this translates directly into a planning calendar. The window from June through September is when resources need to be at full readiness, and the data backs that up with three decades of fire history behind it.

![chart](https://github.com/srahman05/DS-4320-Project-2/blob/6e27f45fe4293b2186e6326b229b0cbfee543865/pipeline%20analysis/output_19_0.png)
