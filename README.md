# EL_project: 
The project is made up by two parts. The first one is the prediction of Airbnb prices in New York City using ensamble methods.
The second one is the implementation from scratch of a decision tree. 

In this repository the following files are available:

`AB_NYC_2019.csv` : file containing the data about the airbnb prices.

`NEW_NY_bnb_pricing.ipynb`: notebook where our project has been implementes

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


## Decision tree implementation
