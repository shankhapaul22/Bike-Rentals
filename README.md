# Context

Many American cities have communal bike sharing stations where you can rent bicycles by the hour or day. Washington, D.C. is one of these cities. The District collects detailed data on the number of bicycles people rent by the hour and day.

Hadi Fanaee-T at the University of Porto compiled this data into a CSV file, which we'll be working with in this project. The file contains 17,380 rows, with each row representing the number of bike rentals for a single hour of a single day. It is included in the files as `bike_rental_hour.csv`.

# Objective

With this dataset, we will create a model to predict the total number of bikes people rented in a given hour. We will predict the `cnt` column using all of the other columns (if possible), except for `casual` and `registered`. These columns leak information from the future and may not be available with new data. We will drop the `yr` column as well, as new data will never have 2011 or 2012 as the year.

# Process

We explore the dataset through visualization and descriptive statistic tables to report any findings that may help or hinder the machine learning process.

We check the dataframe information and find there are no null values and all columns are numeric, except the dates. If there were missing values, we would have had to:

- impute the data with the mean or the mode of the column,
- drop columns if majority of the column was missing since it would add no value to the machine learning process, or
- drop rows if missing values are located randomly within the dataset and imputation is not possible.

The `season`, `month`, `hr`, `holiday`, `weekday`, `workingday`, & `weather` columns represent categorical values therfore we change their type. The `temp`, `atemp`, `windspead` and `hum` columns contain continuous data and need to be analyzed differently than the categorical columns.

We utilize visualization and compared our findings to domain knowledge to verify the data. If there were to be any unusual or corrupt data, we would have had to analyze further and remove the invalid data to our best ability.

We feature engineer a new column for the machine to understand that the hours of the day are relevant to each other. (i.e. Hours labeled 0 - 6 are considered in the morning and categorized together).

We will be treating each observation in the dataset as independent of each other, instead of sequential as the `date` column implies. We use random sampling to create the train and test dataset.

Since we will be training different models, we will be using MSE as our error metric for continuous numeric data to compare the models. MSE was chosen over MAE or RMSE as MSE displays the gap between the predicted and actual values more clearly (by squaring the difference). We may display the RMSE of our best model to observe how far off in rentals we can expect the model to perform since the RMSE value has the same unit as the target column.

We utilize the following models to find the best one for our objective:

- Linear Regression, as a baseline model to see if the target and the features have a linear relationship.
- Decision Tree, to capture non-linearity.
- Random Forest with Grid Search, to reduce overfitting and more accurate predictions than Decision Tree with hyperparameter optimization.

# Results

The Linear Regression model has MSE of 18,168. The histogram plot shows little similarity to target column.

The Decision Tree, with `min_sample_leaf` of 10, has MSE of 5,883. As we increase min_samples_leaf, we decrease variance, however we also increase bias.  

Lastly, the Random Forest, with `max_depth` of 'None', `min_sample_leaf` of 10, and `n_estimators` of 20, has the best(lowest) MSE of 5,043.  

# Conclusion

There is still room for implementing different methods to lower error:

- creating additional features, such as combining humidity, temperature and wind speed.
- utilizing XGBoosting which is another ensemble tree method that applies the principal of boosting.
- applying Multiple correspondence analysis (MCA) with dummy columns and/or Principal Component Analysis (PCA) to reduce dimensionality.

It would be interesting to predict the `casual` and `registered` rentals instead of `cnt` and see how they differ. We could also use the date and predict rentals in a sequential manner using LSTM rather than each hour as independent.
