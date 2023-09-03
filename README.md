# Movie_Pandemic

by [Michelle Tong](https://m1tong.github.io/) (m1tong.edu) 

Last edit: September 3, 2023

### Table of Contents
1. [Introduction](#Introduction)
2. [Research Question](#research)
3. [Background & Prior Work](#background)
4. [Hypothesis](#Hypothesis)
5. [Data(s)](#data)
6. [Data Cleaning and Merging](#cleaning)
7. [Data Analysis & Results](#analysis-result)
   - [Exploratory Data Analysis](#eda)
8. [Ethics & Privacy](#ethics)
9. [Summary](#summary)

---

## Introduction <a name="Introduction"></a>

Movies have been a form of entertainments for a long time. A successful movie can bring a significant amount of revenues. However, a single decisive factor does not exist, as it often involves various confounding variables. The prevalence of COVID-19 over the past two years would be a great example of a factor that has a huge impact on the movie industry. **With this analysis, we would focus on measuring the relationship between movie variables of budget, runtime, popularity, vote average and the revenues of movies released between 2017-2022 as well as the relationship between COVID-19 variables of the number of cases/vaccines administered and the revenues of movies released between 2017-2022. We would also predict the revenue of movies with the covid and movie variables.** As a result, we have found that each of the following factors has a significant relationship with the revenue of a movie: budget, popularity, runtime, vote average, and the number of COVID-19 vaccines administered. We have futher provided a prediction model for the revenue of movies.

## Research Question <a name="research"></a>

Is there a statistically significant relationship between the Movie revenue and COVID-19, specifically the US national COVID vaccination record as well as COVID-19 cases? Moreover, how can we utilize the COVID-19 cases and vaccination along with some movie variables (budgets, runtime, popularity, vote average) to predict the revenue of movies, especially for the movie that didn't release their revenue information?

## Background & Prior Work <a name="background"></a>

The movie industry is a shining ‘business card’ that helps the American culture, society, and economy spread worldwide. A renowned entertainment industry agglomeration is located in Hollywood, Los Angeles. It has become a supreme palace in which every star worldwide wants to step in and a gigantic factory that produces numerous famous and highly rated movies worldwide. My group is interested in movie revenues in the U.S. movie industry changed over the past 60 months (past five years). Due to the covid strike, movie box office in global has decreased by 50 percents in 2021 across the world[1]. In year 2020, the revenue of U.S. movie market even dropped 80% and 71% drop for the global revenue [2]. Therefore, we will observe the relationship between the covid - vaccination data with movie revenue data, including the Covid Crisis which consists of a period of extended quarantine by every citizen spread across the U.S. society. The research can help us determine whether the covid and vaccination data relevant to local box office and whether the movie industry has successfully recovered to normal in the post-Covid period.

Since our research question mainly focus on movie box office, the ideal dataset will have to include informations of movie. It will be the best if it includes the name of the movies, the rating, release data, selling, revenue, genres, the locations that the movie release, cast, and the description of the movie. In addition, the number of observations in the movie should include at least 80% of the movie that released for the past 5 years. Data can be collected from kaggle, or webscrape from movie database website such as TMBD or IMBD. It is best that the data is stored in csv or excel to save up time, but other type of datas is acceptable as long as we can analyze it.

References:

1. McClintock, Pamela. “2021 Global Box Office down 50 Percent from Pre-Pandemic Times: MPA Report.” The Hollywood Reporter, The Hollywood Reporter, 14 Mar. 2022, https://www.hollywoodreporter.com/movies/movie-news/2021-global-box-office-pandemic-1235110511/.
2. Rubin, Rebecca. “U.S. Box Office Plummets 80%, Global Revenue Drops 71% in 2020 amid Pandemic.” Variety, Variety, 12 Jan. 2021, https://variety.com/2021/film/box-office/box-office-final-revenues-2020-coronavirus-pandemic-1234879082/.

## Hypothesis <a name="Hypothesis"></a>

We assume that there is a statistically significant relationship between the revenue of movies and the US national COVID vaccination record as well as COVID-19 cases. Specifically, we assume that the COVID-19 cases will have a more positive relationship with the revenue of movies in comparison to the COVID-19 vaccination record.

## Dataset(s) <a name="data"></a>

**Dataset - Covid-19 Cases Daily Trends**
- Dataset Name: Daily Trends in Number of COVID-19 Cases in The United States for each state
- Link to the dataset: https://data.cdc.gov/Case-Surveillance/United-States-COVID-19-Cases-and-Deaths-by-State-o/9mfq-cb36
- Number of observations: 60060

This dataset include daily numbers of confirmed and probable case and deaths retrieved by CDC from states and territories over time. The columns involved in this dataset are the Submission_Date(string), New_case(string) and etc; each row represents the number of covid-19 cases in the state reported to CDC in that day. This dataset is from the government offical Centers for Disease Control and Prevention which is truthworthy.

**Dataset - Trends in Number of COVID-19 Vaccinations in the US**
- Dataset Name: Daily Count of Doses by Date of Vaccine Administration, United State
- Link to the dataset:https://covid.cdc.gov/covid-data-tracker/#vaccination-trends
- Number of observations: 681

This dataset includes overall Trends in number of COVID-19 Vaccinations in the US at national and jurisdictional levels. The main columns involved in this dataset are the Date (string), vaccination information primarily categorized by total doses, vaccination series, and booster doses (percentage in float otherwise in integer).


**Dataset - Movies Information**
- Dataset Name: Movies Daily Update Dataset
- Link to the dataset:https://www.kaggle.com/datasets/akshaypawar7/millions-of-movies
- Number of observations: 741862

This dataset includes all movies information recorded in TMDB website. The main columns involved in this dataset are the movie id (integer), movie title (string), genres (string), popularity (float), release_date (string), budget (float), revenue(float) and so on. 

**Dataset - Final Merged DataFrame** 
- Dataset contains the combination of movie information dataset and Covid-19 Vaccination and cases datasets.
- Number of observations: 1884

This dataset is the final dataset we will use to analyse the hypothesis after merging the Covid-19 datasets with movie information dataset. The main columns involved in this dataset are the title(string), popularity(float), release_date(string),
budget(float), revenue(float), runtime(float), vote_average(float), end_date(string), num_day(integer), num_cov(integer), and 
num_vac(integer). The dataset contains every released movie in the U.S market within five years, which includes both pre-covid and covid period. In order to better matching the data of covid cases and vaccinations with every movie, we assume that the duration of every movie in the U.S market is 30 days. 

## Data Cleaning and Merging <a name="cleaning"></a>

We have 4 datasets and decide to clean them separately.

Here's the covid dataset after cleaning

| date                |   case |   tot_cases |   case10 |
|:--------------------|-------:|------------:|---------:|
| 2020-01-22 00:00:00 |      4 |           4 | 0.69897  |
| 2020-01-23 00:00:00 |      2 |           6 | 0.477121 |
| 2020-01-24 00:00:00 |      1 |           7 | 0.30103  |
| 2020-01-25 00:00:00 |      0 |           7 | 0        |
| 2020-01-26 00:00:00 |      1 |           8 | 0.30103  |

Here's the vaccine dataset after cleaning

| Date                | Week Number of Year   |   Total Doses Administered Daily |   Cumulative Vaccination |   Vaccination10 |
|:--------------------|:----------------------|---------------------------------:|-------------------------:|----------------:|
| 2020-12-14 00:00:00 | 2020-51               |                             4760 |                     4760 |         3.67761 |
| 2020-12-15 00:00:00 | 2020-51               |                            47690 |                    52450 |         4.67843 |
| 2020-12-16 00:00:00 | 2020-51               |                           159792 |                   212242 |         5.20356 |
| 2020-12-17 00:00:00 | 2020-51               |                           274780 |                   487022 |         5.43899 |
| 2020-12-18 00:00:00 | 2020-51               |                           420158 |                   907180 |         5.62341 |

Here's the movie-covid dataset after cleaning and merging

| title                  |   popularity | release_date        |      budget |          revenue |   runtime |   vote_average | end_date            |   num_day |   num_cov |   num_vac |    pop_log |   bgt_log |   rev_log |   runtime_log |
|:-----------------------|-------------:|:--------------------|------------:|-----------------:|----------:|---------------:|:--------------------|----------:|----------:|----------:|-----------:|----------:|----------:|--------------:|
| Children of Genghis    |        0.6   | 2017-01-01 00:00:00 | 1.2e+06     | 806000           |       101 |          5     | 2017-01-31 00:00:00 |        30 |         0 |         0 | -0.154902  |   6.07918 |   5.90634 |       2.00475 |
| The Invisible Guest    |       37.364 | 2017-01-06 00:00:00 | 4e+06       |      3e+07       |       107 |          8.126 | 2017-02-05 00:00:00 |        30 |         0 |         0 |  1.57361   |   6.60206 |   7.47712 |       2.02979 |
| Çalgı Çengi İkimiz     |        2.585 | 2017-01-06 00:00:00 | 3.91236e+06 |      9.07241e+06 |       116 |          6     | 2017-02-05 00:00:00 |        30 |         0 |         0 |  0.428944  |   6.59244 |   6.95772 |       2.06483 |
| Gautamiputra Satakarni |        0.946 | 2017-01-12 00:00:00 | 6e+06       |      1.2e+07     |       135 |          4.6   | 2017-02-11 00:00:00 |        30 |         0 |         0 |  0.0195317 |   6.77815 |   7.07918 |       2.13066 |
| The Bye Bye Man        |       23.312 | 2017-01-12 00:00:00 | 7.4e+06     |      2.66672e+07 |        96 |          5.2   | 2017-02-11 00:00:00 |        30 |         0 |         0 |  1.36944   |   6.86923 |   7.42598 |       1.98272 |

After cleaning up each individual dataset, we can start creating our final dataframe.

Each movie will have a corresponding "num_cov" as the cumulative number of covid cases between its release date and its showing end date (release date plus 30 days). In the case where the end date exceeds the date limit of our covid cases data (10/18/2022), we will only consider the cumulative number of covid cases between its release date and 10/18/2022. We will apply the same approach for "num_vac", the cumulative number of covid vaccination.

Note that both "num_cov" and "num_vac" are 0 for movies with its release date and end date before covid.

| title                  |   popularity | release_date        |      budget |          revenue |   runtime |   vote_average | end_date            |   num_day |   num_cov |   num_vac |    pop_log |   bgt_log |   rev_log |   runtime_log |
|:-----------------------|-------------:|:--------------------|------------:|-----------------:|----------:|---------------:|:--------------------|----------:|----------:|----------:|-----------:|----------:|----------:|--------------:|
| Children of Genghis    |        0.6   | 2017-01-01 00:00:00 | 1.2e+06     | 806000           |       101 |          5     | 2017-01-31 00:00:00 |        30 |         0 |         0 | -0.154902  |   6.07918 |   5.90634 |       2.00475 |
| The Invisible Guest    |       37.364 | 2017-01-06 00:00:00 | 4e+06       |      3e+07       |       107 |          8.126 | 2017-02-05 00:00:00 |        30 |         0 |         0 |  1.57361   |   6.60206 |   7.47712 |       2.02979 |
| Çalgı Çengi İkimiz     |        2.585 | 2017-01-06 00:00:00 | 3.91236e+06 |      9.07241e+06 |       116 |          6     | 2017-02-05 00:00:00 |        30 |         0 |         0 |  0.428944  |   6.59244 |   6.95772 |       2.06483 |
| Gautamiputra Satakarni |        0.946 | 2017-01-12 00:00:00 | 6e+06       |      1.2e+07     |       135 |          4.6   | 2017-02-11 00:00:00 |        30 |         0 |         0 |  0.0195317 |   6.77815 |   7.07918 |       2.13066 |
| The Bye Bye Man        |       23.312 | 2017-01-12 00:00:00 | 7.4e+06     |      2.66672e+07 |        96 |          5.2   | 2017-02-11 00:00:00 |        30 |         0 |         0 |  1.36944   |   6.86923 |   7.42598 |       1.98272 |


Now, we have the final dataframe we will use for EDA.

Description on the columns of the final dataframe:

- **title**: The title of a movie
- **popularity**: the popularity score of each movies based on number of votes, views, favorites, and number of times being added to the watchlist
- **release_date**: The release date of a movie
- **budget**: The budget of a movie in dollars
- **revenue**: The revenue of a movie in dollars
- **runtime**: The runtime of a movie in minutes
- **vote_average**: The overall rating of a movie by TMDB in a range of 0-10
- **end_date**: Defined as 30 days after the release date of a movie (as we assume the time between release date and end date as the showing period of a movie)
- **num_day**: The number of days record the number of days between the date of first lanuching and date of leaving the movie theater. We assume each movie would be played in the theater for 30 days. 
- **num_cov**: The cumulative number of covid cases between the release date and end date of a movie
- **num_vac**: The cumulative number of covid vaccines administered between the release date and end date of a movie

## Data Analysis & Results <a name="analysis-result"></a> 
### Exploratory Data Analysis <a name="eda"></a> 
#### Covid dataset
We will now take a look at the general trend for covid-19 cases dailly and overall.

![image](https://github.com/m1tong/Movie_Pandemic/assets/82180216/10197426-f455-451b-8cde-2f7562ff99c1)

## Prediction Model

We are going to use pipline to create prediction model to predict revenue.
1. create a preparation ColumnTransformer using standardScaler and FunctionTransformer so we can transform column to our desire value.
2. create a pipeline using our preproc(created in step 1) and a regression model we choose. For here we choose the `Decision Tree Regressor model` instead of `Linear Regression model` because not all column in our dataset is linear or normal.
3. Split our dataset into training and testing portion using train_test_split with 30% as testing data and 70% as training data. We want to split our dataset into testing and training because we want to make sure our model can predict unknown revenue using our model. And we can see how well our prediction model does because we know the acutal revenue in our testing data.
4. fit our model and predict using our testing data. 

## Ethics & Privacy <a name="ethics"></a>

As we decided our topic area to be movies as well as COVID-19 cases/vaccination, the data being used by our project does not contain any personal identifiable information or other sensitive information. We believed that such information might belong to the source of the data we used, i.e. TMBD or CDC. 

Our direct access to movie data was from a database website *Kaggle*. Per Kaggle's privacy terms as well as terms of use, we are not allowed to make any modification on a dataset or leverage a dataset for non-academic uses without a permission from the owner(s) of the dataset. We would strictly follow the requirements to ensure data privacy and would gain a permission before any use of a dataset. As the data we used was from *Kaggle*, a database website, the accuracy would not be guaranteed and should always be doubted. Hence, we have to examine the dataset carefully and compare the revenue in the dataset to its source, TMDB, and other online resources to evaluate and eliminate the accuracy of the data.

On the other hand, the source of our COVID-19 datasets was Centers for Disease Control and Prevention, the U.S. federal public health agency under the Department of Health and Human Services. While we did compare the COVID data from New York Times and that from Our World In Data developed by the University of Oxford, we considered CDC's data the most accurate and trustworthy in terms of the scope of this project. Per CDC's terms of use, we are required to give credit to CDC and are not allowed to change the substantive content of the data. We would strictly follow the requirements to ensure data integrity.

Regarding ethical concerns of our project, we acknowledged that our data and analysis did depend on a specific movie database website as our source of data, while we did not take other data sources such as streaming/video platforms into account for our analysis. On top of that, those movie database websites are similar to Wikipedia where everyone can contribute and edit, and the diversity of users might be limited. Hence, it would be possible that the data would lose its accuracy and representativeness. On top of that, as our analysis and prediction centers around COVID-19, our derived conclusion would be hard to reflect and generalize to a larger scope, such as other movies not in our dataset which were already released or will be released in the future.

We were not planning to address the above identified issues at this point. However, future groups who might take over our project could consider including more diverse data to make the data being used representitive so as to produce a more precise analysis whose conclusion might be less biased and might be able to generalize to a larger scope.


## Summary <a name="summary"></a>

Since the movie market is a booming industry and the name card of the U.S. culture and country, the movie industry has become a critical part of the U.S. GDP, which generates numerous value and employment opportunities in the country. We have noticed that the covid crisis has greatly impacted various industries in the nation, especially the worsening impact on the local entertainment industry. People were required to stay at home, remain a distance from each other, and avoid group gatherings during the covid period. Fewer people were willing to take the risk of being infected when going to the cinema. Most of them prefer to stay at home. Hence, the huge diminish of the U.S. Box office is foreseeable. In the post-covid period, we anticipate the revival of the U.S. movie market. To predict how well and how quickly would the U.S. market bounce back to the pre-covid level, we assume there is a statistically significant relationship between the revenue of movies and the US national COVID vaccination record as well as COVID-19 cases. We will try to find out the model that will predict future movie revenue based on covid and vaccination data.

We began the process by cleaning up the data first and merging multiple data sets (including movie revenues from the past five years, vaccination data, and covid cases) into one data frame that would be best for us to analyze or visualize. We assume each movie would stay in the cinema for one month and record its revenues in the data frame. In the data analysis process, the covid cases data was skewed to the left, and vaccination data is approximately normal after taking the log. In the inferential analysis step, we can observe that the relationship between covid cases and movie revenue is approximately positively correlated and the relationship between vaccination records and movie revenue is also slightly positive after taking the log. The three most transparent positive relationships with movie revenue after taking the log are movie budget, vote, and popularity, which will be two major factors we will use in the OLS model with vaccination and covid data. The OLS of Movie Revenue v.s. Covid Cases + Covid Vaccination + Runtime + Popularity + Budget + Vote Average give a high R square number, which is 0.685, which means 68.5% of movie revenues can be explained by this model. The line plot shows a positive linear relationship between these six factors, but the p-value of covid and vaccination factor is too high, which are 0.21 and 0.31, which suggests there is no significant relationship between these two factors with movie revenue. Hence, we decide to use the Decision Tree Regressor model to train the data and see the performance score. We first use the decision tree regressor on the variable covid, vaccination, popularity, budget, and runtime. The train score is 0.89686 and the test score is 0.24750. After dropping the variable covid and variable vaccination, we can see the train score increases to 0.94006 and the test score increases to 0.44427, which are quite significant. 
Overall, we do not accept the hypothesis that there is a significant relationship between movie revenue and covid data. Although the R square is large, the p-value for covid and the vaccination factor is quite large, which indicates the relationship between revenue and these data is not significant.

To take a further step in this research question and our project, we think that more movie-relevant data or variables can help us to produce a better prediction model and avoid confounding. Moreover, we can extend the region to other countries such as China and Britain, since it can help us to understand the effect of the covid on not only the U.S. movie market but also the global movie market better.
