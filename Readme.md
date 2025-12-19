# 🧠 Deep Learning Dynamics: An Ablation Study on MNIST

![Banner Image](https://img.shields.io/badge/TensorFlow-2.x-orange.svg) ![Banner Image](https://img.shields.io/badge/Python-3.8+-blue.svg) ![Banner Image](https://img.shields.io/badge/Status-Complete-green.svg)

## **1. Project Overview**
This project is a **hands-on experimental study** of Artificial Neural Networks (ANNs) focused on understanding *how and why* deep learning models behave the way they do during training. Using the **MNIST handwritten digit dataset**, I applied a series of **controlled ablation experiments** to systematically evaluate the effect of training duration, regularization techniques, optimizers, batch sizes, and activation functions.

Rather than optimizing for accuracy alone, the project emphasizes **training dynamics**, including convergence behavior, overfitting, stability, and generalization. All experiments were **implemented, trained, and evaluated within this project**.

---

## **2. Repository Structure**
The repository is organized to clearly separate implementation, results, and analysis.

```text
deep-learning-dynamics/
├── notebook.ipynb             # Main Jupyter Notebook containing all experiments
├── README.md                  # Project documentation (this file)
├── image.png/                 # Custom handwritten digit samples
├── image_2.png
├── image_3.png                    
│   
├── results/                   # Generated plots and visual outputs
│   ├── predictions/           # Model predictions and heatmaps
│   ├── loss_curves/           # Training vs Validation loss curves
│   └── comparisons/           # Optimizer and hyperparameter comparisons
└── submission/                # Detailed markdown analysis per experiment
    ├── Task01_PredictionAnalysis.md
    ├── Task02_CustomDigit.md
    ├── Task03_Epochs.md
    ├── Task04_EarlyStopping.md
    ├── Task05_Dropout.md
    ├── Task06_L2.md
    ├── Task07_Optimizers.md
    ├── Task08_BatchSize.md
    ├── Task09_Activations.md
    └── Task10_Weights.md
```

---

## **3. Methodology & Applied Experiments**
The baseline model used throughout the experiments is a fully connected **Multi-Layer Perceptron (MLP)**:

- **Input Layer:** 784 neurons (28×28 flattened image)
- **Hidden Layer:** 128 neurons (activation varies per experiment)
- **Output Layer:** 10 neurons (Softmax)
- **Loss Function:** Sparse Categorical Crossentropy

All modifications listed below were **explicitly implemented and tested in this project**.

---

### **A. Training Duration (Epoch Study)**
To analyze convergence speed and overfitting behavior, the model was trained using different epoch counts:

- **5 epochs**
- **10 epochs**
- **20 epochs**

This experiment highlights the emergence of the **generalization gap**, where validation loss begins increasing despite continued improvement in training loss.

---

### **B. Dropout Regularization Study**
The model architecture was modified to test the effect of neuron deactivation on generalization:

- **No Dropout**
- **Dropout = 0.1**
- **Dropout = 0.3**

This experiment demonstrates how higher dropout forces the network to learn more robust and redundant feature representations, reducing overfitting.

---

### **C. L2 Weight Regularization (Weight Decay)**
L2 regularization was added to the Dense layers using:

```python
kernel_regularizer=keras.regularizers.l2(0.001)
```

The following L2 values were tested:

- **0.0001**
- **0.001**
- **0.01**

Results show how increasing L2 strength suppresses large weight magnitudes and encourages smoother decision boundaries.

---

### **D. Optimizer Comparison**
Four models with **identical architecture** were trained using different optimization algorithms:

- **SGD** (`learning_rate=0.01`)
- **SGD with Momentum**
- **Adam**
- **AdamW**

This comparison illustrates the trade-off between convergence speed, stability, and generalization performance.

---

### **E. Batch Size Experiments**
To study gradient noise and convergence behavior, the model was trained with batch sizes:

- **8**
- **32**
- **128**

Smaller batch sizes introduced noisier gradients, while larger batches converged faster but to sharper minima.

---

### **F. Activation Function Analysis**
The ReLU activation function was replaced to evaluate non-linearity effects:

- **Tanh**
- **Softsign**
- **GELU**

This experiment demonstrates how smoother activations like GELU improve gradient flow and convergence compared to traditional ReLU.

---

## **4. Key Findings**
- Overfitting becomes evident after a limited number of epochs without regularization.
- Dropout and L2 regularization significantly reduce the training–validation gap.
- Adam and AdamW converge faster than SGD, but AdamW provides better long-term stability.
- Batch size directly affects gradient noise and generalization behavior.
- Activation choice has a measurable impact on convergence speed and model robustness.

---

## **5. How to Run the Project**

Clone the repository:
```bash
git clone https://github.com/osamaa004/Task_02-ANN-MNIST-Dataset-
```

Create a virtual environment (optional):
```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
```

Install dependencies:
```bash
pip install tensorflow numpy pandas matplotlib opencv-python
```

Launch the notebook:
```bash
jupyter notebook notebook.ipynb
```

---

**Author:** Osama Magdy Ali Khalifa  
**Course:** Generative AI

