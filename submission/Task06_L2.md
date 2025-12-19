# L2 Regularization Analysis Report

This analysis examines the impact of varying the L2 regularization factor ($\lambda$) across three test values: **0.0001**, **0.001**, and **0.01**.

---

## 1. How L2 Reduces Weight Magnitude
L2 regularization (Weight Decay) adds a penalty to the loss function based on the square of the weights:

$$Cost = \text{Loss} + \lambda \sum_{w \in weights} w^2$$

* **The "Weight Decay" Effect:** During optimization, the gradient of the penalty term is $2\lambda w$. This means that in every update, the model subtracts a portion of the weight itself. 
* **Result in your data:** As $\lambda$ increases from $0.0001$ to $0.01$, we see the **Training Loss** rise from **0.1116** to **0.3610**. This is because the optimizer is no longer just minimizing prediction error; it is also fighting to keep weight magnitudes small.

---

## 2. Why Smaller Weights Improve Generalization
Generalization is the model's ability to perform well on unseen data. Large weights often indicate that the model has "over-fit" to the noise in the training set.

* **Sensitivity:** High weights make the network highly sensitive to small changes in input. If a weight is massive, a tiny fluctuation in an input pixel can drastically change the output.
* **Simplicity:** By forcing weights to be small, L2 encourages a "simpler" model with smoother decision boundaries.
* **Observation:** Note that while the training accuracy drops as we increase L2, the **Validation Accuracy** remains very high and stable. For example, at $0.01$, the validation accuracy ($96.24\%$) is actually higher than the training accuracy ($93.64\%$), suggesting the model is extremely robust and not over-reliant on training-specific patterns.



---

## 3. How L2 Changes the Validation Loss Trend
Regularization significantly alters the trajectory of the validation error during training.

| L2 Value | Training Loss (Ep 5) | Val Loss (Ep 5) | Trend Observation |
| :--- | :--- | :--- | :--- |
| **0.0001** | 0.1116 | 0.1113 | Rapid descent; risks "U-shaped" overfitting if trained longer. |
| **0.001** | 0.1996 | 0.1660 | Balanced; slower but more controlled convergence. |
| **0.01** | 0.3610 | 0.2925 | Conservative; very stable, unlikely to diverge. |

**The Impact:** Without enough L2 ($0.0001$), the gap between training and validation loss is narrow, but the model is "aggressive." With higher L2 ($0.01$), the validation loss stays very close to the training loss (and is even lower here), indicating that the model is successfully resisting overfitting. It prevents the validation loss from bottoming out and starting to rise again.



---

## Summary of Results

| $\lambda$ Value | Final Training Acc | Final Val Acc | Final Val Loss |
| :--- | :--- | :--- | :--- |
| **0.0001** | 97.66% | 97.96% | 0.1113 |
| **0.001** | 96.39% | 97.78% | 0.1660 |
| **0.01** | 93.64% | 96.24% | 0.2925 |