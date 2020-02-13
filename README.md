![LTFS Finhack2](ltfs2.jpg)

# LTFS Data Science FinHack 2

LTFS receives a lot of requests for its various finance offerings that include housing loan, two-wheeler loan, real estate financing and micro loans. The number of applications received is something that varies a lot with season. Going through these applications is a manual process and is tedious. Accurately forecasting the number of cases received can help with resource and manpower management resulting into quick response on applications and more efficient processing.

## Problem Statement
You have been appointed with the task of forecasting daily cases for next 3 months for 2 different business segments aggregated at the country level keeping in consideration the following major Indian festivals (inclusive but not exhaustive list): Diwali, Dussehra, Ganesh Chaturthi, Navratri, Holi etc. (You are free to use any publicly available open source external datasets). Some other examples could be:

Weather Macroeconomic variables Note that the external dataset must belong to a reliable source.

Data Dictionary The train data has been provided in the following way:

* For business segment 1, historical data has been made available at branch ID level For business segment 2, historical data has been made available at State level.

Train File Variable Definition application_date Date of application segment Business Segment (1/2) branch_id Anonymised id for branch at which application was received state State in which application was received (Karnataka, MP etc.) zone Zone of state in which application was received (Central, East etc.) case_count (Target) Number of cases/applications received

Test File Forecasting needs to be done at country level for the dates provided in test set for each segment.

Variable Definition id Unique id for each sample in test set application_date Date of application segment Business Segment (1/2)

### Evaluation
Evaluation Metric The evaluation metric for scoring the forecasts is **MAPE (Mean Absolute Percentage Error)**.

### Important Notes

Note that feasibility of implementation of top solutions will be considered while adjudging winners The solution must produce satisfactory results for both the business segments

Public and Private Split Test data is further divided into Public (1st Month) and Private (Next 2 months).

# Leaderboard

* **[Private LB](https://datahack.analyticsvidhya.com/contest/ltfs-data-science-finhack-2-an-online-hackathon)** : **30th/833 Rank**
* **[Public LB](https://datahack.analyticsvidhya.com/contest/ltfs-data-science-finhack-2-an-online-hackathon)** : **36th/883 Rank**

## Approach
The competition can be treated as a Time Series problem or as a regression problem. I chose the later.
* The final model was an ensemble of lightgbm and catboost with 0.7 weightage to catboost predictions and 0.3 weightage to lightgbm predictions
* Date column was extracted to add features like is_quarter_start/end, is_year_start/end etc.
* Holidays were included from 2017 to 2019. Dates not included in the holiday package was added manually.
* Dropping duplicates based on application date and segment provided a significant jump on the leaderboard.

## Things that did not work.
* Month wise car sales data from 2017 to 2019
* Year wise GDP data from 2017 to 2019.
* Cross validation
