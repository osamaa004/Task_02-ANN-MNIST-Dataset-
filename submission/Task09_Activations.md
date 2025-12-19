# Activation Function Performance Analysis

This report evaluates the training characteristics of **Tanh**, **Softsign**, and **GELU** activation functions based on your experimental data.

---

## 1. Experimental Results Data Table

The following metrics were recorded at the final epoch (Epoch 5) for each activation function:

| Activation | Training Loss | Training Acc | Val Loss | Val Acc |
| :--- | :---: | :---: | :---: | :---: |
| **Tanh** | 0.0975 | 97.02% | 0.0867 | 97.46% |
| **Softsign** | 0.0563 | **98.20%** | **0.0760** | **97.86%** |
| **GELU** | **0.0813** | 97.49% | 0.0880 | 97.46% |

---

## 2. Gradient Flow and Performance Insights

### Tanh vs. Softsign (The Vanishing Gradient Risk)
* **Tanh:** While it is zero-centered, its gradients saturate (become near zero) for very high or low input values. This can lead to slower learning in deep networks. In your results, Tanh had the highest training loss (**0.0975**) and lowest training accuracy (**97.02%**) among the three.
* **Softsign:** Softsign is similar to Tanh but has a flatter curve, meaning its gradients stay "active" longer before saturating. 
* **Observation:** In your logs, **Softsign** actually performed the best, reaching the highest training accuracy of **98.20%** and the lowest validation loss of **0.0760**.


### GELU (Gaussian Error Linear Unit)
* **Mechanism:** GELU weights inputs by their percentile, effectively acting as a smoother, probabilistic version of ReLU. 
* **Transformer Use Case:** GELU is the standard for Transformer models because it avoids the "dead neuron" problem of ReLU while providing better nonlinearity.
* **Your Data:** GELU performed well and stably, ending with a validation accuracy of **97.46%**, identical to Tanh but with a better training loss (**0.0813**).

---

## 3. Why ReLU Remains Preferred for CNN/MLP
While your results show **Softsign** and **GELU** performed excellently, ReLU remains the industry standard for most standard MLPs and CNNs because:
1. **Computational Efficiency:** ReLU only requires a simple threshold at zero ($max(0, x)$), whereas Tanh, Softsign, and GELU require more complex exponential or fractional math.
2. **Sparsity:** ReLU produces "sparse" activations (many neurons become exactly zero), which often leads to better model performance and faster inference.

---

## 4. Final Conclusion
Based on your 5-epoch run, **Softsign** was the clear winner for this specific architecture, providing the fastest convergence and best generalization. **GELU** provided a very stable middle ground, while **Tanh** lagged slightly behind due to its more aggressive gradient saturation.