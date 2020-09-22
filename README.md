# Twitter Sentiment Classification


![rt](graphs/retweet-icon-6.png)

Since I practiced linear regression in my last project, I wanted to try something different this time. I decided to use and tune classification models to classify tweets into categories: positive or negative. I ran five classification models with SKLearn as well as an LSTM recurrent neural network.


## Data Descripton

I worked with a [dataset called 'Sentiment140'](http://help.sentiment140.com/for-students/), that comprised of 1.6 million tweets from the late spring, early summer of 2009, as well as their time stamp, user, tweet ID, and most importantly, their polarity. Polatiry was listed as a 0 if a tweet was negative, 2 if a tweet was neutral, and 4 if it was positive. 

My testing data (data was pre-split into train and test) also came with a column called 'Query' which worked as a categorizer. For example, tweets with a query of 'obama' were about President Barack Obama, those with a query of "at&t" were about the company.

Because I had 'query' as well as polarity, I  wanted to see which topics were the most liked and most disliked. Because I had the dates of each tweet, I attempted to make an inference on why a certain topic was percieived a certain way.


### Topics With Highest Mean Polarity
Topic | Date | Why
----- | ---- | ----
kindle2 |  May 11 - Jun 10 2009 | came out few months ago
obama | 	May 10 2009 |	WHCD funny speech
lebron| May 11 2009 | 	47 points in playoff game
danny_gokey | May 13 2009 |	appearance on American Idol

*Obama was new, Lebron had hair, and Idol was huge. Good times.*

### Topics With Lowest Mean Polarity
Topic | Date | Why
----- | ---- | ----
iran |  June 14 2009 | 2009 election protests
gm | 	June 1 2009 |	files bankrupcy
at&t| Kune 8 2009 | 	wide spread bad service, tons of complains
aig | Jay 10 - may 18 2009 |	paid themselves huge bonuses

*Both the country and the world were on the brink of the Great Recession*


## Class Imbalance

One issue I had to briefly handle was class imbalance. My data was very clean, but I had a very equal number of positive and negative tweets (800K each) and a very small number of neutral tweets (less than 150). Since over or under sampling was not an option, I had to remove the tweets classified as neutral and just work with positives and negatives.


## Vectorizing Tweets

I used [TFIDF Vectorizer, a scikit-learn method](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html) that cleans text and turns it into numerical vectors, which can then be compared and classified using machine learning models.

## Classification Models

I ran five classification models on the tweet vectors. Below is a table and graph that shows their performance when used with their default paremeters. 

**Model** | **Accuracy Score** 
----- | ---- 
Random Forest Classifier | 0.77
Gradient Boosting Classifier | 	0.66 
Decesion Tree Classifier| 0.73
Logistic Regression | 0.80 
K - Neighbors | 0.63 


![scores](graphs/final_default.png)

I tuned my hyperparameters with GridSearchCV and I used an [AWS EC2 C5 Instance](https://aws.amazon.com/ec2/instance-types/c5/) to get more computational power. Once I got optimal hyperparemeters for all five models, I ran them on different sample sizes of data to see how each would fare. Below are the results in both table and graph form. 

**Model** | **Score on 100K sample** | **500K sample** | **1M sample** | **1.6M full data** 
----- | ---- | ---- | ---- | ---- 
Random Forest Classifier | 0.747 | 0.774 | 0.715 | 0.680
Gradient Boosting Classifier | 0.637 | 0.635 |0.554 |0.55
Decesion Tree Classifier|0.699 |0.718 |0.554 |0.55
Logistic Regression | 0.788| 0.810| 0.811| 0.813
K - Neighbors | 0.621 | 0.699 | 0.71 | 0.72

![all_scores](graphs/final_scores.png)

## LSTM Neural Network

I wanted to explore the idea of an LSTM Neural Network so I trained my tweet data on that. After spending lots of time manipulating/adding/removing layers and epochs I came up with a model whose accuracy was on par with my scikit-learn models and also had a decreasing loss per epoch. Below are the layers I ended up using, and below that is a graph of accuracy and loss. 

  * Sequential Model
  * Embedding Layer
  * Dropout Layer
  * Embedding Layer
  * **Two** LSTM Layers
  * Dense Layer, Sigmoid Activiation Function

  * 10 Epochs - ran 6 due to EarlyStop()
  * 64 Batch Size


  * Loss function: Binary Crossentropy
  
  
  ![all_scores](graphs/lstm_performance.png)
  
  
# Conclusion

My Logitic Regression and LSTM Neural Network models finished with the best scores. 

# Next Steps

* Dive deeper into my LSTM Neural Network, add more layers, both in an effort to get a higher score and learn more about the model!

* Do classification projects on multiple classes.

* Classify tweets by category, instead of by sentiment.

