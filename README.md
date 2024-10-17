# Cyber Attack Detection with Machine Learning

## Overview

In this project, we aim to detect cyber attacks using machine learning algorithms. The dataset comprises various network traffic features such as source and destination IP addresses, ports, protocol, payload size, and attack labels. The primary goal is to accurately classify the network traffic into attack categories using models like **Logistic Regression** and **Random Forest**.

We perform comprehensive **exploratory data analysis (EDA)**, handle missing values, and apply **label encoding** to categorical features to prepare the dataset for machine learning modeling. The models' performance is evaluated using accuracy, confusion matrices, and classification reports, with a focus on detecting even the rare attack classes.

---

## Dataset

The dataset consists of 15 key features:

- **Attack ID**: Unique identifier for each attack.
- **Source IP, Destination IP**: IP addresses involved in the network communication.
- **Source Country, Destination Country**: Countries associated with the IP addresses.
- **Protocol**: Network protocol (TCP, UDP, etc.).
- **Source Port, Destination Port**: Port numbers associated with the connection.
- **Attack Type**: The specific type of cyber attack.
- **Payload Size (bytes)**: Size of the data packet involved in the attack.
- **Detection Label**: Indicates whether the traffic was detected as an attack.
- **Confidence Score**: Probability score of the detection.
- **ML Model**: The machine learning model used for the detection.
- **Affected System**: The system affected by the attack.
- **Port Type**: Type of port used in the communication.
- **Timestamp**: Time at which the event occurred.

---

## Preprocessing Steps

1. **Handling Missing Values**:
   - Missing values in numeric columns (e.g., `Payload Size`, `Confidence Score`) were replaced with the median of the respective columns.
   - Categorical columns (e.g., `Source IP`, `Attack Type`) were imputed with the most frequent value (mode).
   - Columns with excessive missing values, such as `Timestamp`, were dropped to prevent model performance issues.

2. **Label Encoding**:
   - Categorical columns were label-encoded to convert them into numerical values that can be used by machine learning models. These columns include `Source IP`, `Destination IP`, `Attack Type`, `Protocol`, `ML Model`, `Port Type`, and others.
   
3. **Feature Scaling**:
   - Continuous numerical columns like `Payload Size` and `Confidence Score` were scaled using standardization to bring all features into a similar range, improving model performance.

---

## Exploratory Data Analysis (EDA)

Several visualizations were performed to understand the distribution of features and the relationships between them:

- **Attack Type Distribution**: A bar plot showing the frequency of each attack type in the dataset.
- **Protocol Usage**: Pie charts or bar plots to visualize the percentage distribution of different protocols (e.g., TCP, UDP).
- **Source and Destination IP Frequency**: Histograms or bar plots indicating the most common source and destination IPs involved in the attacks.
- **Payload Size Distribution**: A histogram showing the distribution of payload sizes in bytes.
- **Correlation Heatmap**: A heatmap visualizing the correlation between numerical features such as `Payload Size`, `Source Port`, `Destination Port`, and `Confidence Score`.

These visualizations provide insights into data distribution, attack patterns, and potential relationships between different features.

---

## Models Implemented

We applied two machine learning algorithms:

1. **Logistic Regression**: A simple yet powerful classification algorithm used for binary and multiclass classification tasks.
2. **Random Forest Classifier**: An ensemble learning method that builds multiple decision trees and merges their predictions for more accurate and robust classifications.

---

## Model Performance and Results

### Logistic Regression

- **Accuracy**: 81.39%
- **Confusion Matrix**:
    ```
    [[8308 1717    0]
     [1987 7970    0]
     [  13    5    0]]
    ```
- **Classification Report**:
    - **Precision for class 0**: 0.81
    - **Precision for class 1**: 0.82
    - **Precision for class 2 (minority class)**: 0.00

The logistic regression model performed reasonably well with an accuracy of **81.39%**, but it struggled with predicting the minority class (class 2). This is likely due to class imbalance in the dataset.

---

### Random Forest Classifier

- **Accuracy**: 99.90%
- **Confusion Matrix**:
    ```
    [[10025     0     0]
     [    3  9954     0]
     [    9     9     0]]
    ```
- **Classification Report**:
    - **Precision for class 0**: 1.00
    - **Precision for class 1**: 1.00
    - **Precision for class 2 (minority class)**: 0.00

Random Forest achieved a near-perfect accuracy of **99.90%**, predicting the majority classes (0 and 1) with exceptional precision and recall. However, it still struggled with class 2 due to the limited number of examples in that category.

---

## Model Comparison

| Metric                   | Logistic Regression | Random Forest  |
|--------------------------|---------------------|----------------|
| **Accuracy**              | 81.39%              | 99.90%         |
| **Precision (Class 0)**   | 0.81                | 1.00           |
| **Precision (Class 1)**   | 0.82                | 1.00           |
| **Precision (Class 2)**   | 0.00                | 0.00           |
| **Recall (Class 0)**      | 0.83                | 1.00           |
| **Recall (Class 1)**      | 0.80                | 1.00           |
| **Recall (Class 2)**      | 0.00                | 0.00           |

- **Logistic Regression** provides a balance between precision and recall for the majority classes but performs poorly on the minority class (class 2).
- **Random Forest** significantly outperforms Logistic Regression with nearly perfect results for majority classes, but like Logistic Regression, it struggles with the rare attack types due to class imbalance.

---

## Challenges and Solutions

1. **Class Imbalance**:
   - Class 2 (representing the rarest attack type) was significantly under-represented in the dataset, leading to poor performance for this class in both models.
   - **Future Steps**: Use **SMOTE (Synthetic Minority Over-sampling Technique)** or **undersampling** methods to balance the classes and improve minority class detection.

2. **Feature Engineering**:
   - Additional feature engineering could improve model performance. For example, combining features such as `Source IP` and `Protocol` or creating new features from the `Timestamp` column could enhance the model's ability to detect attacks.

---

## Future Work

1. **Advanced Models**: Implement more complex models such as **XGBoost** or **SVM** to further improve classification performance.
2. **Hyperparameter Tuning**: Perform grid search or random search to fine-tune model parameters for optimal performance.
3. **Class Imbalance Handling**: Apply oversampling or undersampling techniques to mitigate class imbalance, improving detection of rare attack types.
4. **Time-Series Analysis**: Incorporate time-based features from the `Timestamp` column to better understand attack trends over time.
5. **Deployment**: Develop a web application to deploy the trained model, allowing real-time cyber attack detection in a network environment.

---

## Conclusion

This project demonstrates the application of machine learning to detect cyber attacks in network traffic. While both Logistic Regression and Random Forest performed well for the majority of attack types, the imbalanced dataset led to poor performance in detecting minority classes. Addressing class imbalance through techniques like SMOTE or cost-sensitive learning will be essential for improving future models.


