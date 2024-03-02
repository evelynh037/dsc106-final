# DSC106 Final Project Writeup
## Project Overview:
	The presidential election in 2016 between the republican candidate Donald Trump and democratic candidate Hillary Clinton has been one of the elections in recent decades that received most attention, and ended in the result of Trump winning in electoral votes and Clinton winning in popular votes. A crucial aspect of their campaigns was the use of Twitter as a primary communication tool. In this project we are going to analyze and dive into the reasons for the electoral results of the two candidates by analyzing the topics they focus more about in the tweets they posted during the election and interpret how the difference in the topic they pay attention to might have an impact on the results. We will be using the following dataset that contains the 3000 tweets from each candidate during the election period (https://www.kaggle.com/datasets/benhamner/clinton-trump-tweets), and we will be analyzing the frequency of certain keywords in their tweets.

## What has been done so far (Prototype):
	We have finished processing the dataset in which the tweets are tokenized and the keywords are kept and processed into categories related to different areas of political concerns. We have also transformed the dataset with grouping and other aggregations to export new csv files that are convenient to be read in svelte. As far as the prototype web page of this project is concerned, currently, we have established the general structure of the webpage, in which the layout is set to contain explanatory text on the right panel and the corresponding interactive visualization on the left panel. There’s also descriptive text for all the sections that we plan to include later in our webpage. We have also finished the interactive plot at the bottom of the webpage that allows readers to explore the frequency of different words appearing in each candidate’s tweets to make comparisons and retain insights about the areas they put more effort to campaign. Also, the webpage is deployed through github.

## Most Challenging Part to Design:
	The most difficult part of the project is to include graphical comparisons between different words’ occurrences in the tweets on one plot and to allow readers to select words they think are related in political topics to draw conclusions. This is difficult because we try to implement a graph that the readers can interact with in an open-ended manner (they can search whatever words they prefer in a text box, and we will allow they to compare multiple words at the same time on one plot with a limit up to 3 different words, etc.). We spent a lot of time discussing the interface that would most effectively convey the message of the difference in their amount of campaign on different topics to the readers, so that inferences can be drawn in why they win or lose in the poll. Also, it is technically hard for us to implement the dynamic graph in which we try to keep it up to date when users type in or change the word in a search textbox, as there are not a lot of similar examples we can refer to. 
