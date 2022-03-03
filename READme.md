## Predicting NBA or Chess subreddit

Using NLP and classification techniques, is it possible to create a model that will predict which of two subreddits a post came from better than the baseline model?

Links to the two subreddits: 
https://www.reddit.com/r/chess/

https://www.reddit.com/r/nba/

### 1. Executive Summary

The goal of this project is to beat the baseline model of 50% accuracy.  

#### Scraping

First I scraped the data using Reddit's Pushshift API https://api.pushshift.io/.  In total, 1,000 posts were scraped from both the nba and chess subreddits.

#### EDA

Performed EDA on all 2,000 documents including analyzing distributions of certain engineered features.  The engineered features were: 
1. Word count 
2. Length (in characters)
3. Sentiment Analysis compound score

I then used `CountVectorizer` to split the text up into words.  Looking at the top words from each subreddit's 1,000 posts, it was apparent there were some words that could go both ways, like `game` and `time`.  It also looked like there would be some good predictors, for example `lebron` for the nba subreddit.  

#### Modeling

I split our data into training data and testing data using `Train_Test_Split`.  First I used a Logistic Regression model.  The features were all of the vectorized words columns and the engineered columns listed above.  Using `Pipeline` and `GridSearchCV`, I optimized for certain hyperparemeters and the model was 95.9% accurate. 

I tried a Random Forest model and the accuracy was slightly lower at 95.5%.  

After identifying Logistic Regression as the best model, I then analyzed the most powerful predictor words in both the nba and chess subreddits.  

### 2. Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**title**|*object*|subreddit_data.csv|Title of subreddit post.  This was combined with selftext and then CountVectorized|
|**selftext**|*object*|subreddit_data.csv|Selftext of subreddit post|
|**title_selftext_length**|*int*|subreddit_data.csv|Length of title + selftext|
|**title_selftext_word_count**|*int*|subreddit_data.csv|Word count of title + selftext|
**sentiment_compound**|*int*|subreddit_data.csv|Sentiment Analysis compound score|

### 3. Conclusions, Recommendations, and Next Steps

#### Conclusions
Yes, it is possible to create a model that predicts which of two subreddits a post came from better than the baseline model of 50% Accuracy.  The Logistic Regression model used here was 95.9% accurate.  

The difference in the two subreddits really helped the accuracy score.  There were certain words that if seen by the model, were extremely unlikely to be in one of the two classes.  

#### Recommendations and Next Steps
- To prepare for less-similar subreddits, I recommend more feature engineering and tuning of `CountVectorizer`.  

- Further investigation of the words that best and worst predicted the positive class, and tuning parameters accordingly could also improve the model.  

- Use different token patterns for Count Vectorizer to see if more effective features are attainable.