# Time-Series-Forecasting-ML-Project
## Description
## Step 1 - Code provided in Jupyter Notebook file
## Step 2 - Analysis and service implementation
### What ML model (algorithm) did you use in Step 1 and why?
Initially, I started with a linear regression model, given its simplicity and ease of interpretation. Linear regression also serves as a good baseline model. However, since linear regression is not often suitable for time series forecasting, I wanted to experiment with more advanced models. I proceeded with gradient descent boosting because it can capture complex non-linear relationships and typically provides high accuracy. Random forest was chosen for its ensemble capabilities and resistance to overfitting. I also experimented with ARIMA and SARIMA for their time series forecasting capabilities, considering sales data inherently has time dependencies.
### What features did you use as input for this ML model and how they were prepared from raw data?
The original dataset provided includes features such as 'date', 'store_nbr', 'family', 'sales', and 'onpromotion'. Through feature engineering, I scaled features to normalize their range. Additionally, I performed one-hot encoding over the 'family' feature. 'family' has 20 different categorical variables, resulting in an increase of features from 5 to 21.
### What is the RMSLE metric for the dummy model?
Here, the dummy model is the linear regression model and RMSLE is obtained as 0.29
### What is the RMSLE metric for the developed model?
RMSLE value for the gradient descent boosting is obtained as 0.28

Root Mean Squared Logarithmic Error is calculated by applying log to the actual and the predicted values and then taking their differences. RMSLE is robust to outliers where the small and the large errors are treated evenly. It penalizes the model more if the predicted value is less than the actual value while the model is less penalized if the predicted value is more than the actual value. It does not penalize high errors due to the log. Hence the model has a larger penalty for underestimation than overestimation. This can be helpful in situations where we are not bothered by overestimation but underestimation is not acceptable.

Thus, in applications like sales forecast, and inventory stock it is preferable to choose the RMSLE metric over the other metrics.
### What other metrics do you think could be useful for this model evaluation?
Besides RMSLE, other potential metrics include:
 - Root Mean Squared Error (RMSE): This metric provides the square root of the average squared differences between predicted and actual observations. A lower RMSE indicates a better fit to the data.
 - Mean Squared Error (MSE): It represents the average of the squared differences between predicted and actual values. Lower values of MSE indicate better fit models, but it might be more sensitive to outliers than other metrics.
 - Mean Absolute Error (MAE): MAE calculates the average of the absolute differences between the predicted and actual values. It gives a linear penalty to the errors, making it more interpretable since it provides the average error in the same unit as the target variable.
### Provide the design of prediction model service implementation (Step 2)
#### Service Overview:
The prediction service will be a scheduled automated system, making use of ETL (Extract, Transform, Load) principles. The goal is to fetch data, run the model, and save predictions seamlessly.
#### Service Design & Workflow:
Data Extraction:
 - Automated Extraction: Use a scheduled job (via tools like Cron or Apache Airflow) to automatically extract the previous day's sales data from the MySQL database at 11:00 p.m. daily. A Python script leveraging a library like SQLAlchemy or PyMySQL can accomplish this.
 - Data Transformation: Once the data is extracted, transform it to the required format that the ML model expects.

Model Prediction:
 - Load Model: The ML model developed in Step 1 will be serialized (using libraries like Pickle) and stored. Every day, the prediction service will load this serialized model.
 - Run Prediction: Feed the transformed sales data from the previous day into the model to get the sales prediction for the next day for each store_nbr and family.

Data Loading:
 - Automated Loading: The generated predictions will be written back into the MySQL database in the required format. This ensures that by 1:00 a.m., the database will have the necessary predictions.
 - Logging & Monitoring: Log the success/failure of each step. If any step fails, an alert will be sent to the admin or the concerned team to take necessary actions. This ensures that any disruptions can be promptly addressed.

Service Health & Maintenance:
 - Monitoring: Use monitoring tools to ensure the health and uptime of the service.
 - Error Handling: The system will have error-handling mechanisms in place to gracefully handle any unexpected errors, ensuring that the database isn't populated with incorrect predictions. In case of failure, a backup strategy like using the last known good prediction can be utilized as a fallback.
 - Updates: When the model is retrained or updated, the serialized model file used by the service will be replaced with the newer version.

Assumptions:
 - The system hosting the service has the necessary resources and permissions to read from and write to the MySQL database.
 - There's an alerting mechanism in place to notify system administrators of any service disruptions.
 - The model doesn't take an exorbitantly long time to make predictions, ensuring that the 1:00 a.m. deadline is met.

By designing the service in this manner, we ensure that human intervention is minimized, the predictions are timely, and there's room to scale and expand the system as needed.
