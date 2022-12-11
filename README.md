Osama Dabbousi, Shasta Narayanan, Sungjun Park

Professor Snyder

CS 505

December 12, 2022

**Stock Price Prediction using Tweet Sentiment Analysis**

**Abstract**

This project uses Tweet sentiment analysis to predict stock return changes. In terms of data sources, we used Twitter for the sentiment analysis aspect and stock market API call to gather percentage changes for these respective companies over a given period of time. To find which method of prediction would work best, we decided to test on a couple different models: Linear Regression, Naive Bayes, Logistic Regression, as well as a Neural Network Regression Model. Based on our results, we found that Tweets were poor predictors of the stock market changes, but of the models surveyed we found the Neural Network Regression Model to work best. Also, given the different methodologies, we found that using Word2Vec to preprocess the tweets was more ideal.

**Presentation of the results**

Putting ourselves in the shoes of an investment banking firm, we decided to find a solution to predicting which stock purchases they should make. We decided to use the sentiment analysis of tweets on various companies to predict future stock fluctuations for the following day. We have also worked with tweet data in class with our problem assignments, so we thought it made sense for us to use this method for data extraction. This problem is interesting because stock changes tend to be hard to predict, and many traders and economists try to find models to best figure out where a stock is going next. In addition, many stock prediction models are based on past changes in stock prices, but we decide to use the public viewpoint of companies to predict future stock fluctuations.

**Data Extraction**

In terms of data sources, we used Twitter for the sentiment analysis aspect and stock market API call to gather percentage changes for these respective companies over a given period of time. When testing different methods of prediction we decided to test a couple different models including, Linear Regression, Naive Bayes, Logistic Regression, as well as a Neural Network Regression Model.

To pull public company names and ticker symbols we scraped the top 100 NASDAQ companies from a Wikipedia article. Once we had this information, we ran these tickers through the finance module to extract percent changes in a one-month time frame for these respective companies. The next aspect required us to scrape tweets mentioning these companies from Twitter. In order to do this, we had to make use of the snscrape module rather than Twitter's API. The regular API call does not allow for pulling tweets from the past, but using this modified scraping tool, we were able to specify the exact time period we wanted. In our case, we collected 200 tweets for each of the 100 companies we were analyzing.

**Linear Regression Model and Sentiment analysis with probability using Flair**

The first method we decided to use was creating a linear regression model using sentiment analysis of the tweets using a tool called Flair and stock percent changes. With the extrapolated tweets, we calculated the sentiment for each, and the accuracy percentage. A positive sentiment value is represented with a positive number, and vice versa. Taking the average of all 200 tweets for each company, we imputed this data along with the stock percent change for that given month into a scatter plot and found the linear regression that fit the data. When plotting this data, we put the twitter sentiments on the x-axis, and the respective stock percent returns on the y-axis. From this, we were also able to calculate the Root Mean Square Error value to be able to compare this model with the other methodologies.

**Pseudocode**

-get list of top 100 companies from nasdaq

-scrape 200 tweets for each companies

-get stock change values for each company

-use flair to calculate positivity/negativity for each tweet

-find average positivity for company

-use linear regression to get line of best fit

-calculate RMSE based off line

![](RackMultipart20221211-1-9cpn2n_html_48a88e8691691f14.png)

**Linear Regression Model Output**

Figure 1 - Linear regression on stock and tweet sentiments. Clearly there is no correlation between the Twitter Sentiment and the Stock Percent Return. An interesting note on the graph is the extremity of tweet sentiments.

**Word2Vec**

We were concerned that reducing the tweets into a single positive/negative dimension would lose a lot of information that may be carried within the tweets, so we chose to use a more complex sentence embedding for the remaining models. In particular we chose to take the averaged Word2Vec vector for each of the tweets as inputs. This we hoped would lead to a greater spacial complexity, and would allow our future models to

**Logistic Regression**

Using sklearn we trained a logistic regression classifier on our data. Logistic Regression is a classification algorithm that is used to predict the probability of a categorical dependent variable. In order to use this method, we had to input in two parameters, x and y. For the x, we passed in the Word2Vec vectors that were mentioned in the section above. The dependent variable, y, we passed in our labels, -1, 0, or 1, representing the sentiment. Although our sentiment data contains more specific data, we had to truncate it to these labels since logistic regression requires discrete values rather than continuous. Once we fit our data to this regression model, we were able to extrapolate a Root Square Mean Error value allowing us to compare the results with the other methods.

**Neural Network Regression**

When it came to using Word2Vec, a fully connected neural network made the most sense as a regression model, since neural networks are well known for their ability to slice up high-dimensional spaces, and also because neural networks are especially good at regression tasks when compared to models like naive bayes, logistic regression or otherwise. We chose a fully connected network because their input format most suited the word vector format. Finally, we settled on root mean square error as the loss, and tuned the hyperparameters through some simple trial and error. Finally we found a simple network of four dense layers of size 256x512x256x128, and ReLU activation and light dropout throughout. Even still, we found that training the network seemed to be a game of guesswork, where loss values would bounce up and down without consistent change.

**Pseudocode**

-get list of top 100 companies from nasdaq

-scrape 200 tweets for each companies

-get stock change values for each company

-use flair to calculate positivity/negativity for each tweet

-tokenize tweets

-use Word2Vec to generate learn word associations

-fit logistic/NN model using Word2Vec vectors and sentiment labels (truncated labels for logistic model)

-calculate MSRE

**Comparative Results**

| **Model** | **Root Mean Square Error** |
| --- | --- |
| Linear Regression | 1.559 |
| Logistic Regression | 8.6 (61.5% accuracy) |
| Neural Network | 1.439 |

Figure 2- Comparison of Root Mean Square Error based on model

The graph above compares various models based on their Root Mean Square Error (RMSE), which is a normalized measure of the difference between the predicted values of a model and the true values. A lower RMSE indicates that the model is better able to accurately predict the true values. The results show that the Neural Network model has the best performance, with the lowest RMSE. Logistic regression has the worst performance. Since logistic regression is made for binary classification, we implemented positive or negative partitions and even then the model had a poor performance with 61.5% accuracy.

**Future Plans**

If given more time for the project, we would explore a wider range of input methods, including BERT and bag-of-words, and use more complex neural networks such as LSTMs. We would also incorporate larger and more diverse datasets to improve the model's accuracy and provide a more comprehensive overview of stock movements. Additionally, we would consider incorporating data from a wider range of companies, rather than just tech companies listed on the Nasdaq, to better reflect the overall stock market. However, our findings suggest that tweets are simply not a reliable indicator of future stock performance, and so other methods such as using past stock fluctuations to train the model may be more accurate.

**Team Contribution Statement (Agreed upon by all team members):**

Sungjun:

Worked on scraping tweet data, training the linear regression model and calculating tweet sentiments using Flair.

Wrote the comparative model results analysis, abstract, future plans and analysis of graphs and charts.

Shasta:

Worked on scraping tweet data, extrapolating stock percent changes for each respective company, calculating tweet sentiments using Flair, and training logistic regression model.

Wrote the abstract, presentation of the results, data extraction, Linear Regression, and Logistic Regression sections of this paper.

Osama:

Created tweet tokenizer, Word2Vec vectorizer, logistic regression model and neural network. Wrote sections of this paper discussing the Word2Vec and neural network.
