# Genset Fault Detection using Vibration Analysis

## Overview
This project implements a Machine Learning system to detect and classify **6 types of mechanical faults** in electrical generators (gensets) based on vibration signals. 

This project utilizes **Digital Signal Processing (DSP)** techniques—specifically **Fast Fourier Transform (FFT)**—combined with **Principal Component Analysis (PCA)** to create a highly efficient and accurate classification model.

## Dataset Description
The dataset consists of vibration signals acquired from an accelerometer attached to the genset.
* **Sampling Frequency ($f_s$):** 800 Hz
* **Duration:** 5 seconds per sample
* **Data Points:** 4,000 points per sample
* **Total Samples:** 4,320 samples
### Target Classes (Labels)
The system classifies the genset into one of the following 6 conditions:
1.  **NORMAL**: Normal operation
2.  **AIR_FILTER**: Clogged/Damaged Air Filter
3.  **CARBURATOR**: Carburetor issues
4.  **IGN_COIL**: Ignition Coil faults
5.  **SPARK_PLUG**: Spark Plug faults
6.  **OIL**: Dirty/Degraded Oil

## Methodology
To achieve high accuracy with a relatively low number of features, the following pipeline was implemented:
1.  **Data Acquisition:** Raw vibration signals (Time Domain).
2.  **Signal Processing (FFT):** Converted signals from the Time Domain to the **Frequency Domain** using Fast Fourier Transform. This is crucial as mechanical faults often manifest as specific spectral patterns (harmonics) rather than simple time-domain statistics.
3.  **Feature Reduction (PCA):** Applied Principal Component Analysis to reduce the feature space from ~2,000 frequency bins to just **50 principal components**, retaining the most significant variance while reducing computational cost.
4.  **Classification (SVM):** Trained a **Support Vector Machine (SVM)** with an RBF kernel, optimized using `GridSearchCV`.

## Installation & Usage
### Prerequisites
```bash
pip install numpy pandas scikit-learn matplotlib seaborn
```
### Running the Project
1. Clone this repository.
2. Ensure directory looks like this:
├── data/
│   ├── genset_vibration.csv
│   └── genset_label.csv
├── genset.ipynb
└── README.md
3. Run the notebook:
```bash
jupyter notebook genset.ipynb
```

## Results & Evaluation
The model achieved an accuracy of **~93.43%** on the test set using only **50 features**.
### Classification Report
| Class | Precision | Recall | F1-Score |
| --- | --- | --- | --- |
| **AIR_FILTER** | 0.94 | 0.94 | 0.94 |
| **CARBURATOR** | 0.96 | 0.84 | 0.90 |
| **IGN_COIL** | 0.92 | 0.98 | 0.95 |
| **NORMAL** | 0.90 | 0.96 | 0.93 |
| **OIL** | 0.94 | 0.97 | 0.95 |
| **SPARK_PLUG** | 0.96 | 0.91 | 0.93 |
