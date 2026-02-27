# **Banana Ripeness Detection using Machine Learning**

**Project Overview**

This project presents a machine learning–based image classification system designed to automatically detect banana ripeness stages. The model classifies bananas into four categories:

- Unripe

- Ripe

- Overripe

- Rotten

The system aims to support agricultural quality control, retail monitoring, and supply-chain decision-making by providing a reliable, scalable, and low-cost automated solution for fruit assessment. Instead of relying on deep learning, this project demonstrates how classical feature engineering combined with gradient boosting can achieve highly accurate results.
_____________________________________________________________________
Problem Motivation:

Fruit ripeness assessment is traditionally performed through manual inspection, which is subjective, time-consuming, and inconsistent at scale. Bananas undergo rapid visual and textural changes during ripening, making automated detection valuable for reducing waste, improving distribution efficiency, and ensuring product quality.

Automated detection presents several challenges, including lighting variations, background noise, natural color differences, and visual similarity between ripeness stages. This project addresses these challenges using structured feature extraction and a machine learning classifier.
_____________________________________________________________________
**Dataset:**

The dataset was obtained from Kaggle and contains:

- 13,478 banana images

- Four ripeness classes

Original split: 87% training, 8% validation, 4% testing

For improved model performance, the dataset was restructured into:

- 70% Training

- 15% Validation

- 15% Testing

All images were resized to 128 × 128 pixels to balance computational efficiency and feature preservation.
_____________________________________________________________________
**Methodology:**

**Data Preprocessing**

Images were standardized through resizing and color-space transformations. Images were converted into HSV and LAB color spaces to enhance perceptual color differences and lighting representation.

**Color Feature Extraction**

Statistical features were extracted from HSV and LAB channels, including mean and standard deviation values for each channel. These statistics summarize global color and illumination characteristics.

**Brown Spot Detection**

A brown ratio feature was engineered to capture visual indicators associated with ripeness and over-ripeness. Pixels matching predefined brown color ranges in HSV space were detected, and the proportion of such pixels was calculated relative to the total image area.

**Color Histogram Features**

For each HSV channel, normalized 16-bin histograms were computed. These histograms capture overall color distributions rather than simple averages.

**Texture Feature Extraction (HOG)**

Histogram of Oriented Gradients (HOG) was applied after converting images to grayscale. HOG encodes edge orientations and texture patterns, enabling the model to detect structural differences such as spotting and surface texture variations during ripening.

**Feature Vector Construction**

All extracted features were concatenated into a single feature vector per image, combining color statistics, brown ratio, color histograms, and HOG features. Features were scaled using StandardScaler to ensure balanced learning across feature ranges.
_____________________________________________________________________
**Model Training:**

The classification model used is XGBoost, selected for its robustness to noise, efficiency, and strong performance on structured feature data.

Model configuration:

- Objective: multi-class softmax

- Number of classes: 4

- Learning rate: 0.05

- Number of estimators: 400

- Maximum depth: 6

- Subsample: 0.9

- Column sample by tree: 0.9

- Gamma: 0.1

- Minimum child weight: 3

- Evaluation metric: mlogloss

Parameters were tuned using training and validation datasets.
_____________________________________________________________________
**Evaluation Metrics:**

Model performance was evaluated using the following metrics:

- Accuracy

- Precision

- Recall

- F1-score

- Confusion Matrix

Validation accuracy reached 96.14%, indicating effective parameter tuning prior to final testing.
_____________________________________________________________________
**Results:**

The model achieved strong performance across all four ripeness classes:

Class accuracy ranged between 96% and 98%

Macro average accuracy: 97%

Weighted average accuracy: 96%

The confusion matrix demonstrated strong diagonal dominance, indicating correct classification for most samples with minimal inter-class confusion. One class showed slightly lower performance due to visual similarity with neighboring ripeness stages, but overall classification remained highly reliable.
