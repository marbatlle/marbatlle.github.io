---
title: Classification Algorithms
linktitle: 1. Classification
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: Machine Learning
    weight: 1

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

## 1. Logistic Regression Algorithm
We use logistic regression for the binary classification of data-points. We perform categorical classification such than an output belongs to either of the two classes (1 or 0). With the help of the hypothesis, we can derive the likelihood of the event. The data generated from this hypothesis can fit into the log function that creates an S-shaped curve known as”sigmoid”. Using this log function, we can further predict the category of class.

### Implementation using sklearn

#### Step 1. Load the libraries
import numpy as np 
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
import seaborn as sns
from sklearn import metrics

#### Step 2. Split Data into Training and Test Sets
x_train, x_test, y_train, y_test = train_test_split(digits.data, digits.target, test_size=0.25, random_state=0)

#### Step 3. Make an instance of the Model
# all parameters not specified are set to their defaults
logisticRegr = LogisticRegression()

#### Step 4. Train the Model on the data
logisticRegr.fit(x_train, y_train)

#### Step 5. Make predictions
predictions = logisticRegr.predict(x_test)

#### Step 6. Measuring Model Performance
# Use score method to get accuracy of model
score = logisticRegr.score(x_test, y_test)
print(score)

# Use confusion matrix
plt.figure(figsize=(9,9))
sns.heatmap(cm, annot=True, fmt=".3f", linewidths=.5, square = True, cmap = 'Blues_r');
plt.ylabel('Actual label');
plt.xlabel('Predicted label');
all_sample_title = 'Accuracy Score: {0}'.format(score)
plt.title(all_sample_title, size = 15);
