---
layout: home
---
# Sentipedia: Analyzing Emotions and Sentiment Around Brexit 
Hello this is a test

# 1.Introduction 

### 1.1 What is Brexit 


### 1.2 Motivation

### 1.3 Research Design / Project Flow Diagram
Our project flow is summarised in Figure 4A below. Because reddit’s official API has several limitations on the number of pull requests and retrievable data, an API wrapper from library redditExtractoR was used to bypass its restrictions. Even though RedditExtractoR can still only obtain a limited number of posts, it is superior to the default wrapper in being able to extract all the desired information and contents of the posts. On top of this, the wrapper can restrict the query to specific subreddits, ensuring comments exclusively originate from our target audience of young British redditors. We ultimately choose the unitedkingdom subreddit, as its users represent a wider political spectrum than alternative uk politics-related subreddits, likely contains the most data points on this topic from the desired target group, and most crucially its posts mainly consist of formal news articles. Over half of the post titles are news headlines with the text consisting of the corresponding news article, leaving us with a large sample to work with. This streamlines the data collection process by simultaneously extracting the news articles and the reactions to them, allowing us to ‘kill two birds with one stone’ and avoid a separate data collection process for news articles. However, even though this method has merit in its convenience, it introduces selection bias: articles that draw the most anger and outrage are more likely to be posted on reddit. Nevertheless, given the project scope and the difficulties of matching separate news articles to reddit reactions, it probably remains the most concrete way of gaining an insight into the interaction between redditors and news articles describing Brexit-related events. 
The package also simplifies the data collection process, with just a single command needed to extract a complete data frame (top_Brexit_urls) containing the post url, timestamp, and title text. A second command then extracts the post contents into a list of dataframes (thread_contents) where the comments are indexed into a 2nd dataframe (df_Brexit). We then filtered for comments that contained the word "Brexit", which we will use for our subsequent emotional and sentimental analysis. Following the extraction, both dataframes are cleaned and wrangled using pandas from python and tidyverse in R; this process will be further detailed in the cleaning and EDA section. For subsequent analysis, with additional details and justifications provided in the section 6, thread_df’s post urls are web-scraped to obtain the article content, whereas comment_df will be preprocessed via tidytext and NLTK to assess both emotions and sentiment. The final output is then generated in the form of visualisations such as line charts, wordclouds, and barcharts. 



# 2.Initial Data Collection 

### 

### 


# 3. Data Analysis 
### 3.1 Method Choice and Reasoning for Emotional Analysis
#### 3.1.1 Emotional Word Clouds Method Reasoning: 
For the word clouds, 2-word tokens were used instead of 1-word ones because it reveals more information about the context under which the phrases were used. For example, in the unigram clouds ‘pretty’ was shown as a common ‘emotional’ word, but it reveals little about the emotional target and is merely an ‘amplifier’ used for emphasis.  Of course, the 2-word case is still flawed in being biased towards common short phrases that also lack meaning, but after selectively filtering out stopwords and non-emotional words it tends to not undermine analysis; only ‘oven-ready’ is left as a vague 2 word-phrase, and even this has some Brexit-related meaning in reference to Boris Johnson’s proclamations of an ‘oven-ready’ Brexit deal. Only the top 50 bigrams were retained so the word clouds are less distracting and more comparable.

#### 3.1.2 Emotional Classification Diagrams Method Reasoning: 
Due to time constraints, an off-the-shelf dictionary-based emotional classification model was used. While this model is more advanced than others by being able to account for some negation - for example, “I don’t hate brexit” will be recorded as anger_negated instead of misclassified as anger -  it still fails to detect more nuanced negation such as sarcasm. It records 16 emotions, but only 7 emotions were kept for visualisation. 8 emotions are just their negated counterparts, which are difficult to categorise as positive or negative emotions, while 1, trust, was excluded because it seems prone to misclassification. For example, “I'm not quite sure I agree.” is assigned the highest trust score of 1, even though it suggests uncertainty/trust_negated. Unfortunately, removing ‘one-worders’ was difficult so they were kept, which could potentially distort the analysis. However, one-worders should not be particularly biased towards any emotion and so would only be ‘random noise’. For simplicity and to keep as many comments as possible, only instances where no emotions were recorded were filtered out, so it is possible for each individual sentence in a comment to have multiple emotions as it is just based on the presence of specific dictionary words. For example, the following comment was tagged with the emotions ‘trust’, ‘disgust’, and ‘anger’: 

“I'm wondering if their support was decided upon because they felt there was no realistic prospect of Corbyn actually pushing for a second vote which would mean it was another way they could oppose Brexit - which they consider likely to be seriously harmful to Scotland - whilst knowing that if no second vote happened then there's no way any future government in Westminster could plausibly argue for referendum on any agreed Scottish independence deal and be taken seriously.” 

### 3.2 Implementation: 
#### 3.2.1 Emotional Word Clouds Implementation: 
Uses the filtered dataframe (only comments mentioning Brexit). 
Preprocess comments by tokenising into word pairs (bigrams) that are separated into two columns, before removing stop words using a dataframe (stop_words) from the tidytext package and ‘non-emotional words’ based on whether it appears in a sentiment dictionary (sentiment).

#### 3.2.2 Emotional Classification Diagrams Implementation: 
Preprocess comments by tokenising each comment into individual sentences, before running sentimentr’s off-the-shelf emotion() function to get the recorded number of emotional instances for each sentence in a relatively clean dataframe (emotion1). That dataframe is then filtered to remove instances where 0 emotions were recorded for a particular sentence, before additional tidyverse functions were used to wrangle the data frames into a desired format for visualisation. 

# 7.Discussion of Results 
## 7.1 
According to the sentiment classifier, the frequency of most emotions within comments remained somewhat constant, with fluctuations occurring only by a few percentage points YoY. There are limited changes in the relative rankings, with disgust being the least common and anticipation being the most common expressed emotion throughout the period. 
However, it is clear the ‘negative’ emotions of fear, anger, and disgust surpassed the ‘positive’ emotions of joy and anticipation, with the disparity gradually increasing over time. However, the dominance of negative emotions is probably understated; the simple dictionary-based sentiment classifier is unlikely to detect sarcasm, which in a social media context tends to employ positive words to describe a negative situation as noted by Riloff et al (2013) on twitter comments. Nevertheless, the diagram does paint a rough picture of the emotional distribution, which suggests negative emotions are becoming increasingly more prevalent compared to positive emotions. 
The second diagram shows the mean scores associated with most emotions fluctuated over time but remained relatively similar to each other for most of the time period. The Figure X results again reinforces the idea that there was some misclassification, because comments received a similar score despite negative emotions being prominent according to Figure X; one might expect the more positive emotions to have noticeably lower scores. Another possible reason for this could be due to more controversy in comments tagged with negative emotions, leading to a wider distribution of highly rated and lowly rated negative and positive emotions. 
However, a conspicuous exception is disgust, which was associated with a significantly higher score than all other emotions since 2020 despite being the least common emotion according to Figure X. The strong correlation between disgust and high scores suggests it was a less ‘controversial’ emotion - people have a universal distaste for the Brexit aftermath - compared to other emotions such as anger which could be perceived as misdirected. This in turn implies the correlation might be due to disgust comments being biased towards discussing less contentious topics. However, Figure X probably disproves this- general and disgust comments share over 40 out of the 50 most common non-emotional words, with almost no differences in the log percentage usage rate between shared words. Therefore, the results imply it is the feeling conveyed rather than the topics discussed that increased the average scores of disgust-conveying comments.  
# 8.Conclusion 

## What is Starcraft II?
