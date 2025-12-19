# Batch Size Impact Analysis

This report examines the performance of the model across three different batch sizes: **8**, **32**, and **128**.

---

## 1. Experimental Results Data Table

The following metrics were captured at the final epoch (Epoch 5) for each configuration:

| Batch Size | Steps per Epoch | Training Loss | Training Acc | Val Loss | Val Acc |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **8** | 7500 | 0.0886 | 97.47% | **0.0818** | 98.11% |
| **32** | 1875 | **0.1098** | **97.83%** | 0.1085 | **98.12%** |
| **128** | 469 | 0.3541 | 93.68% | 0.2854 | 96.18% |

---

## 2. Key Insights from Your Data

### The Relationship Between Batch Size and Update Frequency
In deep learning, the model updates its weights once per batch (step). 
* **Batch Size 8:** Performed **7,500 updates** per epoch. This high frequency of updates allows the model to learn much faster within the same number of epochs, explaining why it achieved a very low validation loss (**0.0818**).
* **Batch Size 128:** Performed only **469 updates** per epoch. Because it had nearly 16x fewer opportunities to adjust its weights compared to batch 8, the accuracy is noticeably lower (**96.18%**).



### Generalization and "Noise"
Smaller batch sizes (8 and 32) introduce more "stochastic noise" into the training process. This noise acts as a natural regularizer, helping the optimizer "jump" out of sharp local minima and find broader, flatter minima that generalize better to the validation set.

* **Observation:** Notice that for **Batch 32**, the Validation Accuracy (**98.12%**) is higher than the Training Accuracy (**97.83%**). This is a strong indicator of excellent generalization.



---

## 3. Comparative Summary

| Feature | Batch Size 8 | Batch Size 32 | Batch Size 128 |
| :--- | :--- | :--- | :--- |
| **Training Speed** | Slowest (High overhead) | Balanced | **Fastest (Efficient)** |
| **Accuracy** | Very High | **Highest** | Lower |
| **Memory Usage** | Lowest | Moderate | Highest |
| **Gradient Stability** | Low (Noisy) | **Stable** | Very Stable |

---

## 4. Final Conclusion
While **Batch Size 8** yielded the lowest validation loss, **Batch Size 32** provided the best balance of training accuracy and validation performance. **Batch Size 128** appears to require more epochs or a higher learning rate to match the performance of the smaller batches, as it is under-fitting the data within the 5-epoch limit.