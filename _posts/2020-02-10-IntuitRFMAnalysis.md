---
title: "Customer Analytics-Intuit prediction"
date: 2020-04-20
tags: [Customer Analysis, R,Python, Neural Network, RFM,Logistic Regression, visualization]
header:
  image: "/images/laptop.jpg"
excerpt: "R,Python, Neural Network, RFM,Logistic Regression, visualization"
mathjax: "true"
---

[Code and Details in github](https://github.com/siyulai100/CustomerAnalytics_Intuit)

## Project Description

* Predicted email name list of second wave advertisement based on existing results.
*  Build a model to leverage historical information to predict future likelihood, to optimize return revenue. Used an ensemble method by comparing 5 different models and choosing the model with highest net profit to predict the Email name list.
* Evaluated the predictive performance based on the profit, ROME, Lift, Gain, AUC of models. Extensively tuned the parameters in the model to improve the predictive performance. 
* Identified the business insights of different models via parameter analysis and data visualization in Python and R. 
* By using the logistic regression & NN model to target customers, we can gain 62.25% of buyers by targeting 25% of the customers. 

## How we developed your predictive models, and discuss predictive performance for each model

We selected to use five types of models, namely, RFM sequential, logistic regression, logistic bootstrap, neural networks, and neural networks bootstrap. 

![alt]({{ site.url }}{{ site.baseurl }}/images/intuit/pic1.jpg)
![alt]({{ site.url }}{{ site.baseurl }}/images/intuit/pic2.jpg)

**Sequential RFM:** For the sequential RFM model, we created five deciles for the recency variable and created five deciles within each recency decile for frequency and monetary. 

**Logistic regression:** A review of the distribution of all of the variables, we found out that monetary and purchsince are slightly skewed to the right. Therefore, a log transformation in the logistic regression would allow the model to be more valuable both for making patterns in the data more interpretable and for helping to meet the assumptions of inferential statistics. However, the log-transform on skewed variables does not make our model more accurate. Besides, we also tried lower bound logistic regression, but it does not perform well because it filters out more potential customers.

**Neural network model (Python):** For the neural network model, we transformed the two categorical variables res1_yes, gender_male into numeric variables 0 and 1. We also transformed zip_bins into integers for convenience of neural network analysis. We standardized and transformed the independent variables to be evenly weighted in these hidden layers. We found the parameters with the highest AUC score from the model ‘MLPClassifier’ from ‘sklearn’ package by grid search with cross validation equal to 5. Our parameters are hidden_layer_sizes, alpha, beta_1 (drop-out layer),beta_2 (drop-out layer), activation function, number of hidden layers and number of nodes in each layer. Our best parameter is {'activation': 'tanh', 'alpha': 0.05, 'beta_1': 0.5, 'beta_2': 0.9, 'hidden_layer_sizes': (4, 4)}, and the best AUC score is 0.7169. We applied our best NN model on both the train and test dataset. The profit of the test dataset after applying our NN model is $32,393.28, lower than logistic model and R NN model

**Neural network model (R):** For the NN model in R, we chose logistic regression as our activation function because it allows us to observe the effect of the transformation in our input variables directly. For the feasibility of NN, we can only test the parameters of the NN model step by step. In the beginning, we tried only one hidden layer and ran a for loop (range from 1 to 12) to test how many nodes could generate the result that has the highest profit. However, the result was out of our expectations. The profit became lower when we increased our layer size after size was larger than 5. Then we were figuring out the optimal decay(dropout) by running a cross-validation neural network. Finally, we compared those size-decay combination and selected the optimal model with size = 5, decay = 0.05. 

**Predictive performance:** For all three models’ predictive performance, we created a confusion matrix to compare their accuracies, true positives, AUCs. Among all models, the model that has the highest model prediction accuracy is the neural networks model (0.72) and followed by RFM and logistic regression model (0.71). It means that 72% of all outcomes that were correctly predicted as either positive or negative. The model that has the highest true positives is logistic regression bootstrap model (0.90). It means that 90% of which is the proportion of positive outcomes in the data that received a positive prediction. We calculated the area under the curve for neural networks. The decay is 0.05 and the number of notes in the hidden layer is 5. The optimal AUC is 0.7543 for the NN model using both R and Python. The AUC from logistic regression is 0.754, which is very similar to that from the NN model. AUC of 0.754 means that the probability that pred(x) > pred(y) where x is a randomly selected buyer and Y is a randomly selected non-buyer. 

## Compare and evaluate different models?

* Out of all RMF models, namely, we developed five models: no target, independent RFM, sequential RFM, independent RFM lower bound and sequential RFM lower bound. The model that generates the highest profit is the sequential RFM model ($33,498).
On top of the logistic regression and NN models, we developed the bootstrap models to eliminate the random noise/error.  
* In order to compare three models, we adopted model performance metrics which include profit, lift, and gains. Among all, wave-1 profit is the most important metric for model comparison. We found out that the model that generates the highest profit ($38,613) is the logistic regression model,  which is slightly higher than those of the second ranking logistic bootstrap ($38,209), and third ranking NN model ($38,098). 
* Additionally, we calculated cumulative gains and cumulative gains for the logistic regression model. According to the cumulative lift chart, we can see that targeting on the top 15% decile of customers is expected to yield 3 times the proportion of buyers compared to using no targeting at all to select customers. According to the cumulative gains chart, we can see that by using the logistic regression model to target customers, we can gain 62.25% of buyers by targeting 25% of the customers. 
* Regarding the NN model, the AUC of the optimal model is 0.7543, and it generates a profit of $38,098. Likewise, we applied the same logic to NN bootstrap models and the estimated profit of this model is $38,082. In summary, we believed that the logistic regression model is the most appropriate model for the Intuit case.

##  Criteria I use to decide which customers should receive the wave-2 mailing?

* We will send wave-2 emails to the customers if the following criteria is met: 
    1. The predicted response rate * 0.5 is bigger than the break-even response rate
    2. Among the people who meet the criteria a), choose their res1 = No


## Insights about the business are likely to upgrade. 

* The businesses that are likely to upgrade have the following characteristics, in this order:
    1. A business that recently upgraded from version 1 to version 2 of Quickbooks 
    2. A business that purchased directly Quickbooks version 1 and is currently at version 1
    3. A business that owns a tax products   

- An odds ratio of 1.259 means that a one business increases in number of orders increases the odds of upgrading from version 2 to version 3 by a factor of 1.259 (or 25.9%)

- An odds ratio of 1.001 means that a one business increases in purchase dollar increases the odds of upgrading from version 2 to version 3 by a factor of 1.001(or 0.1%)

- An odds ratio of “ver_up | 10” 2.182 means that one more business increase from who directly purchased the version 1 Quickbooks than directly purchased the version 2 Quickbook increases the odds of upgrading from version 2 to version 3 by a factor of 2.182 (or 118.2%). 

- An odds ratio of “ver_up | 01” 2.702 means that one more business increase from who recently upgraded from version 1 to version 2 than directly purchased the version 2 Quickbook increases the odds of upgrading from version 2 to version 3 by a factor of 2.702 (or 170.2%). 

- An odds ratio of “owntaxprod” 1.356 means that one more business that owns tax products increases the odds of upgrading from version 2 to version 3 by a factor of 1.356 (or 35.6%). 

- For future prediction, customers who stay in version 1 are more likely to upgrade to version 3 compared to those in version 2 currently.  
