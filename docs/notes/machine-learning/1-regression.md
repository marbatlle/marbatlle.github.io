---
title: Regression Algorithms
---

# Regression Algorithms

Regression models are used extensively to predict values based on the variables that are dependent on several factors. Appliied when the model has infinite possible values of outcome

## 1. Prepare the Data for Machine Learning Algorithms
Use of Transformation Pipelines including:
* Data Cleaning
* Handling Text and Categorical Attributes
* Feature Scaling

## 2. Training a Model

### Linear Regression
* **Pros:** Works on any size of dataset, gives informations about relevance of features.
* **Cons:** The Linear Regression Assumptions.

      from sklearn.linear_model import LinearRegression
      # Describe and fit the model
      lin_reg = LinearRegression()
      lin_reg.fit(housing_prepared, housing_labels)
      # Predict using the model
      housing_predictions = lin_reg.predict(housing_prepared)

### Polynomial Regression
* **Pros:** Works on any size of dataset, works very well on non linear problems.
* **Cons:** Need to choose the right polynomial degree for a good bias/variance tradeoff.

### SVR
* **Pros:** Easy adaptable, works very well on non linear problems, not biased by outliers.
* **Cons:** Compulsory to apply feature scalling, not well known, more dificult to understand.

      from sklearn.svm import SVR
      # Describe and fit the model
      svm_reg = SVR(kernel="linear")
      svm_reg.fit(housing_prepared, housing_labels)
      # Predict using the model
      housing_predictions = svm_reg.predict(housing_prepared)
      

### Decision Tree Regression
* **Pros:** Interpretability, no need for feature scaling, works on both linear / nonlinear problems.
* **Cons:** Poor results on too small datasets overfitting can easily occur.

      from sklearn.tree import DecisionTreeRegressor
      # Describe and fit the model
      tree_reg = DecisionTreeRegressor(random_state=42)
      tree_reg.fit(housing_prepared, housing_labels)
      # Predict using the model
      housing_predictions = tree_reg.predict(housing_prepared)

### Random Forest Regression
* **Pros:** Powerful and accurate, good performance on many problems, including non linear.
* **Cons:** Not interpretability, overfitting can easily occur, need to choose the number of trees.

      # Describe and fit the model
      from sklearn.ensemble import RandomForestRegressor
      Predict using the model
      forest_reg = RandomForestRegressor(n_estimators=100, random_state=42)
      forest_reg.fit(housing_prepared, housing_labels)

### Stochastic Gradient Descent Regressor

## 3. Evaluating a Model

### R-squared (R²) 

### Root Mean Square Error (RMSE)
RMSE is a stardard way to measure the error of a model in predicting quantitative data. It measures the average magnitude of the error.

Expressing the formula in words, the difference between forecast and corresponding observed values are each squared and then averaged over the sample. Finally, the square root of the average is taken. Since the errors are squared before they are averaged, the RMSE gives a relatively high weight to large errors. This means the RMSE is most useful when large errors are particularly undesirable.

    from sklearn.metrics import mean_squared_error

    lin_mse = mean_squared_error(housing_labels, housing_predictions)
    lin_rmse = np.sqrt(lin_mse)
    lin_rmse

### Mean Absolute Error (MAE)
MAE measures the average magnitude of the errors in a set of forecasts, without considering their direction. It measures accuracy for continuous variables. 

Expressed in words, the MAE is the average over the verification sample of the absolute values of the differences between forecast and the corresponding observation. The MAE is a linear score which means that all the individual differences are weighted equally in the average.

    from sklearn.metrics import mean_absolute_error

    lin_mae = mean_absolute_error(housing_labels, housing_predictions)
    lin_mae

### Cross-Validation
Evaluation technique that randomly splits the training set into 10 distinct subsets called folds, then it trains and evaluates the model 10 times, picking a different fold for evaluation every time and training on the other 9 folds. The result is an array containing the 10 evaluation scores. 


    from sklearn.model_selection import cross_val_score

    scores = cross_val_score(tree_reg, housing_prepared, housing_labels,
                            scoring="neg_mean_squared_error", cv=10)
    tree_rmse_scores = np.sqrt(-scores)

    def display_scores(scores):
        print("Scores:", scores)
        print("Mean:", scores.mean())
        print("Standard deviation:", scores.std())

    display_scores(tree_rmse_scores)

## 4. Fine-Tune Your Model

### Grid Search

### Randomized Search

## 5. Analyze the Best Models and Their Errors

## 6. Evaluate Your System on the Test Set
