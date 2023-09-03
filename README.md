# Movie_Pandemic

by [Michelle Tong](https://m1tong.github.io/) (m1tong.edu) 

Last edit: September 3, 2023

### Table of Contents
1. [Introduction](#Introduction)
2. [Research Question](#research)
3. [Background & Prior Work](#background)
4. [Hypothesis](#Hypothesis)
5. [Data(s)](#data)
6. [Data Cleaning](#cleaning)
7. 

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

## Data Cleaning <a name="cleaning"></a>

We have 4 datasets and decide to clean them separately.

### US Covid-19 Daily Cases dataset

Let's import the US Covid-19 Daily Cases dataset and take a look at it.

| submission_date   | state   | tot_cases   | conf_cases   | prob_cases   |   new_case |   pnew_case | tot_death   | conf_death   | prob_death   |   new_death |   pnew_death | created_at             | consent_cases   | consent_deaths   |\n|:------------------|:--------|:------------|:-------------|:-------------|-----------:|------------:|:------------|:-------------|:-------------|------------:|-------------:|:-----------------------|:----------------|:-----------------|\n| 03/11/2021        | KS      | 297,229     | 241,035      | 56,194       |          0 |           0 | 4,851       | nan          | nan          |           0 |            0 | 03/12/2021 03:20:13 PM | Agree           | nan              |\n| 12/01/2021        | ND      | 163,565     | 135,705      | 27,860       |        589 |         220 | 1,907       | nan          | nan          |           9 |            0 | 12/02/2021 02:35:20 PM | Agree           | Not agree        |\n| 01/02/2022        | AS      | 11          | nan          | nan          |          0 |           0 | 0           | nan          | nan          |           0 |            0 | 01/03/2022 03:18:16 PM | nan             | nan              |\n| 11/22/2021        | AL      | 841,461     | 620,483      | 220,978      |        703 |         357 | 16,377      | 12,727       | 3,650        |           7 |            3 | 11/22/2021 12:00:00 AM | Agree           | Agree            |\n| 05/30/2022        | AK      | 251,425     | nan          | nan          |          0 |           0 | 1,252       | nan          | nan          |           0 |            0 | 05/31/2022 01:20:20 PM | nan             | nan              |
