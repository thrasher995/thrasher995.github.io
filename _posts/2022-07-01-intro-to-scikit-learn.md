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
- Importing dataset into a Pandas DataFrame
- Creating X & Y:
    **X:** has all of the *features* columns
    **Y:** has *target* column
- Splitting data into *train* & *test* sets:
    `train_test_split` method from `sklearn.model_selection` module is used


### 2. Choosing Suitable Model 
- In Scikit-Learn, ML Models are refered to as *Estimators*.
- Choosing the model depends on the type of problem at hand.
- Some models would yield better results than others for the same problem, so it's important to ensure the right model was chosen.
- The map below helps with choosing the right model for the problem.
![Figure 1: Model Selection Map](https://raw.githubusercontent.com/mrdbourke/zero-to-mastery-ml/d7c767dd562ce65e73efa23c8e210f6260f678e5/images/sklearn-ml-map.png)


### 3. Fitting Model to Data & Making Predictions
- Models attempt to learn patterns in a dataset when the `fit()` method is called on a dataset.
- Predictions are made afterwards using the `prediction()` method.
- To make a prediction on a single sample, a Pandas Series is converted & reshaped into a 1-D NumPy array, and is then given as the argument for `predict()` method as shown below:
    ```
    .predict(np.array(pandas_series).reshape(1, -1))
    ```

### 4. Evaluating Models
- `score()` method is used on split dataset-couples to evaluate estimators.

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
