---
layout: post
title: Introduction to Scikit Learn
subtitle: More on ML Framework
categories: ML Python Scikit-learn Pipelines
tags: [machine learning, scikit-learn, python, pipelines]
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

## Scikit-learn Workflow
1. Getting the data ready
2. Choosing a suitable model 
3. Fitting model to data & make predictions
4. Evaluating the model
5. Improving model through experimentation
6. Saving & Reloading trained model


### Step 1: Getting Data Ready
1. Preparation:
    1. Importing dataset into a Pandas DataFrame
    2. Splitting data into features & labels (X & Y):
        **X:** has all of the *features* columns
        **Y:** has *target* column
    3. Filling (**Imputing**) or disregarding missing values:
        1. Imputing with a [sklearn.impute.SimpleImputer()](https://scikit-learn.org/stable/modules/generated/sklearn.impute.SimpleImputer.html) object.   
        2. Dropping values using [pandas.DataFrame.dropna()](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.dropna.html) method.
            
    4. Converting non-numerical values into numerical values (**feature encoding**):
        1. [sklearn.preprocessing.OneHotEncoder()](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html)
        2. [pandas.get_dummies()](https://pandas.pydata.org/docs/reference/api/pandas.get_dummies.html)
    
    5. **Features Scaling**: 
        - Ensuring that all numerical data (across all features) is on the same scale. 
        - When features are on different scales, one feature would dominate over the other.
        - Needed when using ML Algorithms that require **gradient calculation**, such as: *linear/logistic regression*, *artificial neural networks*, and *deep neural networks*.
        - Not required when using *distance-based* or *tree-based* algorithms, such as: *K-Means Clustering*, *K Nearest Neighbors*, *Decision Trees*, *Random Forest*, and *XG-Boost*.

        1. **Standardization:**
            - Convert features to have a **mean = 0**, **std=1**.
            - Also known as **Z-score Normalization**.
            - Properties have behavior of a standard normal distribution.
            ![Figure 1: Standardized Normal Distribution](https://raw.githubusercontent.com/thrasher995/thrasher995.github.io/main/_data/_pictures/standarized-normal-distribution.jpg)

            - Formula:
                ```
                z = (x - mean) / (std(x)) 
                ```
            - Using `sklearn.preprocessing.StandardScaler`:
                ``` Python
                from sklearn.preprocessing import StandardScaler
                scaler = StandardScaler()
                scaled_df = scaler.fit_transform(original_df)
                ```    
            - Example on *Standardization*:
                **A,B,C** are the Features. 
                
                Before *Standardization*:
                
                || A | B | C |
                |---|---|---|---|
                |count|1000.00|1000.00|1000.00|
                |mean|2.20|56.25|2320.00|
                |std|0.24|4.86|193.85|
                |min|1.50|40.00|1800.00|
                |25%|2.04|53.03|2190.45|
                |50%|2.20|56.16|2312.44|
                |75%|2.36|59.42|2455.76|
                |max|3.00|70.00|3000.00|

                After *Standardization*:
                
                || A | B | C |
                |---|---|---|---|
                |count|1000.00|1000.00|1000.00|
                |mean|0.00|0.00|0.00|
                |std|1.00|1.00|1.00|
                |min|-2.88|-3.34|-2.68|
                |25%|-0.66|-0.66|-0.67|
                |50%|0.01|-0.02|-0.04|
                |75%|0.68|0.65|0.70|
                |max|3.33|2.83|3.51|

        2. **Normalization:**
            - Make features on a scale of 0-1.
            - Formula:
                ```
                x' = (x - min(x)) / (max(x)-min(x)) 
                ```
            - Using `sklearn.preprocessing.MinMaxScaler`:
                ``` Python
                from sklearn.preprocessing import MinMaxScaler
                scaler = MinMaxScaler()
                scaled_df = scaler.fit_transform(original_df)
                ```
            - Example on *Normalization*: 
            
                **A,B,C** are the Features. 
                
                Before *Normalization*:
                
                || A | B | C |
                |---|---|---|---|
                |count|1000.00|1000.00|1000.00|
                |mean|2.20|56.25|2320.00|
                |std|0.24|4.86|193.85|
                |min|1.50|40.00|1800.00|
                |25%|2.04|53.03|2190.45|
                |50%|2.20|56.16|2312.44|
                |75%|2.36|59.42|2455.76|
                |max|3.00|70.00|3000.00|

                After *Normalization*:

                || A | B | C |
                |---|---|---|---|
                |count|1000.00|1000.00|1000.00|
                |mean|0.46|0.54|0.43|
                |std|0.16|0.16|0.16|
                |min|0.00|0.00|0.00|
                |25%|0.36|0.43|0.33|
                |50%|0.47|0.54|0.43|
                |75%|0.57|0.65|0.55|
                |max|1.00|1.00|1.00|


            

        #### Standardization vs Normalization
        - In case of neural networks, Normalization is preffered because distribution is not assumed beforehand.
        - Standardization is preferred when data follows a *gaussian distribution*.
        - Standardization is preferred there are a lot of outliers in the data.

2. Splitting data into *train* & *test* sets:
    - `train_test_split` method from `sklearn.model_selection` module is used.
    - `test_size` parameter is used to set % of dataset to be test (*test_size=0.25* for 25%).
        - Default value is 0.25.


### Step 2: Choosing Suitable Model 
- In Scikit-Learn, ML Models are refered to as *Estimators*.
- Choosing the model depends on the type of problem at hand.
- Some models would yield better results than others for the same problem, so it's important to ensure the right model was chosen.
- The map below helps with choosing the right model for the problem.
![Figure 2: Model Selection Map](https://raw.githubusercontent.com/mrdbourke/zero-to-mastery-ml/d7c767dd562ce65e73efa23c8e210f6260f678e5/images/sklearn-ml-map.png)

- Notes:
    - If you have **structured** (tabulated) data, use ensemble methods.
    - If you have **unstructured** data, use deep learning or transfer learning methods.

### Step 3: Fitting Model to Data & Making Predictions
1. Fitting a model to data:
    - Models attempt to learn patterns in a dataset when the `fit()` method is called on a dataset.
2. Making Predictions:

There are 2 ways to make predictions:
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

### Step 4: Evaluating Models

#### General Evaluation (`score` method):
- Used on split dataset-couples to evaluate estimators.
- Highest value is 1.0 & Lowest value is 0.0.
- Default `score()` evaluation metric for Classification problems is **Mean Accuracy**.
- Default `score()` evaluation metric for Regression problems is **r_squared** (Coefficient of Determination).


- (Check out Sklearn [Metrics & scoring documentation](https://scikit-learn.org/stable/modules/model_evaluation.html) for more info.)

##### Evaluating Classifiers (Classification Problems) 
1. Cross-validation Accuracy:
        ![Figure 3: 5-Fold Cross-validation](https://d2mk45aasx86xg.cloudfront.net/image5_11zon_af97fe4b03.webp)
    - Does k-fold splits.
    - Returns an array.
    - Syntax:
            
        ```Python
        from sklearn.model_selection import cross_val_score
        # 5-fold Cross-val score: 
        cross_val_score(classifier, X, Y, cv=5)
        ```
        
2. AUC/ROC Curves:
    - Area Under the Curve (AUC).
    - Receiver Operating Characteristic (ROC).
    - For binary Classification problems.
    - AUC tells you how good a model can predict - perfect model has a score of 1.0
    - Comparison of model's True Positive Right (TPR) vs models' False Positive Right (FPR):
        - True positive = model predicts 1 when truth is 1
        - False positive = model predicts 1 when truth is 0
        - True negative = model predicts 0 when truth is 0
        - False negative = model predicts 0 when truth is 1
    - Check out [Confusion Matrix](https://thrasher995.github.io/ml/python/scikit-learn/2022/08/12/confusion-matrix.html)

    - Syntax:
           
        ```Python
        from sklearn.metrics import roc_auc_score
        roc_auc_score(y_test, y_predicted_positive)
        ```


##### Classification Report
- Builds a text report showing the main classification metrics, such as:
    - Precision:
        - Accuracy of positive predictions.
        - A model of no False Positives has a *precision* of 1.0.
        - Precision = true_postives/(true_postives + false_postives)
    
    - Recall:
        - The ability of a classifier to find all positive instances.
        - Fraction of positives that were correctly identified.
        - A model with no False Negatives has a *recall* of 1.0.
        - Recall = true_positives/(true_positives + false_negatives)
    
    - F1-Score:
        - Harmonic Mean of Precision and Recall.
        - Best score = 1.0, worst score = 0.0
        - F1 should only be used for comparing models, not for global accuracy.
        - F1-Score = (2 * Recall * Precision) / (Recall + Precision)
    
    - Support:
        - Shows the number of samples each metric was calculated on.

    - Accuracy:
        - The accuracy of the model.
        - Perfect accuracy = 1.0.
    
    - Macro Avg:
        - The average for each metric between the classes 
        - Macro Avg = (metric_class1 + metric_class2) / 2
        - Doesn't class imbalace into account.
        - Pay attention to this metric.
        - Example on Class Imbalance:
            ```
            Total number of samples = 50
            Class 0 has 15 samples (30%)
            Class 1 has 35 samples (70%)
            ``` 
    
    - Weighted Avg:
        - The weighted average for each metric between the classes
        - Macro Avg = ((Class1 percentage * metric_class1) + (Class2 percentage * metric_class2)) / 2
        - Takes class imbalace into account.

- Syntax:
        ```Python
        from sklearn.metrics import classification_report
        print (classification_report(y_test,y_preds))
        ```
#### Evaluating Regressors (Regression Problems)   
1. R2 Score:

2. Mean Absolute Error (MAE):

3. Mean Squared Error (MSE):



### Step 5: Improving Model
- Tuning the estimator's hyperparameters to yield better results.
- It's best practice to test different hyperparameters with a validation set or cross-validation.

### Step 6: Saving & Reloading Trained Model
- Trained models can be exported and used again later.
- Python's `pickle` module is used to export & load trained modules.
- `pickle.dump()` method is used to export models.
- `pickle.load()` method is used to load models.

## Introducing [sklearn.pipeline.Pipeline](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.Pipeline.html):
- Pipeline of transforms with a final *estimator*.
- Sequentially applies a list of transforms and a final estimator.
- The purpose of the pipeline is to assemble several steps that can be cross-validated together while setting different parameters.
- Refer to documentation for more info.

## Examples on the Scikit-Learn Workflow
### Example 1: Predicting Heart Diseases - Classification Problem
[ML - Example on Classification Problems](https://github.com/thrasher995/thrasher995.github.io/blob/main/_data/_notebooks/classification_example.ipynb)


### Example 2: Predicting Median House Values in California Districts - Regression Problem
[ML - Example on Regression Problems](https://github.com/thrasher995/thrasher995.github.io/blob/main/_data/_notebooks/regression_example.ipynb)


### Example 3: Using Scikit-Learn's `Pipeline()` Class:
[ML - Example on Scikit-Learn's Pipeline() Class](https://github.com/thrasher995/thrasher995.github.io/blob/main/_data/_notebooks/pipelines.ipynb)
