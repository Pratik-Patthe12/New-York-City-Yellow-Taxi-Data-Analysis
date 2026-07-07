# New-York-City-Yellow-Taxi-Data-Analysis
An Exploratory Data Analysis (EDA) case study on New York City Yellow Taxi trip data aimed at uncovering actionable insights to optimize taxi operations, maximize revenue, and enhance passenger experience

## Objective
This project focuses on learning and applying Exploratory Data Analysis (EDA) techniques using a dataset of yellow taxi rides in New York City. The primary goal is to understand the critical role EDA plays in the data science and machine learning pipeline.

## Problem Statement
As an analyst for an upcoming NYC taxi operation, the task is to analyze 2023 taxi trip data to uncover patterns and trends. These insights are intended to inform strategic decisions that will:
* Improve service efficiency.
* Maximize revenue.
* Enhance the overall passenger experience.

## Dataset Information
The dataset consists of trip records provided to the NYC Taxi and Limousine Commission (TLC) by various technology providers.
* **Format:** Parquet (*.parquet)
* **Features:** Includes pick-up and drop-off datetimes, locations (TLC Taxi Zones 1-263), trip distances, passenger counts, payment types, and itemized fare breakdowns (standard fares, taxes, tolls, and surcharges).

## Project Workflow

### 1. Data Preparation and Sampling
Due to the massive size of the raw monthly datasets (millions of rows per month), the data is sampled to ensure computational feasibility.
* A random 5% fraction of data is extracted for every hour of every date across the 12 monthly files.
* The sampled records are concatenated into a single, manageable dataset and exported as `nyc_taxi_2025_sampled.parquet`.

### 2. Data Cleaning
Extensive data cleaning is performed to prepare the dataset for accurate analysis:
* **Column Management:** Irrelevant columns, such as `store_and_fwd_flag`, are dropped. Redundant airport fee columns are standardized and merged.
* **Fixing Negative Values:** Negative monetary values (representing refunds or disputed trips) are converted to their absolute values to preserve the trip record while correcting sign errors.
* **Handling Missing Data:** `passenger_count` and `RatecodeID` NaN values are imputed using the mode. Missing monetary fees are filled with 0. Rows missing critical location or datetime data are dropped.
* **Outlier Removal:** Erroneous records are removed, including trips with >6 passengers, zero distance but high fares, unrealistic distances (>250 miles), invalid trip durations, and undefined payment types.

### 3. Feature Engineering
New temporal features are extracted from the datetime columns to support the EDA:
* `trip_duration` (in minutes)
* `pickup_hour`
* `pickup_day`
* `pickup_month`
* `is_weekend` (boolean flag)

### 4. Exploratory Analysis & Visualizations
The cleaned data is used to conduct bivariate and multivariate analysis. Key areas of exploration include:
* Temporal analysis of taxi pickups by hours, days of the week, and months.
* Financial analysis tracking monthly revenue trends.
* Identifying revenue share by quarter.
* Analyzing correlations between trip distance, fare amount, trip duration, passenger count, and tip amount.

## Technologies Used
* **Python**
* **Pandas** (Data manipulation and Parquet file handling)
* **Numpy** (Numerical operations)
* **Matplotlib & Seaborn** (Data visualization)
