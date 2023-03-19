# EL_project: 
The project aims at predicting the Airbnb prices in New York City using ensemble methods.


In this repository the following files are available:

`AB_NYC_2019.csv` : file containing the data about the airbnb prices.

`NEW_NY_bnb_pricing.ipynb`: notebook where our project has been implemented.

## NY Airbnb Prices 
The implementation of the first part can be found in the Notebook `NEW_NY_bnb_pricing.ipynb`

The project uses the data from the file `AB_NYC_2019.csv`, available on this repository.
In order to start with the analysis, the data needs to imported as a dataframe with the following line of code: 
```
dt =  pd.read_csv('/content/AB_NYC_2019.csv')
```
The notebook is made up by different sections. In the first part "Data exploration" there will be different analysis performed on the data to have a better grasp of the characteristics of the data.

The second part is the feature engineering and preprocessing, where the variables are transformed to make more appropriate for modeling and new variables are transformed.

The last part is modeling, where a variety of models are tested.

## Data Exploration

To predict Airbnb prices in New York City, we analyzed the dataset containing information about Airbnb listings in NYC in 2019. We focused on variable types, missing values, and variable distributions. We dropped variables without predictive power, encoded categorical variables, and removed outliers from continuous variables.

## Feature Engineering and Preprocessing

We performed the following preprocessing steps based on our observations from the data analysis:

- One-hot encoding: we applied one-hot encoding to columns such as `neighbourhood_group`, `neighborhood`, and `room_type` as we found them to be highly related to the price. We also performed one-hot encoding in categories for variables such as `minimum_nights`, `availability_365`, and "calculated_host_listings_count`.
- Quantile encoding: we transformed the `number_of_reviews` column into quantile values instead of normalizing to avoid the model being influenced by the extreme values.
- Variable capping: we replaced outliers in the `reviews_per_month` column with the upper whisker value as it was unrealistic for a variable to have more than 50 reviews per month.
- Outliers dropping: we dropped the high values of the target variable `price` as we deemed that our model would not be able to predict them correctly.
- Other calculations: we created new columns such as `n_days` and `mean_price_neigh_room`.
- Handling missing values: we filled the missing values in the `reviews_per_month` column with 0 and in the `n_days` column with the median.
- Dropping features: we dropped some variables such as `id`, `name`, `host_id`, and `host_name` that had no more predictive value.


Thanks to the preprocessing, we created many variables to feed to the model (245 total), however not all of them can be of equal importance when it comes to making predictions, because of this, we performed feature selection on our models to select the most important features.
In Random Forest, GradientBoost, XGBoost, and Gradient Boosting Decision Tree We use extracted feature importance from each model, calculating the mean importance, then selecting only the features which scored above the mean importance. In Stacking model, we perform feature selection by extracting k best features from Linear regression model and ML Regressor and above average from Random forest.


## Models and results

### Models

The specific model flow is shown below:
![alt text](https://github.com/lucreziacerto/EL_project/blob/main/1111.png?raw=true)

In the model training phase, we used different potential algorithms to estimate their predictive power. We evaluated the performance of the models using several error metrics (MAE, MSE, RMSE) and goodness-of-fit (R^2 score). We used GridSearchCV to adjust the hyperparameters of the model yields and applied the following ensemble methods:

- Random Forest: Our baseline model trained on all features with n estimators=300, max features='sqrt', max depth=20, random state=18, gave a score of 0.596 (computed through cross-validation). After selecting 21 features using the threshold method, the score is 0.595.

- Gradient Boost: We achieved a score of 0.598 on our own testing data set with the default parameters. After GridSearchCV to tune hyperparameters, we got n estimators=300, max depth=5, min samples split=2, and learning rate=0.1, giving us the best score of 0.607 after cross-validation. By using the threshold method in feature importance, the score is 0.601 after selecting 71 features.

- XGBoost: We gained 0.588 on the first try. After feature selection and GridSearchCV, we achieved a score of 0.601 on our own testing data set and 0.598 on the test set. By using the threshold method on feature importance, the score is 0.601 after selecting 71 features.

- Gradient Boosting Decision Tree: We got a score of 0.54 on our own testing data set with default parameters. After GridSearchCV, n estimators=100, learning rate=0.1, max depth=3, and random state=100 gave us the best score of 0.599 after cross-validation. By using the threshold method on feature importance, the score is 0.599 after selecting 6 features.

- Stacking: We created a stacking ensemble using RandomForestRegressor and MLPRegressor, achieving a score of 0.605 on the test set. By using RFE to select linear regression features, we got a score of 0.605 on the test set. Selecting the features with importance higher than the average importance, we got a score of 0.595. Selecting the top k (k=30) features using SelectKBest with f regression scoring in MLRegressor, we got a score of 0.567 on the test set.

We studied the possible existence of overfitting through the use of learning curves obtained by cross-validation. The model selection process was carried out using the performance metrics obtained from the test dataset to identify the algorithm that performed best in predicting the dependent variable

### Results

The study analyzed the performance of different models in predicting real estate prices using a dataset with various features. The models' performance was evaluated based on their $R^2$ scores, which represent the proportion of the variance in the target variable explained by the model. The Gradient Boost model achieved the highest $R^2$ score of 60.7%.

Additionally, the study compared the mean absolute error (MAE) and mean squared error (MSE) of the models. The MAE indicates that, on average, the predicted price is off by $30, which is considered acceptable in the real estate industry. However, the MSE is much larger than the square of the MAE, which may be due to the presence of outliers whose actual prices are far from the predicted prices.

Furthermore, the study evaluated the performance of models with feature selection and found that they had similar performance to models that used all the features. This suggests that there are only a handful of variables with a high predictive value, and non-important variables can be dropped without significantly affecting the model's performance. This can make the pipeline more agile and efficient in an industrial setting.

## Conclusion 

The model with the highest performance is Gradient Boost, which achieved an impressive $R^2$ score of 0.607 and the lowest MAE and MSE. However, it should be noted that the model's predictive ability is limited as it lacks a crucial variable, the size of the apartment. Removing outliers helped alleviate the problem, but it persisted. Despite this limitation, the model's performance is still noteworthy. To improve the model's accuracy, we suggest adding more features to differentiate between different types of rental properties, such as the size of the room, number of bathrooms, or number of windows. Alternatively, separate models could be developed for each type of rental property if sufficient data is available.
