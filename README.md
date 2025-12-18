<a id="top"></a>

# US Accidents (2016 - 2023)

## A Countrywide Traffic Accident Dataset

This project explores a dataset of traffic accidents to identify the primary factors contributing to crash severity. By analysing road infrastructure, and environmental conditions, we aim to uncover insights into why certain accidents result in higher severity levels (1–4). In doing so we can predict which conditions result in more severe crashes and what can be done to improve road safety.

# ![Readme header](/images/readme_header.avif)

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

## Hypothesis and how to validate?

**Hypothesis 1**: More crashes, of a higher severity take place at night, than they do during the day regardless of the weather.  
H₀ - There will be no relationship between severity of crashes and time of day  
H₁ - The highest proportion of severe will be at night proving there is a relationship between time of day and intensity of crash

_This will be tested using:_ A chi-squared test to understand the statistical analysis followed by plotting the data.

**Result:**
We reject the Null Hypothesis. There is a significant relationship between time of day and severity. The chi-squared test supports this return a pval of 0.0001210779, well below the 0.05 threshold. The visual plots also support this, whilst there are more crashes during the day and the majority of accidents are given a severity rating of two the largest change in percentage between day and night is category 4 crashes increasing by 106%.

## Project Plan

-   Outline the high-level steps taken for the analysis.
-   How was the data managed throughout the collection, processing, analysis and interpretation steps?
-   Why did you choose the research methodologies you used?

## The rationale to map the business requirements to the Data Visualisations

-   List your business requirements and a rationale to map them to the Data Visualisations

## Analysis techniques used

-   List the data analysis methods used and explain limitations or alternative approaches.
-   How didand did you use an alternative approach to meet these challenges?
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

-   Please mention unfixed bugs and why they were not fixed. This section should include shortcomings of the frameworks or technologies used. Although time can be a significant variable to consider, paucity of time and difficulty understanding implementation are not valid reasons to leave bugs unfixed.
-   Did you recognise gaps in your knowledge, and how did you address them?
-   If applicable, include evidence of feedback received (from peers or instructors) and how it improved your approach or understanding.

## Development Roadmap

-   What challenges did you face, and what strategies were used to overcome these challenges?
-   What new skills or tools do you plan to learn next based on your project experience?

With the Decision Tree ML model different hyperparameters have been tested. Next it could prove beneficial to try a Random Forest Classifier to improve the accuracy score. The severity target variable is imbalanced which is making it hard for the model to predict accurately for targets other than a severity of 2.
To delve deeper into the data the three different twilight columns could be investigated to see if the reducing light levels has a noticeable effect on traffic accidents.

## Deployment

### Heroku

-   The App live link is: https://YOUR_APP_NAME.herokuapp.com/
-   Set the runtime.txt Python version to a [Heroku-20](https://devcenter.heroku.com/articles/python-support#supported-runtimes) stack currently supported version.
-   The project was deployed to Heroku using the following steps.

1. Log in to Heroku and create an App
2. From the Deploy tab, select GitHub as the deployment method.
3. Select your repository name and click Search. Once it is found, click Connect.
4. Select the branch you want to deploy, then click Deploy Branch.
5. The deployment process should happen smoothly if all deployment files are fully functional. Click now the button Open App on the top of the page to access your App.
6. If the slug size is too large then add large files not required for the app to the .slugignore file.

## Main Data Analysis Libraries

-   Here you should list the libraries you used in the project and provide an example(s) of how you used these libraries.

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
