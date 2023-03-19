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

## Models ad results

