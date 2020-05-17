---
title: "E-commerce Analysis"
date: 2020-04-20
tags: [AWS, SQL, visualization]
header:
  image: "/images/fraud.jpg"
excerpt: "AWS, Machine Learning, E-commerce Analysis, Data Science"
mathjax: "true"
---

# E-commerce Analysis

## Project Description

* After a deep dive into the 8 datasets, the rating score for each observation is an interesting perspective to do the analysis. Therefore, we would like to know what are the main drivers to the bad reviews and good reviews. Before the analysis, we did a couple of data visualizations and manipulations which can give us an overview about the problem we are going to solve. We would like to focus more on the delivery time and the product information, because we expect these features may affect the reviews rating score more significantly than other features. 

* After deciding the problems, we planned to give some recommendations to the sellers that could increase their ratings, maybe by decreasing the delivery time and put more information about their product. 


## Data and data prep process

* Join the tables together with orderid, sellerid, productid, customerid in R.
* Convert the character type of date variables to datetime variables with Pandas in python.
* Create new variables
    * Explanatory variables: Delivery time, Early arrival
    * Response Variable: Score 5 or not
* One Hot encoding categorical variables: product category and seller state


## Analysis Approaches & Analysis Results

* First of all, we build a baseline logistic regression model with all actionable features (except for sales and average scores, because these two features are not something we can know even before the product itself, and not something we can adjust).

* Features we selected: Delivery_time, Delivery_late, Product_category_name, Product_description_lenght, Product_photos_qty, Seller_state

* This model ended up with AUC of 0.63
<img src="{{ site.url }}{{ site.baseurl }}/images/ecommerce/pic1.jpg" alt="">

* However, it may not be the best method to one-hot-encode all categorical features. There are a huge number of product categories and seller states. Therefore, we decided to do some feature transformation on it. As we can see here, according to the average proportion of good reviews, the product categories can be divided into 3 parts, and states can also be divided into 2 parts. 

* Category names: divide into 3 parts, as High Medium and Low.
![alt]({{ site.url }}{{ site.baseurl }}/images/ecommerce/pic2.jpg)

* States : divide into 2 parts, as High and Low.
![alt]({{ site.url }}{{ site.baseurl }}/images/ecommerce/pic3.jpg)

* Then we come up with a simplified logistic regression model. AUC decreases a little bit, which may be caused by loss of information due to feature transform. 
    1. Features: Delivery_time, Delivery_late, Product_description_lenght, Product_photos_qty, State_high, State_low, Cate_high, Cate_med, Cate_low
    2. ![alt]({{ site.url }}{{ site.baseurl }}/images/ecommerce/pic4.jpg)


* We also built a Neural Network model to give us more insights. With all features put into the model, the overall AUC increased upto 0.72, which means sales and average score are really important features to review prediction. 

![alt]({{ site.url }}{{ site.baseurl }}/images/ecommerce/pic5.jpg)


## Challenges and solution

* Feature selection:
    1. Select the most important 50% features: using the feature selection method in sklearn packages of python. 
    2. Feature Engineering: divide category and states into several classes

## Insights gained

* Based on the logistic regression results, importance of all actionable features are listed here. As we can see, Despite of historical scores and sales, the number of product photos is the most important feature. More photos make people more satisfied. 
* Higher Delivery Time, worse score. Several Categories and states have lower scores, customers might be more picky than usual. Lastly, Delivery late really makes people upset

## Recommendations:
* Photo Numbers: Put more photos on your product page, make it clear and specific
* Delivery: Decrease delivery time as much as possible. People are very sensitive about delivery late while much more tolerant than common delivery, but still it works
* Categories and States: customers in several categories and states might be more picky than usual, so pay more attention

* Future work
    1. Further analysis on review contents, such as word frequency and topic modeling.
    2. Gather more customer information as predictor variables.
    3. Gather more product related information, such as price. 
 


[Presentation fil and python code is here](https://github.com/siyulai100/E-commerce)
