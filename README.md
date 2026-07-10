# 🔋 Lightweight Hybrid CNN-LSTM for Battery SoC Estimation

**Author:** Regan Agam (NIM: 24/PTK/552177/16439)  
**Program:** Master's in Electrical Engineering, Universitas Gadjah Mada (UGM)  
**Course:** Pattern Recognition and Classification Techniques (Teknik Klasifikasi dan Pengenalan Pola)

## 📌 Project Overview
Accurate State of Charge (SoC) estimation is a fundamental pillar in Battery Management Systems (BMS) for Electric Vehicles (EVs). This project proposes and evaluates a compact Hybrid CNN-LSTM architecture for SoC prediction. The model is evaluated through a dual approach: as a **Regression** task to predict continuous values, and as a **Classification** task to categorize battery condition ranges.

## 📊 Dataset & Preprocessing
The dataset used is a primary time-series dataset of battery operational parameters sourced from the `Book45.xlsx` file.
* **Total Data:** 186,715 rows of data.
* **Input Features (6 Features):** `voltage`, `current`, `temp 1`, `temp 2`, `temp 3`, `temp 4`.
* **Target Variable:** `SOC`.

**Preprocessing Pipeline:**
1. **Normalization:** All input features and targets are normalized to a [0, 1] range using `MinMaxScaler`.
2. **Sequence Generation:** Data is transformed into overlapping sequences with a length of 10 *time-steps* to predict the SoC value at the next time step.
3. **Data Split:** The dataset is split in a time-aware manner into training data (70%), validation data (20%), and testing data (10%).

## 🧠 Model Architecture (Lightweight Design)
This model integrates a Conv1D layer for spatial feature extraction and an LSTM layer to capture temporal dependencies. This architecture is specifically designed to be highly efficient with a total of only **23,415 parameters**, making it a practical solution for edge BMS hardware.

![CNN-LSTM Architecture](assets/gambar.png)

* **Input Layer:** Receives sequence data with dimensions (10, 6).
* **Conv1D Layer:** 64 filters, kernel size 3, ReLU activation.
* **LSTM Layer:** 50 units, ReLU activation.
* **Dropout Layer:** Rate 0.2 for regularization.
* **Dense Layer:** 1 output neuron.

## 📈 Results: Regression Performance
Regression evaluation shows an exceptional level of accuracy in predicting continuous SoC values.

| Metric | Score |
| :--- | :---: |
| **Mean Squared Error (MSE)** | 0.0124 |
| **R-squared ($R^2$)** | 0.9870 |

### Training Dynamics
The *validation loss* curve moves parallel to the *training loss* and achieves convergence at a very low value, serving as a strong indicator that the model has good generalization capabilities and is not overfitting.

![Training vs Validation Loss](assets/grafik1.png)

### Time-Series Prediction Tracking
The prediction curve almost perfectly overlaps with the actual curve, confirming the model's ability to track temporal dynamics such as charging and discharging phases, as well as minor fluctuations that occur.

![Actual vs Predicted SoC Time-Series](assets/grafik2.png)

### Prediction Consistency (Scatter Plot)
Data points form a very dense cluster along the main diagonal line, proving a very strong correlation and unbiased performance across the entire SoC range (low, medium, and high).

![Actual vs Predicted SoC Scatter Plot](assets/grafik3.png)

## 📊 Results: Classification Performance
The model's capability is also assessed in automatically categorizing battery status into 5 SoC interval classes. 

| Metric | Score |
| :--- | :---: |
| **Accuracy** | 90.07% |
| **Macro Avg Precision** | 0.90 |
| **Macro Avg Recall** | 0.90 |
| **Macro Avg F1-Score** | 0.90 |

### Confusion Matrix
Most predictions lie along the main diagonal (correct predictions). Minor misclassifications that occur are generally restricted to adjacent classes.

![Confusion Matrix](assets/cm.png)

## 💡 Key Engineering Insights
Achieving an $R^2$ fit of 0.9870 in regression and 90.07% accuracy in classification with a highly lightweight parameterized model (~23k) proves that this Hybrid CNN-LSTM architecture is not only predictively accurate but also reliable and ready to be implemented for real-world BMS applications with limited computational power.

## 🚀 How to Run
1. Clone this repository to your local machine.
2. Open the `TKPP.ipynb` file using Jupyter Notebook or Google Colab.
3. You can read the comprehensive technical report in the `Regan Agam_552177_LR_11102025.pdf` file located inside the `docs/` folder.
