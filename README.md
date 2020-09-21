## Tweet Sentiment Classification

Since my last project was one where I practiced linear regression, I wanted to try something different this time. I dediced to use and tune classification models to classify tweets into categories: positive or negative. I ran five classification models with SKLearn as well as an LSTM recurrent neural network.


## Data Descripton

I worked with a [dataset from Analytics Vidhya](http://help.sentiment140.com/for-students/) that comprised of 1.6 million tweets from the late spring, early summer of 2009, as well as their time stamp, user, tweet ID, and most importantly, their polarity. Polatiry was listed as a 0 if a tweet was negative, 2 if a tweet was neutral, and 4 if it was positive. 

My testing data (data was pre-split into train and test) also came with a column called 'Query' which worked as a categorizer. For example, tweets with a query of 'obama' were about President Barack Obama, those with a query of "at&t" were about the company. Because I had 'query' as well as polarity, I see which topics were the most liked and most disliked. Because I had the dates of each tweet, I tried made in inference on why a certain topic was percieived a certain way.





## Class Imbalance

One issue I had to briefly handle was class imbalance. My data was very clean, but I had a very equal number of positive and negative tweets (800K each) and a very small number of neutral tweets (less than 150). Since over or under sampling was not an option, I had to remove the tweets classified as neutral and just work with positives and negatives. Below is a chart showing the extreme data imbalance.

![imbalance](graphs/balance.png)

## Vectorizing Tweets

I used [TFIDF Vectorizer, a scikit-learn method](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html) that cleans text and turns it into numerical vectors, which can then be compared and classified using machine learning models.

## Classificaition Models

I ran five classification models on the tweet vectors. Below is a graph that shows their performance when used with their default paremeters. 

![scores](graphs/default_parameters.png)

I wanted to tune my hyperparameters with GridSearchCV and I used an [AWS EC2 C5 Instance](https://aws.amazon.com/ec2/instance-types/c5/) to get more computational power. Once I got optimal hyperparemeters for all five models, I ran them on different sample sizes of data to see how each would fare. Below are the results.

![all_scores](graphs/scores.png)
