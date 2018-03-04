# Project 3: Deliverable II

[Project Description](https://www.cs.usfca.edu/~mmalensek/courses/cs686/projects/project-3.html)

[Collaboration Plan](collaboration-plan.md)

---

# Analysis: 
## [How does business popularity relate to the location of its neighbourhood For example, Richmond, Golden Gate Park, Market Street, and lesser 'hip' neighbourhoods like Glen Park, Excelsior?](https://github.com/cs686-bigdata/p3-d2-bluedragonz/blob/master/Ash%20Analysis.ipynb)
Our assumption is, if a restaurant is in a popular neighbourhood, its review counts will be more, and if a restaurant is in a lesser known or residential neighborhood, the review counts will tend to be less. 

A higher number of reviews for a business/restaurant indicates that more people have visited it and a fewer number of reviews mean that fewer people have visited it. For the purpose of my analysis, I am using the review counts and address attribute for the dataset to determine the popularity of a certain restaurant. 

I discovered that although there is a ‘neighborhood’ attribute in the dataset, it is almost empty for most of the data points, so i decided to use the address attribute instead.

Following is a graph that shows the number of review counts for both popular neighbourhoods and the not so popular ones.

**Graph of review counts for Market Street Businesses**

![Market_Street](imgs/MarketStreetGraph.png)

**Graph of review counts for Businesses in Downtown**

![Downtown](imgs/DowntownGraph.png)

**Graph of review counts for businesses in Excelsior**

![Excelsior](imgs/ExcelsiorGraph.png)

It can also be inferred that popular neighbourhoods tend to have more restaurants and the non popular ones tend not to have many!

<br>

## [How does an influential user affect the check-in rate of a business?](https://github.com/cs686-bigdata/p3-d2-bluedragonz/blob/master/Spark_Yelp_Analysis_Chai.ipynb)
We want to find out if reviews left by influential users (defined here as having a large number of followers) affects the average rating for a particular business.

**For starting off we will pick this approach:**
1) Pick an influential user
2) Look at businesses where he/she left a review
3) Find the nature of the review, whether positive or negative
4) Find a trend for the reviews for the business before and after the 'influencer' posted their review.

**Result:** <br>
We start the analysis with user_id: 37cpUoM8hlkSQfReIEBd-Q with 6087 followers, but interestingly this influencer did not leave a lot of reviews, so we selected the next user with highest followers and termed them as our 'influencer'.

For user with user_id: hizGc5W1tBHPghM5YKCAtg with 2344 followers
We take a summary of 4 businesses where he/she left a review, and analyze the review trend before and after the influencer review.

We obtain the following analysis:

![influential_user](imgs/influential_user.png)

We observe that businesses where the influencer left a positive review of 5 stars, had a increase in their average rating, and businesses where the influencer left a negative review of 1 star, had a decrease in their average rating following the influencer review. For a rating in between the two extremes, were mixed, as for 4 stars the average review rating actually decreased post review.

<br>

## [Analyze user's review type based on their review feedback.](https://github.com/cs686-bigdata/p3-d2-bluedragonz/blob/master/Review%20Feedback.ipynb)
We want to find out how are reviews by influential user tend to be based on Yelp’s category of reviews.

**Approach:**
1) Pick an influential user
2) Filter reviews left by the user
3) Show the proportion of each type of reviews with data visualization
4) Show the proportion of each type of compliments received by user with data visualization

**Result:**<br>
For user with user_id: hizGc5W1tBHPghM5YKCAtg with 2344 followers

**We obtain the following analysis:**

![compliment_rcvd](imgs/compliment_rcvd_pie.png)

![review_feedback](imgs/review_feedback_pie.png)

As we can see from two charts above, useful and plain are the two type that the user’s reviews and compliments received tend to be, so we might be able to say this person is pretty legit on giving professional reviews!

<br>

## [Sentiment analysis and classification of user reviews.](https://github.com/cs686-bigdata/p3-d2-bluedragonz/blob/master/User%20Review%20Analysis.ipynb)
Using Spark's ML package, we created a classification model that identifies reviews as positive or negative based on their content. To preprocess the reviews, the model first tokenizes the text into vectors of words and filters out unimportant, common words (i.e. "the", "that", "and"). It then creates a vector for each review that holds a frequency of each word in the training data. For example, if "yummy" was seen 302 times in the training data, it would be represented by 302 in the vector. Typically, less common words in a text corpus are the terms that carry the meaning and sentiment behind a sentence. Thus, the model then assigns lower weight to words that have higher frequency, and higher weight to those with lower frequency, following the concept of [*Term Frequency - Inverse Document Frequency*](https://en.wikipedia.org/wiki/Tf%E2%80%93idf) (TF-IDF). For classification, the model uses logistic regression with elastic net regularization. 

*Additional Data Info:*
- Total Number of Reviews: 4,736,897
- Number of Training Reviews: 2,842,323 (60%)
- Number of Validation Reviews: 1,420,849 (30%)
- Number of Test Reviews: 473,725 (10%)
- Since the model uses supervised learning, each review is pre-labeled as positive/negative based on the number of stars given by a user: 
    + **positive:** stars > 3
    + **negative:** stars <= 3

### Results: 
After tuning regularization parameters, the model performed with 89% accuracy on the test dataset. 

![confusion_matrix](imgs/sentiment_conf_matrix.png)

From the confusion matrix above, we can see that the model identified 94.2% of all positive reviews in the test data correctly, and 78.9% of negative reviews correctly.

<br>

Here's an example of a review classified as **positive**:

*"Matts feels like home. The tables remind me of snack time in Grandma's kitchen, the salt and pepper shakers remind me of the ones that sat on my neighbor's counter in her collections.... even the slightly wobbly leg of the chair reminds me of my college apartment furnished with family castaways and thrift shop treasures. \n\nREAL food comes from a place that feels so much like home... by real, i mean... real eggs, real butter, real sausage.... \n\nFood at Matt's is pure and innocent... Pancakes with butter. Eggs with potatoes and bacon. Classic. \n\nyum."*

<br>

Here's an example of a review classified as **negative**: 

*"This place has received a lot of hype, so be prepared to wait.\nand wait.\nand wait.\n\nTo make the trip more enjoyable:\n- don't actually come hungry (or risk passing out in the lot from low-blood sugar)\n- show up at least hour earlier than you want to be seated then get on list\n- go hang out  at the farmers market across street while you wait\n- expect solid (but not mind blowing) food\n\nGo for the experience at least once, then find another breakfast spot."*





