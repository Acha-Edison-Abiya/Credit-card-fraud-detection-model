# Credit-card-fraud-detection-model
This project aims to build a fraud detection model using machine learning algorithm train on historical data and then use the model to detect future fraudulent transactions.  It is an end-to-end project built using Synapse Data Science in microsoft fabric.  

# Credit Card Fraud Detection Model

## Objective

The objective of this project is to build a fraud detection model using machine learning to identify and prevent fraudulent credit card transactions. The model is trained on historical transaction data and aims to detect fraudulent activity in real-time. This is an end-to-end project built using Synapse Data Science in Microsoft Fabric.

## Dataset

The dataset consists of credit card transactions made by European cardholders over a two-day period in September 2013. It contains the following features:

- V1 to V28: Principal components derived from a PCA transformation of the original transaction features, ensuring confidentiality and reducing dimensionality.
- Time: The number of seconds elapsed between each transaction and the first transaction in the dataset.
- Amount: The monetary value of each transaction.
- Class: The target variable, where 1 indicates a fraudulent transaction and 0 indicates a legitimate transaction.

The dataset contains 284,807 transactions, with only 492 classified as fraudulent, representing approximately 0.172% of the dataset. This significant class imbalance poses a challenge for machine learning models and is addressed during data preprocessing.

## Methodology

### Data Loading and Preprocessing:
- The dataset is loaded into Microsoft Fabric’s lakehouse, and the target column is cast to integer type.
- The data is cleaned, including handling missing values and duplicate records.
- Exploratory Data Analysis (EDA) is conducted to understand the distribution of the target variable, transaction amounts, and transaction times.
### Handling Class Imbalance:
- Due to the severe class imbalance, the SMOTE (Synthetic Minority Over-sampling Technique) method is applied to the training data to generate synthetic samples of the minority class (fraudulent transactions).
### Model Training:
- A LightGBM model is trained on the balanced dataset created using SMOTE.
- Feature importance is determined and logged, and the model’s performance is evaluated using metrics such as AUROC (Area Under the Receiver Operating Characteristic) and AUPRC (Area Under the Precision-Recall Curve).
### Model Evaluation:
- The model is evaluated using a confusion matrix to analyze the true positives, true negatives, false positives, and false negatives.
- AUC-ROC and AUPRC metrics are calculated to assess the model’s ability to distinguish between fraudulent and non-fraudulent transactions.
### Batch Predictions and Deployment:
- The trained model is registered in MLflow and used to generate batch predictions.
- The predictions are saved to the lakehouse for further analysis or integration with other systems.

## Results
### Key Insights from EDA
- 1. Class Imbalance: The dataset is highly imbalanced, with fraudulent transactions accounting for only 0.172% of the total transactions. This imbalance required the application of SMOTE (Synthetic Minority Over-sampling Technique) to balance the training data and improve the model’s ability to detect fraud.
    ![image](https://github.com/user-attachments/assets/c560901c-db63-40c3-a407-5bd9f1703d08)
- 2.	Feature Distribution:
- Transaction Amount: Fraudulent transactions generally had lower amounts compared to non-fraudulent ones. This insight can help in identifying suspicious low-value transactions that might otherwise go unnoticed.
  ![image](https://github.com/user-attachments/assets/4d6113bd-cb3f-462d-9eb1-bcc7f8c80577)
- Transaction Time: No significant difference was observed in the distribution of transaction times between fraudulent and non-fraudulent transactions, indicating that time alone is not a strong indicator of fraud.
- ![image](https://github.com/user-attachments/assets/56ffb348-6273-4b5b-aee5-b888c61e4d97)
### Key Insights from model
- 1. Model Performance:
- LightGBM Model: The LightGBM model, trained on the SMOTE-balanced dataset, performed well in identifying fraudulent transactions. The model’s performance was evaluated using AUROC and AUPRC metrics, both of which indicated strong predictive capability.
- 2. Confusion Matrix: The model successfully identified a high number of true positives (correctly detected frauds) with a manageable number of false positives (legitimate transactions incorrectly flagged as fraud). This balance is crucial for minimizing potential disruptions to legitimate customers.
- 3. Feature Importance: The analysis of feature importance revealed that certain PCA-transformed features (V1 to V28) were more influential in predicting fraudulent activity. These insights can guide further refinement of fraud detection strategies by focusing on the most predictive variables.
- 4. Model Deployment: The final model was registered and deployed, enabling batch predictions on new data.

## Actionable Recommendations
###### 1. Implement the Fraud Detection Model in Real-Time Systems:
Deploy the trained LightGBM model into the bank’s transaction processing system to monitor transactions in real-time. This will enable the early detection of potentially fraudulent transactions, allowing the bank to take immediate action to prevent financial losses.
###### 2. Enhance Monitoring of Low-Value Transactions:
Given that fraudulent transactions often involve lower amounts, the bank should implement stricter monitoring and additional verification steps for low-value transactions. This can include flagging unusual transaction patterns or requiring additional authentication for suspicious low-value transactions.
###### 3. Regularly Update and Retrain the Model:
Fraud patterns evolve over time, so it is crucial to regularly update and retrain the fraud detection model using the latest transaction data. This ensures the model remains effective in identifying new and emerging fraud tactics.
###### 4. Use Feature Importance for Targeted Monitoring:
Focus on the most predictive features identified by the model when designing fraud prevention strategies. By monitoring these key indicators more closely, the bank can improve its ability to detect fraud earlier in the transaction lifecycle.
###### 5. Balance Fraud Detection with Customer Experience:
While it is essential to prevent fraud, it is equally important to minimize false positives to avoid inconveniencing legitimate customers. Implement a tiered alert system that differentiates between high-risk and low-risk fraud alerts, allowing the bank to respond appropriately without disrupting customer experience.
###### 6. Conduct Regular Audits and Model Performance Reviews:
Periodically review the performance of the fraud detection model, including the confusion matrix, AUROC, and AUPRC metrics, to ensure it continues to meet the bank’s accuracy and efficiency standards. Regular audits can help identify areas for improvement and ensure compliance with regulatory requirements.
###### 7.	Expand Data Collection to Improve Model Accuracy:
Consider collecting additional data points, such as customer behavioral data, transaction location, and device information, to enhance the model’s accuracy. Incorporating more diverse data sources can help the model better differentiate between legitimate and fraudulent transactions.
