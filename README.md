# Decision-Tree-Model-Evaluation

# Project Summary: Decision Tree Classification - Airline Customer Satisfaction Classification

## 1. Dataset Overview

This project analyzes the `invistico_Airline1.csv` dataset, which contains customer satisfaction survey data for an airline. The dataset includes various features related to passenger demographics, flight details, and service ratings, with the target variable being `satisfaction` (binary: 'satisfied' or 'not satisfied').

## 2. Modeling Approach

The goal was to build and optimize a Decision Tree classifier to predict airline customer satisfaction, compare its performance and interpretability against a Logistic Regression model, and provide actionable insights for airline management.

### Data Preparation:

*   Loaded the `invistico_Airline1.csv` dataset.
*   Dropped irrelevant columns.
*   Handled missing values in 'Arrival Delay in Minutes' by imputing with the mean.
*   Encoded categorical features ('Customer Type', 'Type of Travel', 'Class') and the target variable ('satisfaction') using Label Encoding.
*   Split the data into training and testing sets (70% train, 30% test) with `stratify=y` to maintain the proportion of satisfaction classes.

## 3. Decision Tree Optimization

### Tuning Strategy:

`GridSearchCV` was employed to optimize the Decision Tree classifier's hyperparameters, specifically:

*   `max_depth`: `[None, 5, 10, 15, 20]`
*   `min_samples_split`: `[2, 5, 10, 20]`
*   `min_samples_leaf`: `[1, 2, 4, 8]`

The optimization used 5-fold cross-validation and `f1_weighted` as the scoring metric to handle potential class imbalance and balance precision and recall across both classes.

### Best Hyperparameters Found:

*   `max_depth`: 20
*   `min_samples_leaf`: 4
*   `min_samples_split`: 20

### Decision Tree Performance (on Test Set):

*   **F1-score for 'Satisfied' class:** 0.9461

## 4. Feature Importance

The Decision Tree model identified the following top operational drivers of customer satisfaction:

| Feature                    | Importance |
| :------------------------- | :--------- |
| Inflight entertainment     | 0.4377     |
| Seat comfort               | 0.1942     |
| Ease of Online booking     | 0.0692     |
| Customer Type              | 0.0471     |
| Online support             | 0.0384     |
| Type of Travel             | 0.0379     |
| Flight Distance            | 0.0305     |
| Inflight service           | 0.0270     |
| Class                      | 0.0195     |
| Checkin service            | 0.0101     |

`Inflight entertainment` and `Seat comfort` emerged as the most significant factors influencing customer satisfaction, indicating that these areas are critical for airline management to focus on for improvements.

## 5. Comparison with Logistic Regression

To provide a comprehensive view, the Decision Tree model's performance and interpretability were compared against a Logistic Regression model.

### Logistic Regression Performance (on Test Set):

*   **F1-score for 'Satisfied' class:** 0.8411

### Trade-offs:

*   **Performance:** The optimized **Decision Tree (F1-score: 0.9461)** significantly outperformed the **Logistic Regression (F1-score: 0.8411)** on the 'Satisfied' class, suggesting that the non-linear relationships and interactions captured by the Decision Tree are crucial for this dataset.
*   **Interpretability:**
    *   **Decision Tree:** Offers high interpretability through its visual tree structure and direct feature importance, making it transparent and auditable for non-technical users to understand the decision logic and identify actionable insights.
    *   **Logistic Regression:** While its coefficients provide insight into feature impact, it assumes linear relationships and is less intuitive for explaining complex decision pathways to stakeholders.
*   **Business Actionability:** The Decision Tree provides more direct and specific actionable insights (e.g., improve inflight entertainment for customers with certain comfort levels), allowing for targeted operational strategies.

## Conclusion

The Decision Tree classifier proved to be more effective for this dataset due to its superior performance and higher interpretability, offering clear, actionable insights for airline management to enhance customer satisfaction by focusing on key drivers like inflight entertainment and seat comfort. The `plot_tree` visualization serves as a transparent tool for communicating classification logic to stakeholders.
