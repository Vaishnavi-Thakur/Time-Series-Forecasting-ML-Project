# Time-Series-Forecasting-ML-Project
## Description
## Step 1 - Code provided in Jupyter Notebook file
## Step 2 - Analysis and service implementation
### What ML model (algorithm) did you use in Step 1 and why?
Initially, I started with a linear regression model, given its simplicity and ease of interpretation. Linear regression also serves as a good baseline model. However, since linear regression is not often suitable for time series forecasting, I wanted to experiment with more advanced models. I proceeded with gradient descent boosting because it can capture complex non-linear relationships and typically provides high accuracy. Random forest was chosen for its ensemble capabilities and resistance to overfitting. I also experimented with ARIMA and SARIMA for their time series forecasting capabilities, considering sales data inherently has time dependencies.
### What features did you use as input for this ML model and how they were prepared from raw data?
The original dataset provided includes features such as 'date', 'store_nbr', 'family', 'sales', and 'onpromotion'. Through feature engineering, I scaled features to normalize their range. Additionally, I performed one-hot encoding over the 'family' feature. 'family' has 20 different categorical variables, resulting in an increase of features from 5 to 21.
### What is the RMSLE metric for the dummy model?
### What is the RMSLE metric for the developed model?

Root Mean Squared Logarithmic Error is calculated by applying log to the actual and the predicted values and then taking their differences. RMSLE is robust to outliers where the small and the large errors are treated evenly. It penalizes the model more if the predicted value is less than the actual value while the model is less penalized if the predicted value is more than the actual value. It does not penalize high errors due to the log. Hence the model has a larger penalty for underestimation than overestimation. This can be helpful in situations where we are not bothered by overestimation but underestimation is not acceptable.
Thus, in applications like sales forecast, and inventory stock it is preferable to choose the RMSLE metric over the other metrics.

While modeling, I have initially established Linear Regression as the baseline or dummy model, providing a benchmark for performance. The expectation was that more sophisticated models like Gradient Boosting, Random Forest, ARIMA, and SARIMA would surpass this baseline in terms of RMSLE. However, evaluations indicated that Linear Regression yielded the lowest RMSLE compared to the other models.

1. **Linear Regression as a Baseline**: Linear Regression served as the dummy model. Its simplicity was intended to provide a minimum performance benchmark.

2. **Developed Models**: Multiple models, including Gradient Boosting, Random Forest, ARIMA, and SARIMA, were tested. Surprisingly, these models did not outperform the baseline Linear Regression in terms of RMSLE.

    Here is a table of comparison of these metrics across the various models used in this assignment.
     ### Model Performance
    
    | Model              | RMSLE | RMSE | MSE  | MAE  |
    |--------------------|-------|------|------|------|
    | Linear Regression  | 0.33  | 1.01 | 1.01 | 0.53 |
    | Gradient Boosting  | 0.41  | 1.17 | 1.38 | 0.62 |
    | Random Forest      | 0.45  | 1.36 | 1.84 | 0.66 |
    | ARIMA              | 0.45  | 1.21 | 1.46 | 0.52 |
    | SARIMA             | 0.48  | 1.01 | 1.01 | 0.53 |

3. **Potential Reasons**: Several reasons could account for this:
   - The data might have an inherent linear relationship, making Linear Regression a suitable choice.
   - The chosen features might align better with linear models.
   - The hyperparameters or model configurations for the advanced models might require optimization.
   - The metric, RMSLE, emphasizes relative error, which could favor the strengths of Linear Regression for this dataset. It's entirely plausible that simpler models like Linear Regression can sometimes outperform more complex models in terms of RMSLE, depending on the nature of the data and the problem. However, this should be taken in context; there might be other metrics or considerations where complex models may have an edge. Also, the performance of sophisticated models like Gradient Boosting and Random Forest often depends on hyperparameter tuning, feature engineering, and other factors.

4. **Next Steps**: Refining features, and intensively tuning hyperparameters to determine if any model can surpass the performance of simple Linear Regression for this dataset.

### What other metrics do you think could be useful for this model evaluation?
Besides RMSLE, other potential metrics include:
 - Root Mean Squared Error (RMSE): This metric provides the square root of the average squared differences between predicted and actual observations. A lower RMSE indicates a better fit to the data.
 - Mean Squared Error (MSE): It represents the average of the squared differences between predicted and actual values. Lower values of MSE indicate better-fit models, but it might be more sensitive to outliers than other metrics.
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

### 3. Related Files and Images
#### Exploratory Data Analysis in Jupyter Notebook
The plots and visualizations pertaining to the exploratory data analysis are plotted in the Jupyter Notebook. This notebook provides detailed insights into the dataset, including trends, patterns, and statistical summaries.

![image](https://github.com/Vaishnavi-Thakur/Time-Series-Forecasting-ML-Project/assets/63786583/69b637c7-26b2-4900-839f-d972d892d942)
![image](https://github.com/Vaishnavi-Thakur/Time-Series-Forecasting-ML-Project/assets/63786583/20945a97-14b8-4974-b70b-6639a4d53e72)
![image](https://github.com/Vaishnavi-Thakur/Time-Series-Forecasting-ML-Project/assets/63786583/976ee895-1454-4653-b986-a680426d1e4c)
![image](https://github.com/Vaishnavi-Thakur/Time-Series-Forecasting-ML-Project/assets/63786583/19fd8229-7b3f-48dd-8da0-5d109f67de6f)
![image](https://github.com/Vaishnavi-Thakur/Time-Series-Forecasting-ML-Project/assets/63786583/facbb0d2-0e37-4ee8-96e8-e47a4ea28a0f)

#### Interactive Tableau Dashboard
Below are images from a simple interactive dashboard created in Tableau. These visualizations offer a user-friendly interface for exploring and understanding the data more intuitively.

##### Time Series Sales Data
![time-series](https://github.com/Vaishnavi-Thakur/Time-Series-Forecasting-ML-Project/assets/63786583/9785249f-da82-483e-9208-2405a258ab56)
This image displays the time series data, showcasing the sales trends over a specific period. It helps in identifying sales patterns and potential seasonality.

##### Variation of Sales in Each Store Over a Month
![store-family-month](https://github.com/Vaishnavi-Thakur/Time-Series-Forecasting-ML-Project/assets/63786583/ae0393f7-9b4f-4565-8503-4ad6ecf1d36b)
This visualization illustrates how sales vary across different stores over a single month, allowing for comparisons and insights into store performance.

##### Variation of Sales in Each Store Over a Period of Years
![store-family-year](https://github.com/Vaishnavi-Thakur/Time-Series-Forecasting-ML-Project/assets/63786583/3440eba5-a034-4aa9-9939-20b0b280d707)
This image highlights the changes in sales within each store over multiple years. It aids in understanding long-term trends and identifying growth or decline patterns.

##### Percentage Change in Sales of Each Family
![family-month-year](https://github.com/Vaishnavi-Thakur/Time-Series-Forecasting-ML-Project/assets/63786583/6b20221a-3559-42c0-8cbe-2b0dc1223366)
This visualization presents the percentage change in sales for different product families over time. It provides valuable insights into the performance dynamics of each family.
