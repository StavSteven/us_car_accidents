<a id="top"></a>

# US Accidents (2016 - 2023)

# ![Readme header](/images/readme_header.avif)

## Project overview

This project explores a dataset of traffic accidents to identify the primary factors contributing to crash severity. By analysing road infrastructure, and environmental conditions, we aim to uncover insights into why certain accidents result in higher severity levels (1–4). In doing so we can predict which conditions result in more severe crashes and what can be done to improve road safety.

## Project bookmarks:

-   [README](/https://github.com/StavSteven/us_car_accidents/blob/main/README.md)
-   [Project board](https://github.com/users/StavSteven/projects/12)
-   [Raw data](https://github.com/StavSteven/us_car_accidents/tree/main/data/raw_data) | [Clean data](https://github.com/StavSteven/us_car_accidents/tree/main/data/cleaned_data)
-   [ETL Notebook](/jupyter_notebooks/1_etl_us_accidents.ipynb)
-   [Visualisation & Statistical analysis Notebook](/jupyter_notebooks/2_plotting_us_accidents.ipynb)
-   [Machine Learning Notebook](/jupyter_notebooks/machine_learning.ipynb)
-   [Power BI dashboard](/dashboards/)
-   [Conclusion and discussion](#conclusion-and-discussion)

## Contents:

1. [Project Overview](#project-overview)
2. [Dataset Content](#dataset-content)
3. [Business Requirements](#business-requirements)
4. [Hypothesis Testing and Validation](#hypothesis-testing-and-validation)
5. [Project plan](#project-plan)
6. [Rationale to map business requirements](#rationale-to-map-the-business-requirements)
7. [Data Analysis Methods Used](#analysis-techniques-used)
8. [Deployment](#deployment)
9. [Dashboard design](#dashboard-design)
10. [Main Data Analysis Libraries](#main-data-analysis-libraries)
11. [Conclusion and discussion](#conclusion-and-discussion)
12. [Limitations in the data](#limitations-in-the-data)
13. [Unfixed bugs](#unfixed-bugs)
14. [Development Roadmap](#development-roadmap)
15. [Credits](#credits)
16. [Acknowledgements](#acknowledgements)

## Dataset Content

| Category          | Field               | Description                                                              | Data Type  |
| :---------------- | :------------------ | :----------------------------------------------------------------------- | :--------- |
| **Target**        | `severity`          | The severity of the accident (1 to 4), indicating the impact on traffic. | `int64`    |
| **Temporal**      | `time`              | Full timestamp of the accident occurrence.                               | `datetime` |
|                   | `year`              | The calendar year of the crash.                                          | `int64`    |
|                   | `month`             | The month of the crash (January - December).                             | `category` |
|                   | `day`               | The day of the month.                                                    | `int64`    |
|                   | `hour`              | The hour of the day (0-23) for rush-hour analysis.                       | `int32`    |
|                   | `sunrise_sunset`    | Indicates whether the accident occurred during the Day or Night.         | `object`   |
| **Location**      | `start_lat`         | The GPS latitude of the accident start point.                            | `float64`  |
|                   | `start_lng`         | The GPS longitude of the accident start point.                           | `float64`  |
|                   | `city`              | The city where the accident occurred.                                    | `object`   |
|                   | `county`            | The county where the accident occurred.                                  | `object`   |
|                   | `state`             | The US state where the accident occurred.                                | `object`   |
| **Weather**       | `weather`           | Generalised weather category.                                            | `object`   |
|                   | `weather_condition` | Detailed meteorological description (e.g., Fair, Cloudy, Rain).          | `object`   |
|                   | `temperature(f)`    | The ambient temperature in Fahrenheit.                                   | `float64`  |
|                   | `humidity(%)`       | The percentage of humidity in the air.                                   | `float64`  |
|                   | `visibility(mi)`    | Distance visible in miles at the time of the crash.                      | `float64`  |
|                   | `precipitation(in)` | Amount of rain or snow recorded in inches.                               | `float64`  |
|                   | `wind_speed(mph)`   | The speed of the wind at the time of the event.                          | `float64`  |
| **Road Features** | `crossing`          | Presence of a pedestrian crossing nearby (True/False).                   | `bool`     |
|                   | `junction`          | Indicates if the accident occurred at or near a junction (True/False).   | `bool`     |
|                   | `traffic_signal`    | Indicates if a traffic signal was present (True/False).                  | `bool`     |
| **Details**       | `description`       | A brief textual description of the accident event.                       | `object`   |

## Business Requirements

As a local council in America we want to study crash data across the country to determine which road features (junctions, crossings, or signals) are most frequently associated with high-severity crashes. As well as studying the time of day, or year when crashes are taking place to see whether we can put in any preventative measures.
Are accidents happening more at night? Are accidents around crossings more frequent than those not near crossings? Does bad weather cause the increase in number of severity of crashes that we think it does?

## Hypothesis testing and validation?

**Hypothesis 1**: More crashes, of a higher severity take place at night, than they do during the day regardless of the weather.  
H₀ - There will be no relationship between severity of crashes and time of day  
H₁ - The highest proportion of severe will be at night proving there is a relationship between time of day and intensity of crash

_This will be tested using:_ A chi-squared test to understand the statistical analysis followed by plotting the data.

**Result:**
We reject the Null Hypothesis. There is a significant relationship between time of day and severity. The chi-squared test supports this return a pval of 0.0001210779, well below the 0.05 threshold. The visual plots also support this, whilst there are more crashes during the day and the majority of accidents are given a severity rating of two the largest change in percentage between day and night is category 4 crashes increasing by 106%.

**Hypothesis 2:** Accident severity changes depending on whether an accident occurs at a junction.

-   **Null Hypothesis (H0):**  
    Accident severity does not differ between junction and non-junction locations.

-   **Alternative Hypothesis (H1):**  
    Accident severity differs between junction and non-junction locations.

---

### Data Used

-   Dataset: `us_accidents_cleaned.csv`
-   Key variables:
    -   `severity`
    -   `junction` (True / False)

The data was pre-cleaned as part of the shared ETL process.

---

### Methodology

1. Loaded the cleaned dataset in a Jupyter Notebook.
2. Grouped accident records by junction status.
3. Calculated average accident severity for:
    - Junction locations
    - Non-junction locations
4. Created visualizations to compare severity levels.
5. Interpreted the visual results to evaluate the hypothesis.

---

### Visualization

Bar charts were used to compare the **average accident severity** between junction and non-junction locations.  
These visualizations helped identify patterns and differences without applying complex statistical models.

---

### Findings

-   Accidents occurring at junctions show a **different average severity** compared to non-junction locations.
-   The visual comparison suggests that **junction presence is associated with changes in accident severity**.

---

### Conclusion

Based on the exploratory analysis and visual evidence, accident severity appears to vary depending on whether an accident occurs at a junction.  
This supports the alternative hypothesis (H1) and suggests that junctions play an important role in accident risk and outcomes.

---

## Recommendation

-   Junction areas should receive **additional safety measures**, such as improved signage and traffic control.
-   Further analysis could include:
    -   Weather conditions
    -   Time of day
    -   Traffic volume
-   Applying statistical tests or machine learning models could strengthen the findings in future work.

## Project Plan

High-Level Steps,
The dataset was collected from Kaggle and reviewed to understand its structure and variables.,
Data cleaning and preparation were performed, including handling missing values and creating day and night categories.
Exploratory Data Analysis (EDA) was conducted to identify patterns in accident severity.,
Hypotheses were tested using statistical methods (chi-squared test).,
Results were interpreted to generate insights and recommendations.,

Data Management,
Data was sourced from Kaggle and managed in a structured manner throughout the project.,
Cleaning and processing ensured data consistency and accuracy.,
Data was grouped and analysed based on key variables such as time of day and junction presence.,
Visualisations were used to support interpretation and present findings clearly.,

Research Methodologies,
Exploratory Data Analysis (EDA) was used to understand patterns in the data.,
Statistical analysis (chi-squared test) was applied to validate the hypotheses.,
Data visualisation was performed using Power BI to clearly communicate insights.

## Rationale to map the business requirements

The analysis followed a the best practice that we have learnt throughout the course. By examining the dataset of over 4,800 US traffic accidents, the initial stage focused on understanding the distribution of crash severity and identifying critical environmental and infrastructure variables. Data management was central to the process; raw data was cleaned and transformed using Pandas to ensure that temporal features—such as peak hours and seasonal months—were accurately extracted. Categorical variables and boolean flags for road features were encoded to facilitate both statistical correlation and machine learning compatibility, ensuring a high level of data integrity from collection through to interpretation.

The research methodology was designed to provide a multi-dimensional view of road safety. Quantitative analysis was employed to pinpoint how fluctuations in visibility, precipitation, and temperature correlate with accident frequency. This was complemented by a comparative infrastructure study, which isolated the impact of junctions and traffic signals on the resulting severity of a crash. To provide actionable insights for stakeholders, the project utilised supervised machine learning—specifically Decision Tree Classifiers—to rank feature importance. This "white-box" approach was chosen to ensure the findings remained transparent and interpretable for local councils and urban planners. Finally, geospatial mapping was integrated into the workflow to identify physical "black spots," transforming tabular data into a visual narrative that highlights high-risk locations across the United States.

To ensure the analysis provided actionable value, the following requirements were established to map data insights to real-world local council applications:

-   **Infrastructure Safety:** Identifying high-risk road features to prioritised engineering audits.
-   **Environmental Policy:** Determining visibility and precipitation thresholds for dynamic speed limit warnings.

### Data Visualisation Strategy

The project utilised multiple visualisation strategies:

1. **Statistical (Seaborn/Matplotlib):** Used to identify correlations between environmental factors and crash severity.
2. **Interactive (Plotly and Power BI dashboards):** Implemented to allow stakeholders to explore geographic "black spots" across the United States.
3. **Machine Learning:** We were able to create a model which was able to judge the severity of potential crashes based on weather conditions and road infrastructure.
4. **Textual (WordCloud):** Employed to analyse accident descriptions for recurring human factors or situational themes.

## Analysis techniques used

The analysis was structured around the CRISP-DM (Cross Industry Standard Process for Data Mining) framework, ensuring a systematic transition from business understanding to data preparation and modelling. We started the analysis by inspecting, cleaning and transforming it. Once the dataset was loaded, an initial assessment revealed that there were ~7.7 million records. This was far too many for our project and was also over the github data limit. We opted to take a sample of 5000 records from the original set, this would be enough to work with even taking into account the fact that we may lose some records in the cleaning phase. We handled missing values and performed data type conversions, extracting day, month, year from the date/time to allow for better analysis and visualisation. Boolean road features such as junction, crossing and traffic_signal were kept as they were, while environmental metrics like temperature and visibility were checked for outliers. This stage was critical in transforming the raw data into a structured format suitable for high-fidelity statistical exploration. Throughout this preparation phase, we utilised an Agile approach, favouring small iterations with constant evaluation to refine our variables. For example, we initially found the weather_condition column too fragmented to provide clear insights; so we chose to simplify it into 5 categorical values from the original 44.

Following the preparation of the data, we transitioned into machine learning and predictive modelling. Using Scikit-Learn, we developed a pipeline that integrated feature scaling and categorical encoding. The data was scaled using the StandardScaler to ensure that all features were on a comparable scale, which prevents features with larger numerical ranges from dominating the training process. A decision tree classifier was implemented to investigate the drivers of crash severity. A decision tree classifier was chosen for its transparency, easy to interpret the outputs and it can handle both numerical and categorical features. A decision tree is suitable for identifying the most influential variables in predicting adoption outcomes. By splitting the data into training and testing sets, we were able to validate the model's performance through accuracy scores and confusion matrices, ensuring the insights were statistically sound before moving to the visualisation stage. his is an initial model, with further testing a more tuned model or different classifier will provide more accurate predictions.

The final phase of the project focused on data visualisation using a multi-library approach to communicate findings to different stakeholders. Seaborn and Matplotlib were utilised for statistical plots, such as correlation heatmaps and distribution charts, which quantified the relationship between weather conditions and accident severity. To provide a more intuitive experience for local councils, we used Plotly to create interactive charts. Thanks to power BI we were also able to make a couple of intervative dashboards where we mapped accident coordinates across the United States, allowing for a dynamic exploration of accident "hotspots." This combination of static statistical evidence and interactive mapping ensures that the results are both scientifically rigorous and accessible for urban planning decisions.

## Deployment

[Power BI dashboards can be found here](/dashboards/)

## Dashboard Design

### Michael's

US Car Accidents
The single-page dashboard integrates multiple interactive and analytical components:

Filters and Controls
Year, Month, Day, Time Checkboxes: Selectable filters for years 2016-2023
Search Bar: Natural language query input with suggestions

Data Visualisations and Widgets

#### Weather vs Accident Count Table:

Rows: Weather conditions (Cloudy, Clear)
Columns: Precise Monthly accident counts
Widget Type: Interactive table with sorting and filtering

#### Operating Severity Influences

Widget Type: Key influencers visual
Insight: “Clear” weather increases average severity by 0.21
Purpose: Highlights statistically significant factors affecting accident severity

#### Accident Severity Per State Map

Widget Type: Interactive map with scalable blue circular markers
Data Source: OSM and TomTom via Microsoft Azure
Function: Visuals severity distribution geographically

Communicating Insights
Search Bar with Query Suggestions: Enables SQL-like or natural language queries for deeper data exploration.

Key Influencers Analysis: Uses statistical modelling to show causal relationships.

Detailed Monthly Breakdown Table: Offers granular data for time-series analysis and modelling.

Interactive Map: Visually intuitive representation of severity by state.
Checkbox Filters: Simple UI for narrowing down data by time period.
Weather Condition Table: Uses plain language and colour-coded cells to highlight trends.

### Hidaia's

### Dashboard Pages and Content

The project dashboard includes multiple visual components created by the team to analyse accident severity from different perspectives. These include:

**Accident Severity Distribution**
Visuals showing the overall distribution of accident severity levels.

**Severity by Junction Presence**
Bar charts comparing average accident severity at junctions versus non-junction locations.

**Time-Based Analysis**
Visuals showing accident counts by hour of the day.
Comparisons between day and night accidents.

**Weather and Time Interaction**
Charts illustrating how accident frequency varies by weather conditions and time of day.

**Geographical and Influencer Analysis (Dashboard)**

-   Interactive Power BI dashboard including:
-   Filters for year and time
-   Tables summarising accident metrics
-   Key influencer visuals
-   Map showing accident severity by state

**Dashboard Planning and Iteration**
The dashboard design evolved during the project. Initial plans focused on basic charts, but were later refined to include interactive elements such as filters, maps, and key influencer visuals. These changes were made to improve clarity and allow deeper exploration of the data as new insights emerged.

---

**Communication of Data Insights**
For non-technical audiences, insights were communicated using clear visuals, summaries, and interactive dashboards without requiring statistical knowledge.
For technical audiences, detailed charts, statistical results, and breakdowns by variables such as time, weather, and junction presence were provided to support deeper analysis.

---

**Dashboard Design for Different Audiences**
The dashboard was designed to simplify complex accident data by using:
Clear titles and labels
Visual comparisons instead of raw tables
Interactive filters to customise views

This approach ensures accessibility for non-technical users while still supporting detailed analysis for technical users.

## Main Data Analysis Libraries

### 📦 Project Dependencies

| Category             | Library                     | Purpose                                                     |
| :------------------- | :-------------------------- | :---------------------------------------------------------- |
| **Data Handling**    | `pandas`                    | Data cleaning, manipulation, and structural analysis.       |
|                      | `numpy`                     | Numerical operations and array handling.                    |
| **Visualisation**    | `seaborn`                   | Statistical data plotting and heatmaps.                     |
|                      | `matplotlib`                | Core plotting engine for custom static charts.              |
|                      | `plotly`                    | Interactive charts and geospatial Mapbox visualisations.    |
|                      | `wordcloud`                 | Text analysis for accident descriptions.                    |
| **Preprocessing**    | `sklearn.preprocessing`     | Feature scaling and categorical encoding (OneHot/Label).    |
|                      | `sklearn.compose`           | Managing transformations across different column types.     |
| **Machine Learning** | `sklearn.model_selection`   | Data splitting and cross-validation.                        |
|                      | `sklearn.tree`              | Decision Tree classifier implementation.                    |
|                      | `sklearn.feature_selection` | Identifying key variables affecting accident severity.      |
|                      | `sklearn.pipeline`          | Building reproducible end-to-end ML workflows.              |
|                      | `sklearn.metrics`           | Performance metrics (Accuracy, F1-Score, Confusion Matrix). |

## Conclusion and discussion

#### Machine Learning Model

Predictive modelling using a Decision Tree Classifier shows that the most important features are: Start location, temperature, year, humidity, day, time, wind and traffic crossing.

The model could be improved with further adjusting hyperparameters. Perhaps a different type of Classifier might improve the classification scores.

Given a set of conditions the model can predict the severity of a traffic accident (provided no unforeseen variables are used).

Overall accuracy: ~0.67
Not too good but accuracy is misleading because the classes of severity are highly imbalanced.

Classification Report:

-   Class 2 dominates, so the model mostly predicts class 2.
-   Classes 1, 3, 4 are severely under-predicted → recall is very low.
-   Macro F1 (~0.30) shows that minority classes are failing.

Confusion matrix:

-   Most misclassified samples of class 3 and 4 are predicted as class 2.

## Limitations in the data

## Unfixed Bugs

There were no bugs encountered throughout this project

## Development Roadmap

-   What challenges did you face, and what strategies were used to overcome these challenges?
-   What new skills or tools do you plan to learn next based on your project experience?

With the Decision Tree ML model different hyperparameters have been tested. Next it could prove beneficial to try a Random Forest Classifier to improve the accuracy score. The severity target variable is imbalanced which is making it hard for the model to predict accurately for targets other than a severity of 2.
To delve deeper into the data the three different twilight columns could be investigated to see if the reducing light levels has a noticeable effect on traffic accidents.

## Ethical considerations

There were no ethical considerations required. All the data in this dataset was anonymised, no personal details have been included.

## Credits

Data sourced from Kaggle https://www.kaggle.com/datasets/sobhanmoosavi/us-accidents

Please note the following two papers:

Moosavi, Sobhan, Mohammad Hossein Samavatian, Srinivasan Parthasarathy, and Rajiv Ramnath. “A Countrywide Traffic Accident Dataset.”, 2019.

Moosavi, Sobhan, Mohammad Hossein Samavatian, Srinivasan Parthasarathy, Radu Teodorescu, and Rajiv Ramnath. "Accident Risk Prediction based on Heterogeneous Sparse Data: New Dataset and Insights." In proceedings of the 27th ACM SIGSPATIAL International Conference on Advances in Geographic Information Systems, ACM, 2019.

Provenance: “This dataset was collected in real-time using multiple Traffic APIs. It contains accident data collected from February 2016 to March 2023 for the Contiguous United States. This dataset is being distributed solely for research purposes under the Creative Commons Attribution-Noncommercial-ShareAlike license (CC BY-NC-SA 4.0).”

-   In this section, you need to reference where you got your content, media and extra help from. It is common practice to use code from other repositories and tutorials, however, it is important to be very specific about these sources to avoid plagiarism.
-   You can break the credits section up into Content and Media, depending on what you have included in your project.

## Acknowledgements (optional)

-   Thank the people who provided support through this project.

[🔝 Back to Top](#top)
