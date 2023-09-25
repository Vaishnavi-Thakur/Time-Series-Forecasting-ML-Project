## Assignment Description

The main goal is to develop a next-day sales prediction service.

To do this you need to:

1. Create a prediction model
2. Design a service that will return sales predictions for the next day.

## Data Supplied

You are given one CSV (comma-separated) data file train.csv (`/data/train.zip`): time series of features **store_nbr**,
**family**, **onpromotion** as well as the target daily **sales**.
- store_nbr - identifies the store at which the products are sold.
- family - identifies the type of product sold.
- onpromotion - gives the total number of items in a product family that was being
promoted at a store at a given date.
- sales gives the total sales for a product family at a particular store at a given date.
Fractional values are possible since products can be sold in fractional units (1.5 kg of
cheese, for instance, as opposed to 1 bag of chips).

The data is based on [this Kaggle competition](https://www.kaggle.com/competitions/store-sales-time-series-forecasting) (but simplified).

Please, don't use any other data from this competition or any other public data. Even if you do
that - it won't be evaluated.

## Expected results:

### Step 1. Create prediction model

For this step, you need to:
- create a dummy model, which will use the previous day's sales amount (for each store_nbr and family)
as next-day prediction.
- for the dummy model evaluate the RMSLE (Root Mean Squared Logarithmic Error) metric on all the
available days in 2016 and 2017 years.
- create an ML-based prediction model that will give better results (lower RMSLE error on the
same test dataset) than a dummy model.

### Step 2. Design a prediction service

It's not expected that you will implement actual service for this assignment. **No coding required for this step**,
but you need to provide a description (in free form) of how the model was developed on **Step 1**
could be used in production.

The model will be used in this scenario:

>All stores are operating from 9:00 am to 22:00 pm. At the beginning of each day (not later than
5:00 am) In the MySQL database we need to have predicted sales for this day for each store_nbr and
family. All the data for previous days' sales which was provided in train.csv is also stored in the
MySQL database. The data for previous days will be available from 22:00 pm.`

**You are not expected to design a database scheme.**

We understand that the service design could be different based on other requirements and
constraints that are not provided. You are free to make any assumptions if something is not clear from this assignment
description. 

Here is an example of a minimal model implementation design description you need to provide:

>The model will be operated as follows:
>1. We will create a Python script that will read the previous day's sales data from CSV (same format as train.csv) and
as a result, output another CSV with next-day predictions for each store_nbr and product
family type.
>2. Every day at 4:00 we will conduct these actions:
>- manually extract the previous day's data from MySQL database and export it to CSV.
>- manually run the Python script to create CSV with predictions.
>- manually insert predictions from CSV to MySQL database.

## Expected deliverables

Please upload all deliverables to this GitHub repo. You can create a subfolder for that.

The following deliverables must be submitted:
1. Python code with model training and evaluation on the test dataset (used on **Step 1**). The code
could be provided as a Python .py script/Jupyter Notebook/Google collab link.
2. Create a README.md file, containing answers to the following questions:
- What ML model (algorithm) did you use in Step 1 and why?
- What features do you use as an input for this ML model and how they were prepared from raw data?\
- What is the RMSLE metric for the dummy model?
- What is the RMSLE metric for the developed model?
- What other metrics do you think could be useful for this model evaluation?
- Provided design of prediction model service implementation (**Step 2**).
3. Any related files such as figures, images, etc...
