---
layout: post
title: More on the Machine Learning Framework
subtitle: More on ML Framework
categories: ML Frameworks
tags: [machine learning, frameworks]
mermaid: false
---

# Recap: Machine Learning & Data Science Framework:

- This is an iterative process.

1. **Problem Definition:** What's the problem?
2. **Data:** What's the data we have?
3. **Evaluation:** What's a success?
4. **Features:** What features to model?
5. **Modeling:** What kind of model should we use?
6. **Experimentation:** What have we tried/can we try?

- When shouldn't we use ML?
    - If a simple instructions-based system works to solve our problem.

# 1. Problem Definition:
- Aligning the problem we're trying to solve to a machine learning problem.

### Supervised Learning:
- We know inputs & outputs.
1. Classification Example: 
    - Inputs: Patient reports. 
    - Outputs: Patient has/doesn't have a heart disease.

2. Regression:
    - Inputs: Information about houses (area, no. of rooms, location, etc.). 
    - Outputs: Price of the house.

### Unsupervised Learning:
- We know inputs but **not sure** of outputs.
- Example:
    - Inputs: Customers Purchases
    - Outputs: (Try to figure out which purchases are similar to each other)

### Transfer Learning:
- Problem is similar to another problem.
- Example:
    - Current problem: Identify type of a dog.
    - Previous problem: Identifying type of a car.



# 2. Data:
- The more data, the better.
- What kind of data do we have?

## Main types of Data:
1. Structured: tabulated data.
2. Unstructured: Images, Videos, Audio, etc.


# 3. Evaluation:
- How well does a ML model to predict something?
- What's a success? (90%)

## The Metrics for different Problems:
1. **Classification:** Accuracy, Precision, and Recall.
2. **Regression:** Mean Absolute Error (MAE), Mean Squared Error (MSE), Root Mean Squared Error (RMSE).
3. **Recommendation Problems:** Precision at K.


# 4. Features:
- What do we already know about the data?
- Feature variables (inputs) are used to predict target variables (output).

# 5. Modeling:
- Based on the data we have, which ML model should we use?

## Parts of Modeling:
- Train, Validation & Test Sets (3 Sets):
    - Most important concept in ML.
    - Data is split into 3 seperate sets.


### 5.1 Choosing & Training a model:
- **Train set** is used to train the model.
- (70%-80%) of Data.
- Choosing a model: what kind of ML Model to use with what kind of problem.
    - *Structured Data:* CatBoost, XGBoost, Random Forest.
    - *Unstructured Data:* Deep Learning, Transfer Learning.
- Training:
- Model looks at Feature variables (inputs) & finds outputs through algorithms.
- Goal is to minimize time between experiments:
    - Using a small part of the data in the beginning.
    - Start with less complicated models at first, and observe **accuracy** and **training time**.
    - Add **complexity** to model according to your needs.


### 5.2 Tuning a model:
- **Validation set** is used to tune the model.
- (10%-15%) of Data.
- Once initial performance of a model on a dataset is acceptable, it can be fine tuned to the work better with the data it's working on.
- It can happen on *Training Set* if no *Validation Set* is available.
- Hyperparameters to be tuned depend on the model used. For example:
    - Random Forest: Number of Trees
    - Neural Networks: Number of Layers.



### 5.3 Model comparison:
- **Test set** is used to compare different models.
- (10%-15%) of Data.
- Happens during experimentation.
- How well does the model perform on the **Test Set**?
- A good model yields good results on both the **Training** & **Test** sets.
- Performance of Test Set can be slightly lower than the Train set's.

#### Underfitting & Overfitting:
- **Underfitting:** Test set's performance is dramatically lower than Train set's. 
- **Overfitting:** Test set's performance is higher than Train set's.
- *Underfitting* & *Overfitting* are examples of models that can't generalize well.
- A balanced performance, with a fitting in the *Goldilocks Zone*, is desired.
#### Reasons for Overfitting** & **Underfitting:
- **Data Leakage**: When some of the test data leaks into the training data, which results in *Overfitting*.
- **Data Mismatch**: The data you're training on is different than the you're testing on, which results in *Underfitting*. For example: datasets have different features.

#### Fixes for Underfitting & Overfitting:
1. Fixes for Underfitting:
    - Using a more advanced/complicated model.
    - Increasing the number of hyperparameters.
    - Reducing amount of features.
    - Train longer (on more data).
2. Fixes for Overfitting:
    - Collect more data.
    - Using a less complicated model.

# 6. Experimentation:
- Since the ML Framework is a highly iterative process, try different things and compare results.


# Tools used for Machine Learning & Modeling:
- TensorFlow
- PyTorch
- Scikit-learn
- CatBoost
- XGBoost