# 🔋 EV Battery Remaining Useful Life (RUL) Prediction

## Overview

This project presents a robust, end-to-end machine learning framework designed to accurately predict the **Remaining Useful Life (RUL)** of Electric Vehicle (EV) batteries. By processing real-world charge/discharge cycle data, the system utilizes advanced techniques—including feature engineering, Principal Component Analysis (PCA) for dimensionality reduction, and a comparative analysis of multiple regression models—to forecast when a battery will reach its end-of-life threshold. The resulting RUL predictions are vital for proactive maintenance, ensuring operational safety, minimizing costs, and promoting sustainable battery lifecycle management.

### Key Features

* **End-to-End ML Pipeline:** Covers data handling, preprocessing, feature engineering, model training (ensemble and deep learning), and performance evaluation.
* **Domain-Specific Feature Engineering:** New features like `Charge_Discharge_Ratio`, `Voltage_Gap`, and `Const_Current_Efficiency` were created to enhance predictive power.
* **Dimensionality Reduction (PCA):** Principal Component Analysis was employed to reduce the feature space while retaining 95% of the explained data variance, improving model efficiency.
* **Comparative Model Analysis:** Benchmarked advanced regressors: XGBoost, Random Forest, LightGBM, and a Long Short-Term Memory (LSTM) network.
* **Optimal Performance:** **LightGBM** was identified as the best-performing model, achieving a high **R² Score of 0.9965** and the lowest **RMSE of 19.03**.
* **Deep Learning (LSTM) Integration:** A sequential LSTM model was developed and fine-tuned using `RandomizedSearchCV` to optimize its time-series prediction capability.
* **Performance Metrics:** Assesses accuracy using Root Mean Squared Error (RMSE), Mean Absolute Error (MAE), and R-squared ($R^2$) score.
* **External Data Prediction:** Demonstrates the model's practical application by predicting RUL on a custom set of battery data.

***

## Project Design and Methodology

The solution follows a structured machine learning workflow, as implemented across the notebook cells:

### 1. Data Loading and Initial Analysis (Cells 2 & 3)

* **Dataset:** The project uses a dataset containing various battery parameters recorded over charge/discharge cycles.
* **Initial Checks:** Confirmed the dataset shape (15,064 rows, 9 columns) and verified that there were no missing values.
* **Scaling:** Feature data was scaled using **`StandardScaler`** to normalize the data distribution.
* **Train-Test Split:** The dataset was split into $80\%$ for training and $20\%$ for testing.

### 2. Feature Engineering (Cell 6)

New features were created by combining existing physical parameters, which often provide more direct indicators of battery health and degradation:

| New Feature | Formula | Description |
| :--- | :--- | :--- |
| `Charge_Discharge_Ratio` | `Charging time (s) / Discharge Time (s)` | Measures charging efficiency relative to discharge duration. |
| `Voltage_Gap` | `Max. Voltage Dischar. (V) - Min. Voltage Charg. (V)` | Represents the overall voltage operating range in a cycle. |
| `Const_Current_Efficiency` | `Time constant current (s) / Charging time (s)` | Indicates the proportion of charging spent in the constant current phase. |

### 3. Dimensionality Reduction (Cell 7)

* **PCA Implementation:** PCA was applied to the 11 engineered features.
* **Component Selection:** **6 principal components** were selected to explain over $95\%$ of the cumulative variance.
* **Data Transformation:** The feature set was reduced and split into training and testing sets.

### 4. Model Training and Evaluation (Cells 8-18)

A comparative benchmark of models was conducted:

| Model | RMSE | MAE | R² Score | Key Insight |
| :--- | :--- | :--- | :--- | :--- |
| **LightGBM** | **19.03** | **7.68** | **0.9965** | Best overall performance (Cell 10). |
| XGBoost | 20.65 | 6.93 | 0.9959 | Highly competitive (Cell 8). |
| Random Forest | 21.34 | 9.57 | 0.9956 | Strong ensemble performance (Cell 9). |
| LSTM (Tuned) | 21.96 | 12.56 | 0.9953 | Improved significantly after tuning (Cell 17). |

* **Model Selection:** **LightGBM** was chosen as the optimal model for final deployment due to its high accuracy and efficiency.

### 5. Prediction with External Data (Cell 24)

The best-performing model (LightGBM) was used to generate RUL predictions for an external dataset, showcasing the framework's readiness for real-world application.

***

## Technologies and Libraries

| Technology | Role in Project |
| :--- | :--- |
| **Python** | Core programming language for the entire pipeline. |
| **Pandas & NumPy** | Data manipulation, cleaning, and mathematical operations. |
| **Scikit-learn** | Scaling, PCA, and model selection. |
| **LightGBM** | **Best-performing model** for RUL regression. |
| **XGBoost** | High-performance gradient boosting model. |
| **Keras / TensorFlow** | Framework for building and tuning the **LSTM** deep learning model. |
| **Matplotlib / Seaborn** | Data visualization and plotting. |
| **`termcolor`** | Enhanced console output for prediction visualization. |
