# Retailrocket E-commerce User Purchase Prediction

---

## Problem Statement

An e-commerce company wishes to understand visitors behaviour on its site and the factors that drive these site visitors to make a purchase. This is so that they can better target the right audience and improve future online sales. 

For the aim of this project, the Retailrocket e-commerce dataset from <a href="https://www.kaggle.com/retailrocket/ecommerce-dataset">Kaggle</a> is used. The goal is to build and compare different binary classification models that would best predict the purchasing intention of visitors to this e-commerce site. The results and findings will then be presented to the stakeholders in the e-commerce company.

---

## Executive Summary

There are 2 notebooks for this Capstone project. The main one is "Retailrocket Ecommerce Purchase Prediction" and the second one is "Retailrocket E-commerce Purchase Prediction - Data Cleaning". The latter only covers the data cleaning for each of the 4 datasets from <a href="https://www.kaggle.com/retailrocket/ecommerce-dataset">Kaggle</a> - Item Properties 1, Item Properties 2, Category Tree and Events. Most of the product features in the Item Properties datasets are encrypted except for category id and product availability. Hence, only these two features could be used. The dataset used in the main notebook is the result of the cleaning and merging of the 4 original datasets.

Initial analysis of the merged dataset indicates that this is an imbalanced one, with 99% of sessions without a purchase. Furthermore, there are some abnormal users observed. These users have visited the site over hundreds of times and made over hundreds of purchases over a span of several months. As the dataset is based on less than 4 months of data, such behaviour is not normal. Hence, these users are excluded from the data and for further analysis. 

To understand the different types of users behaviour and to better predict users purchase intention, K-Means clustering is used to segment site users to different groups. This clustering is based on users activity and purchase level on the site - total sessions, frequency of purchase and size of purchase. The optimal number of cluster is found to be 7. These user groups will serve as a proxy for these visitors. 

It is expected that users in the high activity level group (very frequent visit and purchase) to be more likely to purchase. On the other hand, users in the low activity level group are expected to be less likely to purchase. Hence, identifying the different group of users based on their site behaviour would enable the company to provide a more differentiated marketing approach for each user group. This in turn may help to improve future online sales and minimize the cost that is associated with targeting the wrong audience.

Overall, 4 different models are tested. These models are Logistic Regression, XG Boost, ADA Boost and Random Forest. These models are run multiple times using GridSearch Cross Validation to find the optimal hyperparameters for each model that would maximize F1 score. The models are then run again for the final time with their respective optimal hyperparameters. F1 score will be used as the metric to compare the performance of the different models.

---

### Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**group0**|*integer*|train, test, df|A dummy variable to indicate whether the users belong to group 0. If the value is 1, then yes. Otherwise, no.| 
|**group1**|*integer*|train, test, df|A dummy variable to indicate whether the users belong to group 1. If the value is 1, then yes. Otherwise, no.| 
|**group2**|*integer*|train, test, df|A dummy variable to indicate whether the users belong to group 2. If the value is 1, then yes. Otherwise, no.| 
|**group3**|*integer*|train, test, df|A dummy variable to indicate whether the users belong to group 3. If the value is 1, then yes. Otherwise, no.| 
|**group4**|*integer*|train, test, df|A dummy variable to indicate whether the users belong to group 4. If the value is 1, then yes. Otherwise, no.| 
|**group5**|*integer*|train, test, df|A dummy variable to indicate whether the users belong to group 5. If the value is 1, then yes. Otherwise, no.| 
|**group6**|*integer*|train, test, df|A dummy variable to indicate whether the users belong to group 6. If the value is 1, then yes. Otherwise, no.| 
|**friday**|*integer*|train, test, df|A dummy variable to indicate whether the session occurs on a Friday. If the value is 1, then yes. Otherwise, no.| 
|**saturday**|*integer*|train, test, df|A dummy variable to indicate whether the session occurs on a Saturday. If the value is 1, then yes. Otherwise, no.| 
|**office_hours**|*integer*|train, test, df|A dummy variable to indicate whether the session occurs within 8 am to 5 pm. If the value is 1, then yes. Otherwise, no.| 
|**avail_in_cart**|*float*|train, test, df|The percentage of items in the cart that are available.| 
|**tot_view**|*integer*|train, test, df|The total number of items viewed during a particular session.| 
|**cat_view_diff**|*float*|train, test, df|A scaled value to show the difference in the items being viewed (scaled between 0.005 and 1, with 1 indicating that all items viewed come from different categories).| 
|**session_duration_m**|*float*|train, test, df|The duration during which there are regular active interactions coming from a user on the website.| 

