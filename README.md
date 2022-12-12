# NLP Reddit Project
Kate Crawford | US-DSI-1010 | 12.06.2022

## Problem Statement
The intention behind this project is to predict when people are asking for legal advice. Considering the low access rate to legal services, these posts are considered valid forms for evaluating legal related questions. Therefore, it is suggested that the models and insights provided by the project could be used for attorney-client matching projects to address in [The Justice Gap](https://www.lsc.gov/events/justice-gap-2022-report-release-unmet-civil-legal-needs-low-income-americans). 

View the presentation slides for this project [here](https://drive.google.com/file/d/10vNTveZoSe-bpelQiXR9gZizJKEB2pcX/view?usp=share_link).


## Project Directory
project-3
|__ code
|   |__ 01_Subreddit_Collection.ipynb
|   |__ 02_DataCleaning.ipynb
|   |__ 03_Preprocessing.ipynb
|   |__ 04_EDA.ipynb
|   |__ 05a_Modeling_RandomForest.ipynb
|   |__ 05b_Modeling_LogReg_SVC.ipynb
|   |__ extra.py
|__ data
|   |__ clean_relationships.csv
|   |__ clean_legal.csv
|   |__ raw_relationships_frame_initial_scrape.csv
|   |__ raw_legal_frame_initial_scrape.csv
|__ nlp_reddit_presentation.pdf
|__ README.md


## Exectuive Summary
First, post data was collected from the r/legaladvice and the r/relationships subreddits using Pushshift's API, the Requests library, and Beautiful Soup. About 10,000 posts from each subreddit was placed into dataframes and saved to CSV files. These two datasets were taken into another notebook and cleaned separately. Based on value counts, any missing, duplicate, and unwanted data was identified and removed. Once cleaned, the dataframes were merged. Using a replace function, binary values of 0 and 1 were applied to r/relationships and r/legaladvice, respectively, for the subreddit labels used in classification modeling.

Using spaCy, a list of natural language processing documents were created from the text column data. I created a custom function that counted each part of speech tag in each document and returned a dataframe that shared an index with the original data set. Through calculating correlation values it was found that the subreddits differed in Hence, the data was transformed in a Count Vectorizer and analyzed for word and ngram frequency. 

After analyzing the transformed data, it was passed through a three types of classifier models: (1) Random Forest, (2) Logistic Regression, and (3) a Support Vector Classifier. These models were optimized by performed Random Search and Bayes Search to get the best parameters and scores. All models outperformed the baseline of choosing the most frequent subreddit in the training data, r/relationships. The best model was chosen based on f1-score and recall with the intention of improving the true positive rate for r/legaladvice.

## Findings
All models outperformed the baseline accuracy. The best performing model was chosen based on it's ability to predict if a person's post was requesting legal advice. Therefore, models were optimized for better recall scores reflecting accuracte predictions of r/legadvice. 

The primary metric considered was f1-score for its ability to consider true positives, false positives, and false negatives in its formula. This was ideal as accuracy, precision, and recall had many overlapping improvements across models. 

The best performing model was a Random Forest Model built by cross-validating with RandomSearchCV over parameters, such as max features and bootstrapping for sample replacement. It is true that its recall score was lower than the Bayes Search using Rendom Forest as an estimator. However, the f1-score after a Random Search was the highest across all other models.

Regarding the content of the collected data, word sequences and sentiment differed between posts requesting legal advice and relationship advice. However, posts had similar word count trends, minus the occasional emotional dump in r/relationships. The altered performance of models that contained the additional features engineered durign this EDA process would be interesting to discover.

## Conclusions
The legal advice subreddit revealed that many people used legal jargon and language related to protection, responsibility, and civil rights when asking about potential legal problems. They were also 'particular' about certain aspects of their situation. This was in contrast to the relationship advice subreddit where people described their situations with 'ok'-ness and relied heavily on pronouns and personal identifiers to describe their problems.
