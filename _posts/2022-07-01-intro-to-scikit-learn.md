---
layout: post
title: Introduction to Scikit Learn
subtitle: More on ML Framework
categories: ML Python Scikit-learn
tags: [machine learning, scikit-learn, python]
mermaid: false
---

## What is Scikit-learn (sklearn)?
- It's a Python Machine Learning library.
- It helps users to build Machine Learning Models that come up with patterns in the data & use the patterns to make predictions.
- Scikit-learn implements tools to evaluate predictions.

## Why use Scikit-learn?
- It's built on Numpy & MatplotLib
- Has many in-built ML models
- Implements methods to evaluate ML models
- Very well-design API

## Scikit-learn Workflow:
1. Getting the data ready
2. Choosing a suitable model 
3. Fitting model to data & make predictions
4. Evaluating the model
5. Improving model through experimentation
6. Saving & Reloading trained model


### 1. Getting Data Ready
1. Preparation:
    - Importing dataset into a Pandas DataFrame
    - Splitting data into features & labels (X & Y):
        **X:** has all of the *features* columns
        **Y:** has *target* column
    - Filling (**Imputing**) or disregarding missing values.
    - Converting non-numerical values into numerical values (**feature encoding**).
        - [sklearn.preprocessing.OneHotEncoder()](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html)
        - [pandas.get_dummies()](https://pandas.pydata.org/docs/reference/api/pandas.get_dummies.html)
        - **Feature Scaling**: Ensuring that all numerical data (across all features) is on the same scale.
            - Example: 
2. Splitting data into *train* & *test* sets:
    - `train_test_split` method from `sklearn.model_selection` module is used.
    - `test_size` parameter is used to set % of dataset to be test (*test_size=0.25* for 25%).
        - Default value is 0.25.


### 2. Choosing Suitable Model 
- In Scikit-Learn, ML Models are refered to as *Estimators*.
- Choosing the model depends on the type of problem at hand.
- Some models would yield better results than others for the same problem, so it's important to ensure the right model was chosen.
- The map below helps with choosing the right model for the problem.
![Figure 1: Model Selection Map](https://raw.githubusercontent.com/mrdbourke/zero-to-mastery-ml/d7c767dd562ce65e73efa23c8e210f6260f678e5/images/sklearn-ml-map.png)

- Notes:
    - If you have **structured** (tabulated) data, use ensemble methods.
    - If you have **unstructured** data, use deep learning or transfer learning methods.

### 3. Fitting Model to Data & Making Predictions
1. Fitting a model to data:
    - Models attempt to learn patterns in a dataset when the `fit()` method is called on a dataset.
2. Making Predictions:
- There are 2 ways to make predictions:
    1. Using `predict()` method:
        - Main method used
        - Used for Regression & Classification problems.
    2. Using `predict_proba()` method:
        - Shows probability for each classification estimate.
        - Used for Classification problems.
        - Left value represents probability of prediction being False.
        - Right value represents probability of prediction being True.


- Predictions are made afterwards using the `predict()` method.
- To make a prediction on a single sample, a Pandas Series is converted & reshaped into a 1-D NumPy array, and is then given as the argument for `predict()` method as shown below:
    ```
    .predict(np.array(pandas_series).reshape(1, -1))
    ```

### 4. Evaluating Models
- Ways to evaluate Sklearn estimators: 
    - Check Sklearn [Metrics & scoring documentation](https://scikit-learn.org/stable/modules/model_evaluation.html) for more info.
    1. `score()` method:
        - Used on split dataset-couples to evaluate estimators.
        - Highest value is 1.0 & Lowest value is 0.0.
        - Default `score()` evaluation metric for Classification problems is **Mean Accuracy**.
        - Default `score()` evaluation metric for Regression problems is **r_squared** (Coefficient of Determination).

    2. The `scoring` parameter:
        - Cross-validation Accuracy:
            ![Figure2: 5-Fold Cross-validation](https://d2mk45aasx86xg.cloudfront.net/image5_11zon_af97fe4b03.webp)
            - Does k-fold splits.
            - Returns an array.
            - Syntax:
            
            ```Python
            from sklearn.model_selection import cross_val_score
            # 5-fold Cross-val score: 
            cross_val_score(classifier, X, Y, cv=5)
            ```
        
        - AUC/ROC Curves:
            - Area Under the Curve (AUC).
            - Receiver Operating Characteristic (ROC).
            - Comparison of model's True Positive Right (TPR) vs models' False Positive Right (FPR):
                - True positive = model predicts 1 when truth is 1
                - False positive = model predicts 1 when truth is 0
                - True negative = model predicts 0 when truth is 0
                - False negative = model predicts 0 when truth is 1
            

    3. Problem-specific metric functions:

    
- Evaluation Metrics in Regression problems:
    1. Mean Absolute Error (`mean_absolute_error` from sklearn.metrics)
    2. 


### 5. Improving Model
- Tuning the estimator's hyperparameters to yield better results.
- It's best practice to test different hyperparameters with a validation set or cross-validation.

### 6. Saving & Reloading Trained Model
- Trained models can be exported and used again later.
- Python's `pickle` module is used to export & load trained modules.
- `pickle.dump()` method is used to export models.
- `pickle.load()` method is used to load models.

## Examples on the Scikit-Learn Workflow:
### Example 1: Predicting Heart Diseases - Classification Problem
[ML - Example on Classification Problems](https://github.com/thrasher995/thrasher995.github.io/blob/main/_data/_notebooks/classification_example.ipynb)



### Example 2: 
[ML - Example on Regression Problems](https://github.com/thrasher995/thrasher995.github.io/blob/main/_data/_notebooks/regression_example.ipynb)
