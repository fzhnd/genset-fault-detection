# Genset Fault Detection Using Machine Learning

This repository implements a **machine learning–based fault detection system** for an electric generator (genset) using **vibration signal data** acquired from an accelerometer sensor.

The system is designed to detect **six operating conditions** of a genset and demonstrates that **high classification accuracy can be achieved using raw vibration signals combined with dimensionality reduction (PCA)**.

## Problem Description

The vibration signals are collected from a genset under different operating conditions:

| Label      | Condition                  |
| ---------- | -------------------------- |
| NORMAL     | Normal operating condition |
| CARBURATOR | Faulty carburator          |
| IGN_COIL   | Faulty ignition coil       |
| AIR_FILTER | Faulty air filter          |
| SPARK_PLUG | Faulty spark plug          |
| OIL        | Dirty oil condition        |

**Signal specifications:**
* Sampling frequency: **800 Hz**
* Signal duration: **5 seconds**
* Total samples per signal: **4000**
* Sensor: Accelerometer (vibration signal)

## Machine Learning Approach
Two machine learning models are implemented:

### 1. Baseline Model – Random Forest + PCA
* Raw vibration signal
* Standardization
* PCA (retain 95% variance → 519 components)
* Random Forest classifier

### 2. Final Model – Optimized SVM + PCA
* Raw vibration signal
* Standardization
* PCA (retain 95% variance → 519 components)
* Support Vector Machine (RBF kernel)
* Hyperparameter tuning using GridSearchCV

## Results
### PCA Information
```
Number of PCA components: 519
```

### Random Forest Performance
```
Accuracy: 0.9694
```

### Optimized SVM Performance
```
Accuracy: 0.975
```

**Confusion Matrix (SVM):**
```
[[175   0   3   0   0   2]
 [  0 173   4   3   0   0]
 [  3   2 175   0   0   0]
 [  0   1   0 179   0   0]
 [  0   0   0   0 179   1]
 [  3   0   0   0   5 172]]
```

**Conclusion:**
The optimized SVM model achieves **97.5% accuracy**, demonstrating excellent performance in detecting all six genset operating conditions.

## How to Run
### 1. Clone the Repository
```bash
git clone https://github.com/fzhnd/genset-fault-detection.git
cd genset-fault-detection
```

### 2. Install Required Dependencies
Make sure Python **≥ 3.8** is installed, then install the required packages:
```bash
pip install numpy pandas scikit-learn jupyter
```

### 3. Check Dataset Structure
Ensure the dataset files are located in the `data/` directory:
```
genset-fault-detection/
│
├── genset.ipynb
├── data/
│   ├── genset_vibration.csv
│   └── genset_label.csv
└── README.md
```

### 4. Run the Notebook
Open and run:
```bash
jupyter notebook genset.ipynb
```
Then execute all cells sequentially (Run All).

## Evaluation Metrics
The system is evaluated using:
* Accuracy
* Precision
* Recall
* F1-score
* Confusion Matrix

Stratified train-test split is applied to ensure balanced class distribution.
