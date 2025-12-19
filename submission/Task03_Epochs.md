## 📈 Training Dynamics Analysis (5, 10, and 20 Epochs)

### 1. 5 Epochs Results Analysis (image_f84317.png)

| Metric | Start (Epoch 1) | End (Epoch 5) | Trend |
| :--- | :--- | :--- | :--- |
| **Loss** | 0.2687 | 0.0463 | Decreasing |
| **Val\_Loss** | 0.1202 | 0.0864 | Decreasing |
| **Accuracy** | 0.9230 | 0.9859 | Increasing |
| **Val\_Accuracy** | 0.9658 | 0.9786 | Increasing |

* **Signs of Overfitting (Epoch 5):** Minimal signs of overfitting. Both $\text{loss}$ and $\text{val\_loss}$ are decreasing, and both $\text{accuracy}$ and $\text{val\_accuracy}$ are increasing right up to the end. The model is still learning and generalizing well.
* **Conclusion:** The model is **underfitting** or **optimally fit** at 5 epochs. More training would be beneficial.

### 2. 10 Epochs Results Analysis (image_f7f101.png)

| Metric | Start (Epoch 1) | End (Epoch 10) | Trend |
| :--- | :--- | :--- | :--- |
| **Loss** | 0.2764 | 0.0166 | Decreasing |
| **Val\_Loss** | 0.1351 | 0.0944 | **Increasing** (from E8/9) |
| **Accuracy** | 0.9210 | 0.9949 | Increasing |
| **Val\_Accuracy** | 0.9592 | 0.9796 | **Decreasing** (from E8/9) |

* **Signs of Overfitting (Epoch 10):** Clear signs of **early overfitting** begin around **Epoch 8/9**:
    * **Epoch 8:** $\text{val\_loss}$ reaches its minimum (0.0777).
    * **Epoch 9/10:** $\text{val\_loss}$ starts to increase (0.0915, 0.0944) while the $\text{loss}$ continues to drop rapidly (0.0199, 0.0166). This divergence is the classic indicator of overfitting. 
    * Similarly, $\text{val\_accuracy}$ peaks around Epoch 8 (0.9804) and then slightly declines, while training $\text{accuracy}$ continues to rise toward 1.0.
* **Conclusion:** Training should ideally be stopped around **Epoch 8** to maximize generalization.

### 3. 20 Epochs Results Analysis (image_f7f0c5.png)

| Metric | Start (Epoch 1) | Optimal (Epoch 8) | End (Epoch 20) |
| :--- | :--- | :--- | :--- |
| **Loss** | 0.2660 | 0.0242 | 0.0045 |
| **Val\_Loss** | 0.1160 | 0.0795 | **0.1388** |
| **Accuracy** | 0.9241 | 0.9926 | 0.9986 |
| **Val\_Accuracy** | 0.9676 | 0.9806 | 0.9732 |

* **Signs of Overfitting (Epoch 20):** **Severe overfitting** is evident.
    * The **Training Loss** drops almost to zero (0.0045), indicating near-perfect memorization of the training data.
    * The **Validation Loss** rises dramatically from its minimum (0.0795 at Epoch 8) to **0.1388** at Epoch 20, which is *worse* than the $\text{val\_loss}$ after just 5 epochs!
    * The $\text{val\_accuracy}$ has dropped from its peak of 0.9806 down to 0.9732.
    * **Key takeaway:** The model has become highly specialized to the training set and has lost its ability to generalize to new data.

---

## 4. Adam Optimizer's Influence on Convergence

The Adam optimizer significantly influenced the **speed** and **stability** of convergence observed in all three runs:

* **Speed (Rapid Initial Convergence):** Adam uses **Momentum (First Moment)**, which allowed the network to quickly overcome the initial high loss. We see this where the $\text{loss}$ drops from $\sim 0.27$ to $\sim 0.06$ in just 4-5 epochs. This fast initial progress is due to Adam accumulating past gradients to smooth the optimization path. 
* **Stability (Smooth Convergence in Later Epochs):** Adam uses the **Second Moment (RMSProp)**, which tracks the magnitude of the squared gradients and adaptively scales the learning rate per weight.
    * As the model approaches the minimum (e.g., after Epoch 5), the gradients become smaller and more noisy.
    * Adam ensures that large, noisy gradients do not cause the optimization to "jump out" of the minimum, providing **stable, fine-tuned updates**. This stability is crucial for achieving high $\text{accuracy}$ (up to $0.99+$) without excessive oscillation.
* **Trade-off:** Adam's efficiency allows the network to reach the minimal $\text{loss}$ quickly, but this rapid convergence also accelerates overfitting, as seen clearly by Epoch 8 where generalization starts to suffer.

