---
layout: post
title: Confusion Matrix
subtitle: Representing TPR vs FPR
categories: ML [Data Science] Scikit-learn 
tags: [machine learning, scikit-learn, data science]
mermaid: false
---

# Introducing the Confusion Matrix
- Also known as an **Error Matrix**.
- Quick way to compare a model's **predicted labels** with the **actual labels** it was supposed to predict.
- Not strictly used for **binary classification** problems.
- Gives you an idea where the model gets confused.
- Syntax:
                
```Python
from sklearn.metrics import confusion_matrix
confusion_matrix = (y_test, y_pred)
pd.crosstab(y_test, y_pred, rownames=["Actual"], colnames = ["Predicted"])
            
```
![Figure 1: Confusion Matrix](https://github.com/thrasher995/thrasher995.github.io/blob/main/assets/images/resources/confusion_matrix.jpeg?raw=true)


# Visualizing the Confusion Matrix

1. Using `pandas.crosstab(y_test, y_pred, rownames=["Actual"], colnames = ["Predicted"])`
2. Using `ConfusionMatrixDisplay` from `sklearn.metrics`: (refer to [ML - Example on Classification Problems](https://github.com/thrasher995/thrasher995.github.io/blob/main/_data/_notebooks/classification_example.ipynb) for examples)
    1. `.from_estimator(estimator = used_estimator, X = X, Y=Y)`: includes training set in visualization.
    2. `.from_predictions(y_true=y_test,y_pred = y_pred)`: only includes set used for predictions.
    
    - Colors can be changed (refer to sklearn documentations).
