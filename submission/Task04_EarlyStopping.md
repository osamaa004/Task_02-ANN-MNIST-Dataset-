## 🛑 Early Stopping Analysis

The analysis is based on the Early Stopping criterion: `keras.callbacks.EarlyStopping(patience=3, restore_best_weights=True)`. This means training stops if the $\text{val\_loss}$ does not improve for 3 consecutive epochs, and the final model restores the weights from the epoch with the lowest $\text{val\_loss}$.

We will use **Run A (image\_f7e1fc.png)** to demonstrate `patience=3`.

### 1. At which epoch did training stop? (Run A: Patience=3)

We trace the $\text{val\_loss}$ in **Run A (image\_f7e1fc.png)**:

| Epoch | $\text{val\_loss}$ | Best $\text{val\_loss}$ so far | Count of Non-Improving Epochs | Action |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 0.1184 | 0.1184 | 0 | |
| 2 | 0.0909 | 0.0909 | 0 | Improvement |
| 3 | 0.0986 | 0.0909 | 1 | No Improvement |
| 4 | 0.0880 | 0.0880 | 0 | Improvement (New Best) |
| 5 | 0.0850 | 0.0850 | 0 | Improvement (New Best) |
| 6 | 0.0801 | 0.0801 | 0 | Improvement (New Best) |
| 7 | **0.0740** | **0.0740** | 0 | **Best Epoch!** |
| 8 | 0.0843 | 0.0740 | 1 | No Improvement (Count 1) |
| 9 | 0.0826 | 0.0740 | 2 | No Improvement (Count 2) |
| 10 | 0.0885 | 0.0740 | **3** | No Improvement (Count 3) |

**Result:** Training stops **after Epoch 10** because the validation loss failed to improve for 3 consecutive epochs (8, 9, and 10). The final model's weights would be restored to the state from **Epoch 7**.

### 2. Why does the validation loss control this decision?

* **Goal:** The primary goal of training is **generalization**—performance on unseen data.
* **Overfitting Sentinel:** The $\text{val\_loss}$ acts as a proxy for generalization error. As training progresses, the training loss ($\text{loss}$) continues to drop (memorization), but the $\text{val\_loss}$ eventually stops decreasing or starts to increase. 
* **Decision Trigger:** Early Stopping uses the increase in $\text{val\_loss}$ as the critical signal that the model is beginning to **overfit** and stops the process before generalization performance is severely degraded.

### 3. What happens if you increase patience (e.g., to 5)?

If **patience is increased** (e.g., from 3 to 5):

* **Effect:** The training allows the model to continue past the initial optimal point for a longer duration. This provides the model **more opportunity** to potentially find a lower $\text{val\_loss}$ minimum if the loss landscape is noisy or bumpy.
* **Trade-off:**
    * **Benefit:** Reduces the risk of **stopping prematurely** due to a temporary spike in $\text{val\_loss}$.
    * **Risk:** Increases the risk of **severe overfitting**, as the model spends much more time training past the point where the $\text{val\_loss}$ first plateaued, often leading to larger final $\text{val\_loss}$ if the weights are not restored. (This is evidenced in **Run B (image\_f7e1bf.png)**, which runs past the `patience=3` stop point).

### 4. Would a different optimizer (e.g., SGD) change the Early Stopping pattern?

**Yes, a different optimizer like SGD (Stochastic Gradient Descent) would change the pattern.**

* **Convergence Style:** SGD converges much **slower** and with **more oscillation** compared to Adam. 
* **Effect on Early Stopping:**
    * The epoch where the minimum $\text{val\_loss}$ is reached would likely be **higher**.
    * The noise and oscillations in the $\text{val\_loss}$ curve would make the **patience** hyperparameter even more critical. A low patience (like 3) might mistakenly stop the training after a few temporary spikes, even if the model was still on a good path, thus requiring a higher patience value.

### 5. Explain how EarlyStopping acts as an indirect form of regularization.

**Regularization** is the process of adding constraints to reduce overfitting and encourage generalization.

* **Mechanism:** Early Stopping prevents the model from continuing to train until the training $\text{loss}$ is near zero (perfect memorization).
* **Indirect Regularization:** By stopping early (e.g., at Epoch 7), Early Stopping effectively constrains the size of the model's weights.
    * Weights start near zero and grow larger as the model overfits.
    * Stopping before the weights become excessively large (which would happen at Epoch 20) keeps the model simpler and smoother. This enforcement of simpler, smaller weights is the core function of explicit regularization techniques (like L2 weight decay), making Early Stopping an **indirect, temporal form of regularization**.