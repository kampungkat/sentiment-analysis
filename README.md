# Project 3 - API and NLPs
Project showcasing usage of APIs and NLP for text analysis and extracting insights from the same
## Project Title: Sound Decisions - Market Analysis and Consumer Sentiments
## Scenario
We, at JACK’s Consultancy Pte are a leading market research and business intelligence company based in Singapore.
Shure, the world’s leading personal audio and accessories company, is planning to enter the Singapore / South-east Asia market with the launch of their latest new wireless earbuds and headsets.
They’ve reached out to JACK’s and have commissioned to conduct market research and analysis to understand how best to position themselves in the market.

## Problem Statement
1. **Machine Learning**
   - Develop and train a sentiment analysis machine learning model to classify reviews based on their sentiment. 


2. **Data Visualizations and Insights**
    - Create visualizations to represent the findings clearly. 
    - Provide a detailed report with actionable insights and recommendations for the client.

## Project Summary
As part of the dataset analysis, we performed the following tasks in order:

**1. Data Collection and Cleaning**:
We collected user reviews from Amazon with the help of a 3rd party API marketplace - RapidAPI. We chose to only get reviews and comments from verified buyers, and tried to choose the most reviewed products, and a wide spectrum of user ratings

We then cleaned the data by dropping non-English reviews, personal information (names), emojis among others.
We then deduped all reviews, which left us with ~1.7K reviews, from an initial number of 5.9K records.

**2. Initial Data Analysis**: 
Next, we took a cursory look at our data, and tried to identify some trends and datapoints. Most review lengths ranged between 50 to 100 words, but there were some outliers with the longest review being over 9200 words (as long as a third of a novel)

**3.Exploratory Data Analysis**:
We then grouped the reviews based on the star ratings into 3 categories - Excellent (4 stars and above), Average (3 stars) and Low(2 stars and below).

We also applied text preprocessing on the review text and review title - this was done in the following order:
1. lowercasing
2. punctuation removal
3. word tokenization
4. stop word removal
5. lemmatization

We then combined both review text and review title to get a single combined column.
We tried to then identify some common themes in the reviews - and grouped them under **Aspects**
|Aspect|Key words|
|-|-|
|Sound Quality|'sound', 'audio', 'bass', 'noise', 'quality'|
|Comfort and Fit|'fit', 'comfort', 'wear', 'ear', 'head'|
|Battery Life|'battery', 'life', 'charge', 'performance'|
|Product Issues|'issue', 'problem', 'broke', 'fail', 'defect'|
|Purchase Experience|purchase', 'buy', 'order', 'warranty', 'service'|

Taking this a step further, we crafted buyer personas / types from these Aspects as below:

**Personas**

|Persona|Aspects|
|-|-|
|Audiophile|Sound Quality, Product Issues|
|Frequent Traveler|Battery Life, Sound Quality|
|Enthusiast|Battery Life, Product Issues, Purchase Experience|
|Professional|Product Issues, Sound Quality, Comfort and Fit|

**4. Data Modelling**:
For the features, we chose the preprocessed review text first, and then later the combined text column.
The target was the rating category - excellent, average and low (converted into a numeric label 2, 1 and 0 respectively)

We used a mix of simple and advanced models - of these, Support Vector Machines was the most accurate at 68%.

|Model Name|Accuracy Score|Type|Vectorizer|Notes|
|-|-|-|-|-|
|Naive Bayes|0.60|Simple|TF-IDF|Baseline model using only review_comment text|
|Naive Bayes|0.37|Simple||Word2Vec|Worst performer|
|Naive Bayes|0.63|Simple|TF-IDF|Combines review title and review comment|
|Decision Trees|0.57|Simple|TF-IDF|Worse than baseline|
|Random Forests|0.64|Simple|TF-IDF|Best among the simple models|
|**Support Vector Machines**|**0.68**|**Advanced**|**TF-IDF**|**Best of all models tested**|
|Gradient Boosting|0.65|Advanced|TF-IDF||
|XGBoost|-|Advanced|TF-IDF|Couldn't test this due to Kernel issues..|



## Conclusion and Recommendations

For the analysis -

1. We can identify and scrape more reviews from local e-commerce sites such as Lazada, Shopee etc.
2. We can look into more advanced modeling and fine-tuning with GridSearchCV etc.
3. Deploy other gradient-boosting models such as Catboost, LightGBM in place of XGB

For the client, Shure, -

1. Focus on the Aspects (category themes) and the Buyer Personas to introduce products based on these archetypes
2. Conduct more user research including both review analysis, as well as other forms of feedback gathering such as surveys, competitor research etc.
