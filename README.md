# 🩺 Pneumothorax Detection from Chest X-ray Images

> **A Classical Machine Learning Approach for Medical Image Analysis**

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Machine%20Learning-orange)
![Medical Imaging](https://img.shields.io/badge/Medical%20Imaging-DICOM-green)
![License](https://img.shields.io/badge/License-Academic-lightgrey)

---

# Overview

This project presents a complete **medical imaging pipeline** for analysing chest X-ray images using **classical machine learning techniques**.

Using the **SIIM-ACR Pneumothorax Imaging Challenge** dataset, the project develops models capable of:

- Detecting pneumothorax (collapsed lung)
- Predicting patient sex
- Estimating patient age

Unlike many medical imaging projects that rely on deep learning, this work demonstrates that carefully designed handcrafted image features combined with traditional machine learning algorithms can achieve strong predictive performance.

---

# Clinical Background

Pneumothorax is a potentially life-threatening condition caused by the accumulation of air within the pleural cavity, resulting in partial or complete lung collapse.

Rapid diagnosis from chest X-rays is essential for timely clinical intervention. This project investigates whether machine learning can automatically identify pneumothorax from chest radiographs while also learning demographic characteristics directly from medical images.

---

# Dataset

**Dataset: SIIM-ACR Pneumothorax Segmentation Challenge**

The dataset contains:

- **10,675** chest X-ray images
- DICOM image format
- Run-Length Encoded (RLE) segmentation labels
- Patient metadata including age and sex

Dataset distribution:

- Healthy: **8,296**
- Pneumothorax: **2,379**

The project also utilises DICOM metadata for demographic prediction tasks.

---

# Project Objectives

The project consists of three independent tasks.

## Task A — Pneumothorax Detection

Binary classification:

- Healthy
- Pneumothorax

Objective:

Automatically determine whether a chest X-ray contains pneumothorax.

---

## Task B — Patient Sex Prediction

Binary classification:

- Male
- Female

Objective:

Investigate whether anatomical characteristics contained within chest X-rays are sufficient to predict patient sex.

---

## Task C — Patient Age Prediction

Regression problem

Objective:

Estimate patient age directly from chest X-ray images.

---



---

# Image Preprocessing

Each chest X-ray undergoes several preprocessing stages before feature extraction.

### Image Normalisation

- Pixel intensity normalization
- Scale images to the range [0,1]

### Image Resizing

- Original resolution: **1024 × 1024**
- Resized to **128 × 128**

This significantly reduces computational cost while preserving clinically relevant structures.

### CLAHE Enhancement

Contrast Limited Adaptive Histogram Equalization (CLAHE) is applied to improve local image contrast and enhance subtle lung boundaries.

---

# Feature Extraction

Instead of using deep neural networks, handcrafted image descriptors are extracted.

## Global Intensity Statistics

- Mean
- Standard deviation
- Minimum
- Maximum
- Percentiles
- Skewness

(10 features)

---

## Histogram of Oriented Gradients (HOG)

Captures:

- Lung edge information
- Pleural boundary gradients
- Structural shape information

---

## Local Binary Patterns (LBP)

Captures:

- Lung texture
- Local intensity variation
- Tissue appearance

(64 histogram bins)

---

## Quadrant Asymmetry Features

Computes intensity statistics across four image quadrants to capture the unilateral appearance of pneumothorax.

---

## Final Feature Vector

Each chest X-ray is represented by **1,846 handcrafted features**.

---

# Machine Learning Models

Five classical machine learning models are implemented and compared.

- Logistic Regression
- Support Vector Machine (RBF)
- Random Forest
- k-Nearest Neighbours (k-NN)
- XGBoost

Each model is trained using a unified pipeline:

```
StandardScaler
        ↓
PCA (95% variance retained)
        ↓
Machine Learning Model
```

Class imbalance is handled using:

- Class weighting
- SMOTE (evaluated)
- XGBoost scale_pos_weight

---

# Model Evaluation

Classification metrics include:

- ROC-AUC
- Accuracy
- Precision
- Recall
- F1-score
- Sensitivity
- Specificity

Regression metrics include:

- Mean Absolute Error (MAE)
- Root Mean Squared Error (RMSE)
- R² Score

Robustness is assessed using:

- Stratified 5-fold Cross Validation
- Learning Curves
- Permutation Testing
- Confusion Matrices
- ROC Curves

---

# Results

## Task A — Pneumothorax Detection

**Best Model:** Support Vector Machine (RBF)

Performance:

- ROC-AUC: **0.831**
- Accuracy: **79%**
- Macro F1-score: **0.723**

---

## Task B — Sex Prediction

**Best Model:** Support Vector Machine (RBF)

Performance:

- ROC-AUC: **0.964**
- Accuracy: **89.6%**

---

## Task C — Age Prediction

**Best Model:** Lasso Regression

Performance:

- MAE: **10.43 years**
- RMSE: **13.52 years**
- R²: **0.375**

---

# Technologies Used

- Python
- NumPy
- Pandas
- Scikit-learn
- XGBoost
- OpenCV
- scikit-image
- pydicom
- Matplotlib
- Seaborn
- Jupyter Notebook

---


---

# Skills Demonstrated

- Medical Image Analysis
- DICOM Image Processing
- Feature Engineering
- Computer Vision
- Machine Learning
- Image Classification
- Regression Analysis
- Model Evaluation
- Cross Validation
- Class Imbalance Handling
- PCA
- Medical Data Analytics

---

# Future Improvements

Potential extensions include:

- Deep Learning (CNNs)
- U-Net for Pneumothorax Segmentation
- Vision Transformers (ViTs)
- Explainable AI using Grad-CAM
- Multi-label thoracic disease classification
- Clinical deployment as a decision support system

---

# License

This repository was developed for academic purposes as part of a Medical Imaging and Big Data course.
