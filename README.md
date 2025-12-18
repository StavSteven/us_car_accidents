<a id="top"></a>

# US Accidents (2016 - 2023)

# ![Readme header](/images/readme_header.avif)

This project explores a dataset of traffic accidents to identify the primary factors contributing to crash severity. By analysing road infrastructure, and environmental conditions, we aim to uncover insights into why certain accidents result in higher severity levels (1–4). In doing so we can predict which conditions result in more severe crashes and what can be done to improve road safety.

-   [README](/https://github.com/StavSteven/us_car_accidents/blob/main/README.md)
-   [Project board](https://github.com/users/StavSteven/projects/12)
-   [Raw data](https://github.com/StavSteven/us_car_accidents/tree/main/data/raw_data) | [Clean data](https://github.com/StavSteven/us_car_accidents/tree/main/data/cleaned_data)
-   [ETL Notebook](/jupyter_notebooks/1_etl_us_accidents.ipynb)
-   [Visualisation & Statistical analysis Notebook](/jupyter_notebooks/2_plotting_us_accidents.ipynb)
-   [Machine Learning Notebook](/jupyter_notebooks/machine_learning.ipynb)
-   [Power BI dashboard](/dashboards/)
-   [Conclusion and discussion]()

1. [Project Overview](#project-overview)
2. [Dataset Content](#dataset-content)
3. [Business Requirements](#business-requirements)
4. [Hypothesis Testing and Validation](#hypothesis-testing-and-validation)
5. [Rationale to map business requirements](#rationale-to-map-business-requirements)
6. [Project plan](#project-plan)
7. [Data Analysis Methods Used](#data-analysis-methods-used)
8. [Development Roadmap](#development-roadmap)
9. [Deployment](#deployment)
10. [Main Data Analysis Libraries](#main-data-analysis-libraries)
11. [Conclusion and discussion](#conclusion-and-discussion)
12. [Limitations in the data](#limitations-in-the-data)
13. [Overall summary](#overall-summary)
14. [Credits](#credits)
15. [Acknowledgements](#acknowledgements)

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

## Data Used

-   Dataset: `us_accidents_cleaned.csv`
-   Key variables:
    -   `severity`
    -   `junction` (True / False)

The data was pre-cleaned as part of the shared ETL process.

---

## Methodology

1. Loaded the cleaned dataset in a Jupyter Notebook.
2. Grouped accident records by junction status.
3. Calculated average accident severity for:
    - Junction locations
    - Non-junction locations
4. Created visualizations to compare severity levels.
5. Interpreted the visual results to evaluate the hypothesis.

---

## Visualization

Bar charts were used to compare the **average accident severity** between junction and non-junction locations.  
These visualizations helped identify patterns and differences without applying complex statistical models.

---

## Findings

-   Accidents occurring at junctions show a **different average severity** compared to non-junction locations.
-   The visual comparison suggests that **junction presence is associated with changes in accident severity**.

---

## Conclusion

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

## The rationale to map the business requirements to the Data Visualisations

### Project Methodology and Execution

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

-   List the data analysis methods used and explain limitations or alternative approaches.
-   How did you use an alternative approach to meet these challenges?
-   How did you use generative AI tools to help with ideation, design thinking and code optimisation?

*   Utilise CRISP-DM: Cross Industry Standard Process for Data Mining
*   Utilise the Agile approach: small iterations with constant evaluation. For example: simplifying the number of weather conditions and then working with a new version of the data.

#### The machine learning model

-   Why a decision tree classifier for the machine learning model? The target variable to be predicted is one of four outputs and therefore a classification model is appropriate. A decision tree was chosen because it is easy to interpret the outputs and it can handle both numerical and categorical features. A decision tree is suitable for identifying the most influential variables in predicting adoption outcomes.

-   The data was encoded, ready for the ML model using the straightforward OneHotEncoder.

-   The data was scaled using the StandardScaler to ensure that all features were on a comparable scale, which prevents features with larger numerical ranges from dominating the training process.

-   This is an initial model, with further testing a more tuned model or different classifier will provide more accurate predictions.

## Ethical considerations

There were no ethical considerations required. All the data in this dataset was anonymised, no personal details have been included.

## Dashboard Design

-   List all dashboard pages and their content, either blocks of information or widgets, like buttons, checkboxes, images, or any other item that your dashboard library supports.
-   Later, during the project development, you may revisit your dashboard plan to update a given feature (for example, at the beginning of the project you were confident you would use a given plot to display an insight but subsequently you used another plot type).
-   How were data insights communicated to technical and non-technical audiences?
-   Explain how the dashboard was designed to communicate complex data insights to different audiences.

## Conclusions

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

## Unfixed Bugs

There were no bugs encountered throughout this project

## Development Roadmap

-   What challenges did you face, and what strategies were used to overcome these challenges?
-   What new skills or tools do you plan to learn next based on your project experience?

With the Decision Tree ML model different hyperparameters have been tested. Next it could prove beneficial to try a Random Forest Classifier to improve the accuracy score. The severity target variable is imbalanced which is making it hard for the model to predict accurately for targets other than a severity of 2.
To delve deeper into the data the three different twilight columns could be investigated to see if the reducing light levels has a noticeable effect on traffic accidents.

## Deployment

[Power BI dashboards can be found here](/dashboards/)

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

## Credits

Data sourced from Kaggle https://www.kaggle.com/datasets/sobhanmoosavi/us-accidents

Please note the following two papers:

Moosavi, Sobhan, Mohammad Hossein Samavatian, Srinivasan Parthasarathy, and Rajiv Ramnath. “A Countrywide Traffic Accident Dataset.”, 2019.

Moosavi, Sobhan, Mohammad Hossein Samavatian, Srinivasan Parthasarathy, Radu Teodorescu, and Rajiv Ramnath. "Accident Risk Prediction based on Heterogeneous Sparse Data: New Dataset and Insights." In proceedings of the 27th ACM SIGSPATIAL International Conference on Advances in Geographic Information Systems, ACM, 2019.

Provenance: “This dataset was collected in real-time using multiple Traffic APIs. It contains accident data collected from February 2016 to March 2023 for the Contiguous United States. This dataset is being distributed solely for research purposes under the Creative Commons Attribution-Noncommercial-ShareAlike license (CC BY-NC-SA 4.0).”

-   In this section, you need to reference where you got your content, media and extra help from. It is common practice to use code from other repositories and tutorials, however, it is important to be very specific about these sources to avoid plagiarism.
-   You can break the credits section up into Content and Media, depending on what you have included in your project.

### Content

-   The text for the Home page was taken from Wikipedia Article A
-   Instructions on how to implement form validation on the Sign-Up page was taken from [Specific YouTube Tutorial](https://www.youtube.com/)
-   The icons in the footer were taken from [Font Awesome](https://fontawesome.com/)

### Media

-   The photos used on the home and sign-up page are from This Open-Source site
-   The images used for the gallery page were taken from this other open-source site

## Acknowledgements (optional)

-   Thank the people who provided support through this project.

[🔝 Back to Top](#top)