---

### Conclusions

Generally, all of the models that have been tested have low F1 score due to low precision. On the other hand, these models have high recall. This means that these models are able to capture the majority of actual purchasing customers. However, given that the precision is low, it also means that most of the users that are classified as purchasing customers will in fact not purchase. 

As this is an imbalanced dataset, with the positive being in the minority class, there are many negative examples that could become false positives. These false positive cases seem to be mostly driven by the misclassification of users from the cluster group 7. These are users who are found only in the test set. Thus, indicating the lack of robustness of these models. Moreover, as the data contains many encrypted features that could not be used, some key information might have been missing in the modelling. The model performance might have been restricted as a result. Thus, resulting in high false positive cases and lack of robustness in the model. 

Based on the models that have been tested, the Random Forest model is deemed to be the best model to predict users purchase. The model has the highest F1 score out of all the models that were tested. Compared to the boosting models, Random Forest is more robust to outliers and seem to work better when dealing with an imbalanced dataset.

### Recommendations

Based on the results from the Random Forest model, timing, users engagement level and item availability are some of the key factors that drive users to make a purchase. Some of the recommendations to help improve future online sales include:

#### Avoid certain timing when launching short-term campaigns like flash sales

Avoid launching these short-term campaigns on Friday, weekends or from 8am to 5pm. Based on the analysis above, users activity level on the site is generally low during that period. Fewer purchases are made during that period compared to other periods.

#### Keep users engaged

Users who are more active on the site and spend a longer time on the site have a higher tendency to purchase. Hence, to improve users engagement, the company should clearly display the best performing or related content on the item pages. This would provide a glimpse of other items that the site provides and help to aid the users to navigate to other pages which might be of interest to them. 

#### Implement different marketing strategies to different user groups

Based on the K-Means clustering above, there are 7 different user groups. Each group seems to display different type of user behaviour. Some groups, like group 3, contain more active users. These users visit the site very often and also make frequent purchases. On the other hand, groups like group 0 do not engage much on the site and have not made any purchases. By being able to segment the users based on their site behaviour, the company would be able to provide a more differentiated marketing approach that is customized to the site behaviour of each group. This in turn may help to improve future online sales.

Examples of strategies that could be implemented:

- Group 3 (visit and purchase often) - Loyalty programs and market new products
- Group 0/group 5 (does not engage much on the site) - Provide aggressive price incentives

### Next Steps

The dataset for this project is limited as most of the information is encrypted. Thus, the lack of features might have restricted the model performance. Hence, for the next step, other information and data that are relevant and important in predicting users purchase should be incorporated. Adding more useful features to the model may reduce the false positive cases and improve the robustness of the model. Some of the useful data that should be incorporated include:

- marketing channels that led users to the site
- sales campaigns that drove users to the site
- purchase value

Moreover, with additional key information, the users segmentation should be refreshed to incorporate the missing key information. This may improve the relevance and importance of some of the clusters. For example, replacing purchase size with purchase value as one of the features in which the users are segmented on. 

Lastly, other models like Neural Network should also be tested. 

---

### Data Source

- [Kaggle](https://www.kaggle.com/retailrocket/ecommerce-dataset)


*Due to the large file sizes, the original and cleaned data sets can be found here https://www.dropbox.com/sh/knwwjcmntjzkhy1/AABwtz3Gt2lLpYvMmOMWJjAaa?dl=0
