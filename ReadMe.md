CLASSIFYING JAPAN TRAVEL POST FROM JAPAN LIFE IN REDDIT.COM
 
PROBLEM STATEMENT:
Classifying whether the post coming from japan travel or japan life Subreddit. This classification is done to improve customer satisfaction and to avoid missing of any information related to a particular post as they are poster under wrong subreddit. Reddit will be able to move the post under right category using this classification model.

Steps:
-Imported the libraries used in the coding

-Data Preprocessing
* maximum column display is increased to 999
* reading scraped Japan trip csv with pandas
* Checked for duplicates and deleted the duplicates
* Checked for the null values. Replaced the null values with space character in the posts
* Joined the title of the post and the actual posts together.
* Repeated the above steps for Japan life subreddit
* After that we got 996 posts for Japan travel and 998 posts for Japan life subreddit.
* Round 1 cleaning
   ...Following regex is used to extract the words from the raw data
      [A-Za-z]{2,}-[A-Za-z]+ this regex finds the words split by '-'
      [A-Za-z]+ this regex finds the words 
      [A-Z]{2,} this regex finds the 2 or more capital letters together
   ...The extracted words are converted into lower case words
   ...Using stopwords some of the words are removed
* lemmatized the words from Round 1 cleaning
* stemming done on words from Round 1 cleaning
* stemming done also on lemmatized words.
* lemmatising and stemming reduced the words from 16404 to 12358.
* Eventhough some of the words lost the last few words and their meaning after stemming.It just gave us words that are unique and reduced 4000 words.
* So, I have used the words after lemmatizing and stemming as corpus.
* Using count vectoriser corpus is converted into document term matrix.

- EDA: 
* The top words are explored and wordplot is constructed with the top 50 words by frequency for both subreddit
* Venn2 wordplot is constructed to visualize the common words used between 2 subreddit.
* While analysing found that only about 1000 words out of 12358 words have considerable frequency for the           remaining words the frequency is less than 10.
* So only about 800 to 1000 words is supplied as max features.

-Modelling:
MODEL 1 LOGISTICS REGRESSION:
* Started modelling with logistics regression.
* fit and predict the data for max_features 800, 900 and 1000 under count vectorizer.
* The accuracy was better for 900 features, so I have used it.
* This model had a training accuracy of 99.56% but the accuracy and test data is only 90.72%
* The difference is about 9% and this shows that the model overfits with training data.


MODEL 2 Multinomial Naive Bayes and TFID vectoriser:
* Used a pipeline and built a model with TFID vectoriser and Multinomial Naive Bayes.
* fit and predict the data for max_features 800, 900 and 1000 under count vectorizer.
* The accuracy was better for 900 features also for this model, so I have used it.
* This model had a training accuracy of 90.34% but the accuracy and test data is only 91.73%
* The difference is about 1% and this time the accuracy of test data is even better than training data.
* So used this as a final model.

-MODEL EVALUATION:
* I have used confusion matrix, Accuracy, classification report and AUC curve for model evaluation.
* Based on AUC curve both the model doesn't show high difference in the performance.
* But still Multinomial Naive Bayes with TFID vectoriser did show a slight higher performance.

-CONCLUSION AND RECOMMENDATION:

To classify the posts from japan travel and japan life subreddit, We have used 2 models. One is Logistics regression and the other is Multinomial naive bayes. Accuracy calculated from test data for both the model are quite similar and it is just more than 90%. But still I choose Multinomial naive bayes to be the better model as the accuracy on test data is even higher than on the training data. While, the accuracy on test data is 9 percent lower than on the training data. This shows the logistic regression model overfits on the training data.

The Multinomial naive bayes model has accuracy of 91.72%. Japan life and Japan travel have some top common words like Japan, Tokyo etc. The model maynot work well on the common topwords between both subreddit. 

Also to avoid posting under a wrong subreddit and to get customer satisfaction reddit could create a category countries and put the political, life based posting there and use the travel category for travel related subreddit.




