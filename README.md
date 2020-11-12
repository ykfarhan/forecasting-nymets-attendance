# Capstone Project - Forecasting New York Mets Game By Game Home Attendance
Yasir Karim

Source: [Baseball Reference](https://www.baseball-reference.com/teams/NYM/2020.shtml)

## Introduction
We are living in the age of a global pandemic. Covid-19 has a put a dent in global economy that hasn't been seen in decades. One of the many industries that are suffering is global sports. From Europe to Asia to North America, almost all professional sporting leagues in the world came to a halt in mid 2020. After months of constant delays and uncertainty, top level sporting leagues such the Major League Baseball and the English Premier League resumed with the help of bio-secure bubbles in order to protect playes and staff. Furthermore, teams are playing without the fans to cheer them on at the stadiums. It is a hefty price that sporting institutions around the world are paying.

Major League Baseball is a prime example of how much revenue is being lossed due to the absence of ticket sales. If we look at the New York Mets for example, they reportedly made around $100 million during the 2019 season from tickets sales and other matchday incomes such as consessions and parking sales[[source](https://www.forbes.com/teams/new-york-mets/?sh=642da0253215)]. If we can succesfully predict attendance for New York Mets home games then not only can we better estimate the lost revenue this season but we can also determine how to increase revenue in following seasons when fans are back allowed in stadiums again. We will use linear regression and time-series modelling in order to predict our target.

## Data
Our data was collected from the [Baseball Reference](https://www.baseball-reference.com) website. We exported results of each game from the past 10 seasons for the New York Mets. These results include stats like the current winning/losing streak the team is on, the attendance, the away team, how many games behind the mets are etc. These additional stats other than attendance can be used as our exogenous/feature variables for the modelling process. Below is the detailed index of this repository:

[`Data_cleaning_mlb.ipynb`](https://github.com/ykfarhan/forecasting-nymets-attendance/blob/main/Data_cleaning_mlb.ipynb): For data cleaning and exploratory data analysis

[`Regression_mlb.ipynb`](https://github.com/ykfarhan/forecasting-nymets-attendance/blob/main/Regression_mlb.ipynb): For linear regression modelling on the cleaned data 

[`time_series_mlb.ipynb`](https://github.com/ykfarhan/forecasting-nymets-attendance/blob/main/time_series_mlb.ipynb): For time-series modelling on the cleaned data

[`Visualizations/`](https://github.com/ykfarhan/forecasting-nymets-attendance/tree/main/Visualizations): For visualizations created in these notebooks:

[`Presentation_nym.pdf`](https://github.com/ykfarhan/forecasting-nymets-attendance/blob/main/Presentation_nym.pdf): For the non-technical presentation:

### Data Cleaning And Exploration
Some of the data cleaning measure we took include, removing all away games as we only care about the games played the Citi Field in Queens. Then, we added the year value to the date column indicicating which season a game was played in. We imputed missing attendace values and converted the columns _streak_, _games_behind_ & _d/n_ into numeric types. Furthermore, we engineered new features from the _date_, and _opponent_ columns among others.

### Visualizations
We explored the data initialy in order to find possible correlations between the features. We visualized these inter-feature relationships.

<img src="https://github.com/ykfarhan/forecasting-nymets-attendance/blob/main/Visualizations/weekend_night_games.png">
Weekned-night games are definitely more popular than alternative options.
<img src="https://github.com/ykfarhan/forecasting-nymets-attendance/blob/main/Visualizations/avg_attendance_daily.png">
Furthermore, games played during the weekend are popular than weekday games in general.
<img src="https://github.com/ykfarhan/forecasting-nymets-attendance/blob/main/Visualizations/attendance_x_games_behind.png">
There seems to be no significant correlation between the how many games behind the team is with attendance. A slightly positive correlation may be present.
<img src="https://github.com/ykfarhan/forecasting-nymets-attendance/blob/main/Visualizations/avg_attendance_by_team.png">
Some opponenents are clearly more popular than others such the New York Yankees and the Boston Red Sox.

### Queries
```
1. How accurately can we predict game-by-game attendance at the New York Mets home ground?
2. How much gameday revenue will the Mets lose in the 2020 season?
3. Can we identify time periods such as months or days of the week where the attendance is effected by that time period?
4. What game/seasonal stats effect attendance the most?
```

## Modelling And Evaluation Process

In order to predict our target, we iterated through two different sets of models. Firstly, we ran a set of linear regression models. We split our cleaned data into train and holdout sets in an 9:1 ratio, since we want to predict one season. After that, we fit our data through iterations of time series models. We used RMSE scores as our evaluation metric for both sets of data.
### Linear Regression
We started off with using 50 features for our training data. The K-Best (K=25) model on our original training gave us the best evaluation score. We used this model to predict on our holdout data.
| Model | RMSE |
| --- | --- |
| Dummy Regressor | 5987.98
| Linear Regression | 4763.06
| **K-Best** | **4691.09**
| Polynomial Lasso | 6130.96
| Polynomial K-Best | 4719.73

Our best model overall was the K-Best Linear Regression model. It achieved a mean absolute error of ~2000 on the holdout data. That means for every game it predicted attendace for, it was off by about 2000 tickets. Which is 7% of average tickets sold per game on the entire data set. This may indicate that that our model is better at predicting single seasons than multiples at once, which is why it has better a lot better scores than the training data.
| Best Model | Holdout RMSE | Holdout MAE |
| --- | --- | --- |
| K-Best | 2947 | 2119

<img src="https://github.com/ykfarhan/forecasting-nymets-attendance/blob/main/Visualizations/feature_imp_kbest.png">

### Post-Evaluation Analysis
Looking at the feature co-efficients of our K-best model, we can determine how each feature affects ticket sales.

* Some of our initial analysis from data exploration have been proven right.
* Weekday games and games played during may and september have a negative effect on attendance.
* Weekend night games significantly boost tickets sales. As does playing against the Yankees and the Nationals.
* Games against Cincinnati, Miami and Minnesota result in reduced ticket sales.

### Time-Series 
We started off with a simple ARMA model as our baseline and kept increasing the complexity of the models. We used subsets of the best features from our regression model as exogenoues variables for the ARIMAX and SARIMAX models. The exogenous variables included the time/day of the game, the opponent and the teams form etc. Simply looking at attendance as a series prevents us from looking at all the available information affecting ticket sales, this is why our RMSE scores improved after introducing the exogenous variables. However, our RMSE scores on these models were not as good as our regression models'.
| Model | RMSE |
| --- | --- |
| Baseline (ARMA) | 6575.41
| ARIMAX | 5389.56
| SARIMAX #1 | 5827.97
| SARIMAX #2 | 5326.13
| **SARIMAX #5** | **5006.82**

## Conclusion
* We can use the data from the 2020 season to calculate lost revenue from the predicted attendance.
* Increase prices for weekend-night games and games against popular opponents.
* Offer reduced prices for weekday games and less popular opponents.
* Improve on-field performances as negative streak & games behind have an adverse effect on ticket sales.

### Future Work
* We can integrate more features for our data such as the weather of that day and in-game stats such number of injured players.
* We may implement a recurrent neural network model to our data set.
* We can incorporate the impact of different categories of tickets sold such as premium and non-premium tickets and look at how that impacts revenue.
