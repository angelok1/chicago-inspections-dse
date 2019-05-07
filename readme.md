# Predicting Food Inspection Outcomes in Chicago
**Based on the original graduate project at Haravrd contributed by:**<br>
Angelo Kastroulis, Calvin J Chiew, Tim Hagmann<br>

## Background
In an effort to reduce the public’s exposure to risk of food-borne illnesses, the [City of Chicago](https://github.com/Chicago) has developed a predictive model to [forecast food inspection outcomes](http://chicago.github.io/food-inspections-evaluation/) so that food establishments with high risk of failure can be prioritized for inspection. The new data-optimized approach to food inspections allows establishments that fail inspection (thus posing a greater health risk) to be identified earlier. Their project is now open sourced on [GitHub](https://github.com/Chicago/food-inspections-evaluation), allowing others to implement and refine their model.

## About This Project
Using the publicly available dataset of about 130,000 food inspections in Chicago since 1 January 2010, a model was developed for predicting food inspection outcomes. Building on the intuition gained from Chicago’s project, I examined how variables contained in the dataset, as well as other factors such as climate data from the National Centers for Environmental Information, business licenses, crime and 311 sanitation code complaints. This project is coded in Python (jupyter notebooks) and run on Datastax Enterprise Spark.

Our original python/sklearn project can be found [here](https://github.com/angelok1/cs109project) and website [here](https://medium.com/inspections-2).

## File Layout

DIRECTORY           | DESCRIPTION
--------------------|----------------------
`.`                 | Project files
`./data/`           | Raw data files
`./models/`        |Computed models
`./full_set/`      | parquet cleaned dataset
`./last_60_set/`      | parquet cleaned dataset of the 60 days after the mode

## Prerequisites

You'll need python 2.7 and Datastax Enterprise 5.

## Introduction
There are more than 15,000 food establishments in Chicago but fewer than three dozen food inspectors. 15% of these establishments will have at least one critical violation. Many of them are discovered long after the violations have occurred, thereby exposing the public to risk of food-borne illnesses.

To address this problem, the City of Chicago developed a model to forecast establishments with high likelihood of critical violations and prioritized them for inspections. In a pilot study, the data-optimized order of inspections identified unsafe establishments earlier than the usual workflow, by 7.5 days on average.

## Data

In this project, I used publicly available datasets of about 130,000 food inspections, business license, crime, and sanitation code (311) complaint data from Chicago’s open data portal as well as daily climate data from the National Centers for Environmental Information (NCEI).

Some aggregated features including proportion of past inspections failed, days since last inspection, most recent inspection outcome, and three/five-day rolling average of max temperatures were considered. Crime, weather and sanitation data were mapped to inspections by “clustering” them in proximity.

As expected, a majority of the time was consumed by data cleaning, exploration, and filling in missing data. For example, some missing weather data required that a separate ML model be put in place to predict the missing values.

### Exploration

Data exploration was performed on [weather](/ExploringWeather.ipynb), [inspection data](/ExploringInspectionData.ipynb), and [combined inspection and license data](/ExploringCombinedSets.ipynb).

## Data Wrangling

- [Step 1](/Step1-InspectionData.ipynb): Inspection Data
- [Step 2](/Step2-BusinessData.ipynb): Business License Data
- [Step 3](/Step3-CrimeData.ipynb): Crime Data
- [Step 4](/Step4-SanitationData.ipynb): Sanitation Complaint Data
- [Step 5](/Step5-WeatherData.ipynb): Weather Data
- [Step 6](/Step6-MoreFeatureProcessing.ipynb): Feature processing and joining weather, crime, and sanitation
- [Step 7](/Step7-FinalFeatureEngineering.ipynb): Encoding categorical features and combining all data to a final model

## Modeling

I evaluate Random Forest, Decision Tree, Gradient Boosted Trees, and Logistic Regression models against the training and test set [here](/Step8-Modeling.ipynb).

Then, for a discussion on what accuracy means to us and running the models against real data [here](/Step9-UsingOurModel.ipynb).

