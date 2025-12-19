# Optimizer Performance Analysis Report

This report compares the training characteristics of four optimization algorithms—**SGD**, **SGD Momentum**, **Adam**, and **AdamW**—using the specific results from your training logs.

---

## 1. The Evolution of Optimizers

Each optimizer represents a step forward in how the model navigates the loss landscape:

* **SGD:** The baseline. Updates weights purely on current gradients.
* **SGD Momentum:** Adds "velocity" to skip over local minima and speed up training.
* **Adam:** Uses adaptive learning rates for every parameter, allowing for rapid convergence.
* **AdamW:** The modern standard. It decouples weight decay from the gradient update, ensuring better regularization than standard Adam.

---

## 2. Experimental Results (Epoch 5)

Based on the uploaded logs, here is how the optimizers performed at the end of the 5-epoch run:

| Metric | SGD | SGD Momentum | Adam | AdamW |
| :--- | :---: | :---: | :---: | :---: |
| **Training Loss** | 1.1042 | 0.2855 | 0.1116 | **0.1098** |
| **Training Acc** | 84.14% | 93.64% | 97.66% | **97.83%** |
| **Val Loss** | 0.8115 | 0.2265 | 0.1113 | **0.1085** |
| **Val Accuracy** | 86.84% | 96.20% | 97.96% | **98.12%** |

---

## 3. Key Observations & Comparison

### From SGD to Momentum
By adding momentum, the "zig-zagging" behavior of basic SGD is reduced. 
* **Your Data:** You can see this in the massive jump in **Validation Accuracy** from **86.84%** (SGD) to **96.20%** (Momentum). Momentum allowed the model to find a much better global minimum in the same 5 epochs.



### From Adam to AdamW
Adam-based optimizers are "smarter" because they adjust learning rates automatically. However, AdamW handles weight decay more effectively.
* **Your Data:** While Adam performed excellently, **AdamW** achieved the best overall results in the group, with the lowest **Val Loss (0.1085)** and highest **Val Accuracy (98.12%)**. 
* **Generalization:** Notice that for AdamW, the Validation Accuracy is higher than the Training Accuracy, suggesting the model is extremely robust and not overfitting.



---

## 4. Final Comparison Summary

| Feature | SGD | SGD Momentum | Adam | AdamW |
| :--- | :--- | :--- | :--- | :--- |
| **Convergence Speed** | Slow | Moderate | Fast | **Fastest** |
| **Final Val Loss** | 0.8115 | 0.2265 | 0.1113 | **0.1085** |
| **Final Val Acc** | 86.84% | 96.20% | 97.96% | **98.12%** |
| **Stability** | Low (Noisy) | Medium | High | **Very High** |