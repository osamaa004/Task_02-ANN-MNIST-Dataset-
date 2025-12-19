# Analysis of Weight Distributions and Regularization

This report analyzes how different regularization techniques affect the internal weight behavior and final performance of your model.

---

## 1. Experimental Results Comparison

Below are the metrics recorded at the final epoch for each configuration:

| Configuration | Training Loss | Training Acc | Val Loss | Val Acc |
| :--- | :---: | :---: | :---: | :---: |
| **Normal Weights** | 0.1116 | 97.66% | 0.1113 | 97.96% |
| **0.3 Dropout** | 0.1248 | 96.29% | 0.0906 | 97.34% |
| **0.01 L2** | 0.3610 | 93.64% | 0.2925 | 96.24% |

---

## 2. Weight Description and Behavior

### Normal Weights (Baseline)
* **Description:** Weights are free to grow as needed to minimize training loss.
* **Behavior:** This typically results in the lowest training loss (**0.1116**). However, the model may rely heavily on specific "strong" weight paths, which can lead to overfitting if the data is noisy.
* **Observation:** Your baseline achieved high accuracy quickly, but notice that the gap between training and validation is very tight, suggesting it has likely fully utilized its capacity.

### Weights with 0.3 Dropout
* **Description:** During training, 30% of neurons are randomly deactivated, forcing the weights to be more distributed and redundant.
* **Behavior:** No single neuron can carry all the information, so the weights become more balanced across the layer.
* **Observation:** While training accuracy is slightly lower than the baseline (**96.29%**), the validation loss is extremely healthy (**0.0906**), indicating that dropout successfully forced the weights to learn more robust features.



### Weights with 0.01 L2 (Weight Decay)
* **Description:** A penalty proportional to the square of the weights is added to the loss function.
* **Behavior:** This creates a "pressure" that pulls weight magnitudes toward zero. It effectively prevents any single weight from becoming too large and dominating the output.
* **Observation:** In your results, L2 has the highest training loss (**0.3610**). This is expected because the weights are being constrained from reaching their "ideal" mathematical values to ensure they remain small and generalize better.



---

## 3. Summary Comparison

| Feature | Normal Weights | 0.3 Dropout | 0.01 L2 |
| :--- | :--- | :--- | :--- |
| **Weight Magnitude** | Unconstrained | Distributed | **Smallest (Decayed)** |
| **Constraint Method** | None | Stochastic (Random) | Mathematical Penalty |
| **Primary Goal** | Minimize Loss | Reduce Co-dependency | Limit Complexity |
| **Impact on Loss** | Lowest | Moderate | **Highest (Penalty added)** |