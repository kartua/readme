## Using Twitter Sentiment Analysis To Improve Stock Price Prediction Performance
## Abstract
In this project, we have create sentiment scores from twitter post and use it to predict that the stock will go up or down on. Then we use that sentiment score as additional data for stock price prediction in another model and compared the result of the prediction with and without sentiment score.

## Data
 The data that we use in this project are twitter post related to American Airline (AAL) which was acquired form  [FollowTheHashtag](https://followthehashtag.com/datasets/nasdaq-100-companies-free-twitter-dataset/) and AAL stock price form Yahoo finance API.
 ### Project files description
 In our project contain several files.

 - AAL.xlsx: file associated with twitter post related to AAL stock which we acquired from  [FollowTheHashtag](https://followthehashtag.com/datasets/nasdaq-100-companies-free-twitter-dataset/)
 - $AAL_clean.xlsx: A dataset that we created with sentiment score of each day combined with stock price of related day
 - ABL.csv: file of cleaned tweeter content for EDA purpose
 - country.csv: file which exacted from AAL.xlsx for EDA purpose
 - tweets.csv: file which exacted from AAL.xlsx for EDA purpose
 - EDA.ipynb: EDA process of our project
 - PreProcessing.ipynb: file that use AAL.xlsx data to create $AAL_clean.xlsx dataset
 - classifySentiment.ipynb: file that use sentiment score form $AAL_clean.xlsx to predict that stock will go up or down based on sentiment score.
 - LSTMstock.ipynb: file that we use to create RNN model to predict stock price from $AAL_clean.xlsx
## How to use our project
#### EDA
Exploratory data analysis can be found in EDA.ipynb file. This file use ABL.csv, contry.csv and tweets.csv as datasets for the analysis
### Project implementation
#### 1. Creating sentiment score and stock price dataset
Use Preprocessing.ipynb to create a dataset that contains sentiment score of each data and related stock price of that day. The procedure of this file is following
 - load data from ./data/AAL.xlsx
 - exact tweet content clean url, emoji, username tag and punctuation
 - use the cleaned tweet content to create sentiment score by using SentimentIntensityAnalyzer( ) module from vaderSentiment
 - combine the score from each tweet into each day score
 - load AAL stock price from yahoo finance API
 - create a new dataset which contains the sentiment score related to the stock price of each day as $AAL_clean.xlsx

 #### 2. Investigate the accuracy of sentiment score
 Use classifySentiment.ipynb to investigate how accurate the sentiment score is.
 - This file loads $AAL_clean.xlsx from the previous part
 - create label for the dataset by label 1 if the price increase in the next day otherwise 0.
 - Input sentiment score to classifiers to train the model for predicting if the price will go up or down based on the label that we create
 - By using k-fold validation(k=5) in several machine algorithms, our best algorithm was random forest with 69% accuracy and 65% F1 score
 - We concluded that our sentiment score has an acceptable performance and we would like to utilize it in our next step

#### 3. Integrate sentiment score and stock price for RNN model to predict stock price
Use LSTMstock.ipynb to create and test model for stock price prediction

 - This file load $AAL_clean.ipynb dataset and create LSTM model to predict stock price
 - It contain 2 model, one is predict by only stock price and one with stock price and our sentiment score
 - We can compare the result of the prediction of those two model
 - We found out that the model can learn stock pattern better when the integration of stock price and sentiment score data
## Challenge
The most challenge of this project is the RNN model part. Deep Neural Network is hard to understand in a limited of time. As we arrived the process of developing RNN, we only have a short time to learn how it work including the the shape of input layer which we have to use more than a single column for LSTM layers. 
## Experience
In this project we have gain a lot of experience such as
 - Pre-processing NLP data.
 - EDA for NLP data
 - Creating sentiment score and exploring the module
 - Creating and exploring various kinds of classifier algorithms
 - Using k-fold validation to train and test data
 - Creating and exploring LSTM model by using keras

## Development
This project can be improved in several ways as follow

 - Implementing other way of sentiment analysis.
 - Using more data to train our model. Since the tweet dataset for our model is only about 70 days, we have too small dataset for our model to learn.
 - Our future plan is to create sentiment analysis base on POMs surveys score. We believe that this will be a very effective way to create the score to predict stock price
- We can also create a script to real-time request tweets from tweeter and predict real-time stock price. 

## Limitation
 - A small dataset is one of our limitation for this project
 - We also have time limitation to learn more about deep neural network.
