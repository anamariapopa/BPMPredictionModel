### NOTE: To improve prediction accuracy and model relevance, we shifted the target variable to `Calories_Burned`. You can find the optimized version of the project [here](https://github.com/anamariapopa/CaloriesBurnedPrediction.git).


# BPM Prediction Model

A Machine Learning project focused on predicting a gym member's **Average Heart Rate (Avg_BPM)** during physical activity. 

## Data Preprocessing
The most critical phase of the project, ensuring that the model learns from high-quality, unbiased data.

### 1. Data Cleaning & Integrity
* **Safety Copying**: Initialized a deep copy of the raw dataset to maintain data lineage.
* **Duplicate Removal**: Identified and eliminated redundant rows to prevent overfitting.
* **Missing Value Analysis**: Confirmed 0 null values across the entire dataset.
* **Outlier Mitigation**: Applied the **IQR (Interquartile Range)** method to detect and remove statistical noise in numerical features.

### 2. Feature Engineering & Leakage Prevention
* **Feature Dropping**: Removed `Max_BPM` and `Calories_Burned`. 
    * *Why?* Including these would cause **Data Leakage**, as they are post-workout metrics that would allow the model to "cheat" during training by using target-correlated results.
* **Categorical Encoding**: Utilized `OneHotEncoder` for `Gender` and `Workout_Type`.
* **Numerical Scaling**: Applied `StandardScaler` to ensure all numerical inputs (Age, BMI, etc.) have a mean of 0 and a standard deviation of 1.

### 3. Splitting Strategy
* **Train-Test Split (80/20)**: Data was split *before* applying transformations to ensure unbiased evaluation.
* **Strict Fit/Transform Logic**: The scaler and encoder were fitted **only on the training set** and then used to transform the test set, preventing any information from the test set from "leaking" into the training process.

## Modeling & Results
The project compares two distinct algorithms to evaluate their predictive power:

* **Linear Regression**: Used as a baseline model to identify straightforward, linear correlations between physical traits and heart rate.
* **Random Forest Regressor**: Our advanced model, used to capture complex and non-linear patterns that a simple linear model might miss.

### Performance Evaluation
The model's performance (R² score and error metrics) indicates that predicting **Avg_BPM** is highly challenging with the current features:

* **Low Correlation**: Preliminary EDA showed a weak correlation between available predictors and the target variable (`Avg_BPM`).
* **Model Limitations**: Because the physiological response to exercise is highly individual and influenced by factors not present in the dataset (like caffeine intake, stress, or sleep), the models achieved sub-optimal accuracy.
* **Conclusion**: The results suggest that the provided features are not strong predictors for heart rate, leading to high MAE (Mean Absolute Error) and low R² scores.

##  Tech Stack
* **Language**: Python
* **Analysis**: Pandas, NumPy
* **Machine Learning**: Scikit-Learn
* **Visualization**: Matplotlib, Seaborn

