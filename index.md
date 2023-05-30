---
layout: home
---
# Sentipedia: Analyzing Emotions and Sentiment Around Brexit 
Hello this is a test

# 1.Introduction 

### 2.What is Brexit 


### 3.Motivation

### 4.Research Design / Project Flow Diagram
Our project flow is summarised in Figure 4A below. Because reddit’s official API has several limitations on the number of pull requests and retrievable data, an API wrapper from library redditExtractoR was used to bypass its restrictions. Even though RedditExtractoR can still only obtain a limited number of posts, it is superior to the default wrapper in being able to extract all the desired information and contents of the posts. On top of this, the wrapper can restrict the query to specific subreddits, ensuring comments exclusively originate from our target audience of young British redditors. We ultimately choose the unitedkingdom subreddit, as its users represent a wider political spectrum than alternative uk politics-related subreddits, likely contains the most data points on this topic from the desired target group, and most crucially its posts mainly consist of formal news articles. Over half of the post titles are news headlines with the text consisting of the corresponding news article, leaving us with a large sample to work with. This streamlines the data collection process by simultaneously extracting the news articles and the reactions to them, allowing us to ‘kill two birds with one stone’ and avoid a separate data collection process for news articles. However, even though this method has merit in its convenience, it introduces selection bias: articles that draw the most anger and outrage are more likely to be posted on reddit. Nevertheless, given the project scope and the difficulties of matching separate news articles to reddit reactions, it probably remains the most concrete way of gaining an insight into the interaction between redditors and news articles describing Brexit-related events. 
The package also simplifies the data collection process, with just a single command needed to extract a complete data frame (top_Brexit_urls) containing the post url, timestamp, and title text. A second command then extracts the post contents into a list of dataframes (thread_contents) where the comments are indexed into a 2nd dataframe (df_Brexit). We then filtered for comments that contained the word "Brexit", which we will use for our subsequent emotional and sentimental analysis. Following the extraction, both dataframes are cleaned and wrangled using pandas from python and tidyverse in R; this process will be further detailed in the cleaning and EDA section. For subsequent analysis, with additional details and justifications provided in the section 6, thread_df’s post urls are web-scraped to obtain the article content, whereas comment_df will be preprocessed via tidytext and NLTK to assess both emotions and sentiment. The final output is then generated in the form of visualisations such as line charts, wordclouds, and barcharts. 

# 5.Initial Data Collection 

### 

### 


# 6.Data Analysis 

# 7.Discussion of Results 

# 8.Conclusion 

## What is Starcraft II?
