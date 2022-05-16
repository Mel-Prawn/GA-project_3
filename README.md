# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: Web APIs, NLP and Classification


# Overview

### Introduction
The increased awareness of climate change and its urgency have spurred efforts mitigate mankind's negative effect on the environment. Actions have been taken by countries with their climate pledges at the Climate Change Conference ([CNBC, 2021](https://www.cnbc.com/2021/11/13/cop26-countries-strike-climate-deal-at-un-summit-to-limit-heating.html)), and by multinational corporations. One widely publicised green initiative is the "Straw-Free" movement", which is adopted by fast food giants such as Mcdonald's and Starbucks ([National Geographic, 2019](https://www.nationalgeographic.com/environment/article/news-plastic-drinking-straw-history-ban))([CNA, 2019](https://www.channelnewsasia.com/singapore/more-than-270-fb-outlets-stop-providing-plastic-straws-july-873951)).<br/>

Riding on this wave, there is a growing market for *green* products such as reusable/glass straws, shopping bags, clothes made from recycled waste, energy efficient appliances etc.([onyalife](https://www.onyalife.com/eco-friendly-products/)) Such products appeal to consumers who subscribe to the *green* cause, and wish to reduce their impact on the environment ad having less waste.

### Problem Statement
To assist targeted advertising on social media platforms, this project seeks to create a classification model to identify users who are likely to been keen on *green* products based on their text-based interactions on such platform.

**Strategy<br/>**
To scrape posts from subreddit "ZeroWaste" which represents *green* user group and scrape posts from subreddit *Frugal* which will represent the control group. "ZeroWaste" is a subreddit where people discuss how to reduce environmental impact through green ideas and minimizing waste. Frugal is a subreddit where people discuss how to conserve time, money, resources.

These subreddits were chosen as it will contain the most challenging users to discriminate. Both contain extensive discussions on waste reduction, reusing and recycling. However, the motivations for both user groups will be different. (e.g. The "Frugal" group may be happy to secure a deal of 10,000 plastic straws for \\$1, while the "ZeroWaste" group will be more interested to buy a carbon negative glass straw at \\$20)

**Goal**: To train a classification model which can **ACCURATELY** distinguish text created by individuals who are motivated to be *green* from those are are *Frugal*. Accuracy and Sensitivity are the key metrics as you would want to get as many ZeroWaste users as possible without making too many mistakes.

### Method

**Procedures<br/>**
Part 1: Webscraping, Data Exploration and Data Cleaning
- Webscrape posts from subreddits "ZeroWaste" and "Frugal" using the pushshift API
- Do preliminary data cleaning by removing links and potential spam to ensure that there are at least 10,000 text posts from each subreddit.
- Perform data visualisation on the length of the posts and the common words or phrases in each subreddit

Part 2: Analysis and Model Tuning
- Use classifiers KNearestNeighbors, MultinomialNaiveBayes and RandomForest to differentiate between the two subreddits. Concurrently use GridSearch to find the best set of hyper parameters for each classifier.
- Feature Analysis to identify top features in the model as well as common features in missclassified posts.
- To further tune the models through stop word removal.


### Results

**Exploratory Data Analysis**<br/>
Top words in each of the subreddits included distinct words that were reflective of their underlying motivations. (e.g. "save money" and "time" in Frugal, "plastic" and "eco friendly" in ZeroWaste). If the posts contained distinctive words that are representative of its subreddit it should be correctly classified. Of course, words such as "waste" were popular in both subreddits.

#### Summary of Models with the "best hyperparameter combination" with different stopword sets

|              |                        | **Train**    |          |          | **Test**     |          |          |
|:-------------|:-----------------------|--------------|----------|----------|--------------|----------|----------|
|              |                        | **Accuracy** | **Sens** | **Spec** | **Accuracy** | **Sens** | **Spec** |
| Model 2b     | MNB original Stopwords | 0.924        | 0.944    | 0.909    | 0.884        | 0.918    | 0.860    |
| Model 2b_sw1 | MNB Stopwords set1     | 0.924        | 0.941    | 0.910    | 0.883        | 0.916    | 0.859    |
| Model 2b_sw2 | MNB Stopwords set2     | 0.924        | 0.942    | 0.909    | 0.882        | 0.912    | 0.860    |
| Model 3b     | RF original Stopwords  | 0.948        | 0.954    | 0.943    | 0.894        | 0.902    | 0.888    |
| Model 3b_sw1 | RF Stopwords set1      | 0.948        | 0.953    | 0.943    | 0.894        | 0.903    | 0.886    |
| Model 3b_sw2 | RF Stopwords set2      | 0.947        | 0.952    | 0.942    | 0.896        | 0.905    | 0.889    |


**Modeling and Tuning**<br/>
An iterative search process using GridSearch led to a decently performing model with the RandomForest algorithm. An accuracy of 89% and sensitivity of 90% was achieved, which meant that we are able to classify ZeroWaste users apart from relatively similar users rather well. The effects of removing tokens from spam entries cannot be seen at this point, but could be salient when the model is deployed on real posts. Likewise, the removal of tokens which are common and without logical affliation with either subreddits did not yield conclusive improvements.

### Future Directions
The algorithm trained performs relatively well, and will be able to identify ZeroWaste users to a high accuracy. The RandomForest model with TfdifVectorizer to be deployed for use.

Based on our analysis, we feel that thee stop words list can be further increased, and strategies such as stemming can be explored. Future analysts can also consider combining the model's predicitions with other user behaviours on the social media platform to improve prediction.