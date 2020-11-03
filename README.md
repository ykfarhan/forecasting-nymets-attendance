# Capstone Project - Forecasting New York Mets Game By Game Home Attendance
Yasir Karim

Source: [Baseball Reference](https://www.baseball-reference.com/teams/NYM/2020.shtml)

## Introduction
We are living in the age of a global pandemic. Covid-19 has a put a dent in global economy that hasn't been seen in decades. One of the many industries that are suffering is global sports. From Europe to Asia to North America, almost all professional sporting leagues in the world came to a halt in mid 2020. After months of constant delays and uncertainty, top level sporting leagues such the Major League Baseball and the English Premier League resumed with the help of bio-secure bubbles in order to protect playes and staff. Furthermore, teams are playing without the fans to cheer them on at the stadiums. It is a hefty price that sporting institutions around the world are paying.

Major League Baseball is a prime example of how much revenue is being lossed due to the absence of ticket sales. If we look at the New York Mets for example, they reportedly made around $100 million during the 2019 season from tickets sales and other matchday incomes such as consessions and parking sales. If we can succesfully predict attendance for New York Mets home games then not only can we better estimate the lost revenue this season but we can also determine how to increase revenue in following seasons when fans are back allowed in stadiums again. We will use linear regression and time-series modelling in order to predict our target.

## Data
Our data was collected from the [Baseball Reference](https://www.baseball-reference.com) website. We exported results of each game from the past ten seasons for the New York Mets. These results include stats like the current winning/losing streak the team is on, the attendance, the away team, how many games behind the mets are etc. These additional stats other than attendance can be used as our exogenous/feature variables for the modelling process. Below is the detailed index of this repository:

For data cleaning and exploratory data analysis: [`Data_cleaning_mlb.ipynb`](https://github.com/ykfarhan/forecasting-nymets-attendance/blob/main/Data_cleaning_mlb.ipynb)

For linear regression modelling on the cleaned data: [`Regression_mlb.ipynb`](https://github.com/ykfarhan/forecasting-nymets-attendance/blob/main/Regression_mlb.ipynb)

For time-series modelling on the cleaned data: [`time_series_mlb.ipynb`](https://github.com/ykfarhan/forecasting-nymets-attendance/blob/main/time_series_mlb.ipynb)

For visualizations created in these notebooks: [`Visualizations/`]()

For the non-technical presentation: [`Presentation_mlb.pdf`]()

## Modelling Process


### Linear Regression


### Time-Series 


## Conclusion


### Future Work
