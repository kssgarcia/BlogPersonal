---
title: "Variance and bias in neural network"
date: 2024-04-25T11:48:52-05:00
draft: false
math: true
---

In this post, I will talk about a crucial topic in neural networks that is present in all of them: regularization. It is important to understand the metrics used in training, with the most common being the loss.

### High Variance

"High variance," also known as overfitting, refers to when the model performs well on the training set but not on the validation set. This indicates that the model has learned the dataset well, including noise, but has not generalized well to unseen data. Although overfitting shows that the model has learning capacity, regularization techniques are necessary to improve its generalization ability. Some common techniques include L1, L2, dropout, early stopping, and others. In my opinion, early stopping should not be used, although some prefer it.

### High Bias

"High bias" or underfitting occurs when the neural network is unable to learn adequately from the training set, which is reflected in high loss in both the training and validation sets. The metrics for both sets will be similarly low.

### High Bias and High Variance

This case occurs when the model performs poorly in both training and validation, showing poor metrics in both sets.

### What to Do?

#### High Bias

Underfitting indicates that the model is not complex enough for the task or that the dataset is not well-structured.

#### Steps:
1. Review the dataset and check if it is well-constructed.
2. If the dataset is fine, switch to a larger model and observe the metrics.

#### High Variance

Overfitting can be countered using regularization techniques, which adjust the capacity of neural networks to better fit the task and generalize appropriately.

### Regularization Techniques

#### 1. **L1 and L2 Regularization (Weight Decay)**

##### L1 Regularization (Lasso):

- **Description**: Adds a penalty based on the sum of the absolute values of the parameters' coefficients, which can lead to sparser models.
- **Formula**: $Loss = \text{Loss original} + \lambda \sum |w_i|$

##### L2 Regularization (Ridge):

- **Description**: Adds a penalty based on the sum of the squares of the parameters' coefficients, distributing weight across all coefficients.
- **Formula**: $Loss = \text{Loss original} + \lambda \sum |w_i|^2$

#### 2. **Dropout**

- **Description**: During training, randomly deactivates a fraction of neurons in each layer to prevent neurons from becoming too reliant on one another, reducing overfitting and improving generalization.

#### 3. **Early Stopping**

- **Description**: Stops training when the performance on the validation set stops improving, preventing overfitting.

#### 4. **Batch Normalization**

- **Description**: Normalizes the outputs of a layer to have zero mean and unit variance, then applies a linear transformation. It speeds up training and improves model stability, also acting as a form of regularization by introducing noise into training.

### Considerations

When thinking about the machine learning process, it's useful to view it as several independent steps:

1. **Optimize a cost function $J(W,b)$**: Review the dataset and find a model that minimizes this function.
2. **Avoid Overfitting**: Use regularization techniques like L1, L2, batch normalization, and dropout. I do not recommend early stopping as it combines both tasks and can prevent the model from reaching its best convergence point in training.
