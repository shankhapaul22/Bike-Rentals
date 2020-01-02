# Context

Many American cities have communal bike sharing stations where you can rent bicycles by the hour or day. Washington, D.C. is one of these cities. The District collects detailed data on the number of bicycles people rent by the hour and day.

Hadi Fanaee-T at the University of Porto compiled this data into a CSV file, which you'll be working with in this project. The file contains 17380 rows, with each row representing the number of bike rentals for a single hour of a single day. It is included in the files as `bike_rental_hour.csv`.

# Objective

We will create a model to predict the number of bikes people rented in a given hours. We will predict the `cnt` column (the target) using all of the other columns as features, except for `casual` and `registered`.

# Process

We feature engineer a new column for the machine to understand that the hours of the day are relevant to each other. (i.e. Hours labeled 0 - 6 are considered in the morning and categorized together).

We choose Mean Squared Error(MSE) as our error metric and split the dataset into `train` and `test`.

We utilize the following models to find the best one for our objective:

- Linear Regression, with feature selection.
- Decision Tree, with feature selection and parameter optimization.
- Random Forest, with feature selection and parameter optimization.

# Results

The Linear Regression model has a MSE of 17,397.  The Decision Tree, with `min_sample_leaf` of 5, has a MSE of 3,297.  Lastly, the Random Forest, with `max_depth` of 'None', `min_sample_leaf` of 1, and `n_estimators` of 20, had the best (lowest) MSE of 2,011.  For future predictions, the Random Forest would be the best model to use as overfitting is reduced is this model as well.


