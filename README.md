# DSAI Midterm Project: Kaggle Competition
### [Predict Future Sales](https://www.kaggle.com/c/competitive-data-science-predict-future-sales/overview)

![](https://i.imgur.com/KufvSwl.png)

## Description
This challenge serves as final project for the "How to win a data science competition" Coursera course.

In this competition you will work with a challenging time-series dataset consisting of daily sales data, kindly provided by one of the largest Russian software firms - 1C Company. 

We are asking you to predict total sales for every product and store in the next month. By solving this competition you will be able to apply and enhance your data science skills.

## File descriptions
- sales_train.csv - the training set. Daily historical data from January 2013 to October 2015.
- test.csv - the test set. You need to forecast the sales for these shops and products for November 2015.
- sample_submission.csv - a sample submission file in the correct format.
- items.csv - supplemental information about the items/products.
- item_categories.csv  - supplemental information about the items categories.
- shops.csv- supplemental information about the shops.

## Data fields
- ID - an Id that represents a (Shop, Item) tuple within the test set
- shop_id - unique identifier of a shop
- item_id - unique identifier of a product
- item_category_id - unique identifier of item category
- item_cnt_day - number of products sold. You are predicting a monthly amount of this measure
- item_price - current price of an item
- date - date in format dd/mm/yyyy
- date_block_num - a consecutive month number, used for convenience. January 2013 is 0, February 2013 is 1,..., October 2015 is 33
- item_name - name of item
- shop_name - name of shop
- item_category_name - name of item category

## Method
Refer to a public kernel: [Feature engineering, xgboost](https://www.kaggle.com/dhimananubhav/feature-engineering-xgboost), which can achieve 0.90646 of RMSE. 
    Following are detailed steps of feature extraction.

- load data
- heal data and remove outliers
- work with shops/items/cats objects and features
- create matrix as product of item/shop pairs within each month in the train set
- get monthly sales for each item/shop pair in the train set and merge it to the matrix
- clip item_cnt_month by (0,20)
- append test to the matrix, fill 34 month nans with zeros
- merge shops/items/cats to the matrix
- add target lag features
- add mean encoded features
- add price trend features
- add month
- add days
- add months since last sale/months since first sale features
- cut first year and drop columns which can not be calculated for the test set
- select best features
- set validation strategy 34 test, 33 validation, less than 33 train
- fit the model, predict and clip targets for the test set

## Result
![](https://i.imgur.com/Q2YwdSa.png)
