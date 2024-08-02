# Yelp

## Overview

This is a project completed in Python to analyze trends and discreptencies between yelp reviews and their corresponding star ratings. Most people don't want to give a restaurant less than 5 stars if there was nothing inherently wrong with the experience, however, I was curious to find 'true' 5-star experiences across the US based on a sentiment analysis of the text reviews.


## Built With

- Python
- BeautifulSoup
- Scikit-learn
- TestBlob
- BERT
- Torch
- Transformers
- Spacy


## Data Collection

I collected data from 5000 reviews from yelp.com using the requests and bs4 libraries. I got data from 50 restaurants per city in 10 cities across the US. Due to restaurants with <10 reviews or missing data, I ended up with 4330 complete instances.


## Sentiment Analysis

To conduct the sentiment analysis, I first used textblob to calculate the polarity of each review. After playing with the tags and adjusting for the skew that was apparent, I tagged each review as 'Positive', 'Negative', or 'Neutral' from the review's polarity score.
I didn't fully like the results of this analysis after looking at the results, so I wanted to try a different approach. 
To do so, I imported a pretrained BERT model that specializes in sentiment analysis. I used this model to assign a sentiment score to each review and ran regression analyses on these scores against the original star ratings. 


## Analysis

I was curious to look at whether these sentiment scores (either from the polarity model or BERT model) would be accurate predictors for the rating that the review originally had. I ran regression analyses on both models which did not yield statistically significant results. Both models' R-squared values were also low, however, I was not expecting the regression analysis to be perfect because of the expected bias.

I also conducted residuals analyses for both models-- The mean squared error told me most predictions were about 0.7 and 0.46 stars off from the original rating for the polarity and BERT models, respectively. 

In the context of this project, this confirmed what I expected because the sentiment scores trend slightly lower than the yelp ratings. The aggregate mean for the yelp ratings was 4.4 across 4330 reviews and the aggregate sentiment scrore was 3.8 for the polarity model and 4.17 for the BERT model. 


## In Progress

I am currently making visualizations for both models. 

After, I will use spacy to extract the prominent factors from each review and use that paired with the polarity of the sentiment score to build actionable insights for each business. For example, if they have multiple negatively tagged sentiment scores with reviews that discuss service related topics, the function will be able to deliver that as an area that needs improvement for that business. 
