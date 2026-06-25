# EDA Summary Report: Student Exam Performance Dataset

**Author:** Data Science Analysis
**Date:** March 30, 2026
**Dataset:** Student Exam Performance Dataset

---

## 1. Executive Summary

This report presents the findings from an Exploratory Data Analysis (EDA) performed on a dataset of 10,000 students. The dataset contains demographic, behavioral, and academic performance information. The analysis reveals key factors influencing student exam performance and provides insights for predictive modeling.

### Key Highlights
- **Dataset is clean** with no missing values
- **51.4% failure rate** indicates a challenging academic environment
- **Previous GPA** is the strongest predictor of final exam score (r = +0.89)
- **Study hours** positively correlate with performance (r = +0.58)
- **Social media usage** negatively impacts exam scores (r = -0.25)

---

## 2. Dataset Overview

### 2.1 Basic Information

| Metric | Value |
|--------|-------|
| Total Records | 10,000 students |
| Total Features | 23 columns |
| Numerical Features | 14 |
| Categorical Features | 9 |
| Missing Values | 0 |
| Duplicate Records | 0 |

### 2.2 Feature Categories

| Category | Features | Count |
|----------|----------|-------|
| Demographics | student_id, gender, age, parental_education, family_income | 5 |
| Study Environment | internet_access, study_environment, study_hours_per_day | 3 |
| Engagement | attendance_rate, assignment_completion_rate, participation_score, online_courses_completed, tutoring | 5 |
| Lifestyle | sleep_hours, social_media_hours | 2 |
| Subject Scores | math_score, reading_score, writing_score, science_score | 4 |
| Target Variables | final_exam_score, previous_gpa, pass_fail, grade_category | 4 |

---

## 3. Target Variable Analysis

### 3.1 Final Exam Score Statistics

| Statistic | Value |
|-----------|-------|
| Mean | 49.68 |
| Standard Deviation | 12.15 |
| Minimum | 4.40 |
| 25th Percentile | 41.50 |
| Median (50th) | 49.50 |
| 75th Percentile | 57.60 |
| Maximum | 97.80 |

**Distribution:** The final exam scores follow an approximately normal distribution centered around 50.

### 3.2 Pass/Fail Distribution

| Status | Count | Percentage |
|--------|-------|------------|
| Fail | 5,142 | 51.4% |
| Pass | 4,858 | 48.6% |

**Insight:** The dataset is nearly balanced for binary classification (pass/fail).

### 3.3 Grade Category Distribution

| Grade | Count | Percentage |
|-------|-------|------------|
| A | 10 | 0.1% |
| B | 85 | 0.9% |
| C | 904 | 9.0% |
| D | 3,829 | 38.3% |
| F | 5,172 | 51.7% |

**Insight:** The grade distribution is heavily skewed toward lower grades (D and F account for 90%). This indicates:
- Challenging exam difficulty
- Potential need for grade adjustment or intervention programs
- Imbalanced classification problem for multi-class tasks

---

## 4. Categorical Features Analysis

### 4.1 Gender Distribution

| Gender | Count | Percentage |
|--------|-------|------------|
| Male | 5,013 | 50.1% |
| Female | 4,987 | 49.9% |

**Performance by Gender:**
| Gender | Mean Score | Std Dev |
|--------|------------|---------|
| Female | 49.81 | 12.18 |
| Male | 49.56 | 12.12 |

**Insight:** Gender distribution is balanced with no significant performance difference.

### 4.2 Parental Education Distribution

| Education Level | Count | Percentage | Mean Score |
|-----------------|-------|------------|------------|
| High School | 3,926 | 39.3% | 49.42 |
| Bachelor | 3,502 | 35.0% | 49.90 |
| Master | 2,047 | 20.5% | 49.78 |
| PhD | 525 | 5.3% | 49.79 |

**Insight:** Parental education level has minimal impact on student exam performance.

### 4.3 Family Income Distribution

| Income Level | Count | Percentage |
|--------------|-------|------------|
| Medium | 5,068 | 50.7% |
| Low | 2,971 | 29.7% |
| High | 1,961 | 19.6% |

### 4.4 Study Environment Distribution

| Environment | Count | Percentage |
|-------------|-------|------------|
| Quiet | 4,073 | 40.7% |
| Moderate | 3,947 | 39.5% |
| Noisy | 1,980 | 19.8% |

### 4.5 Other Categorical Features

| Feature | Category | Count | Percentage |
|---------|----------|-------|------------|
| Internet Access | Yes | 8,986 | 89.9% |
| | No | 1,014 | 10.1% |
| Tutoring | No | 7,004 | 70.0% |
| | Yes | 2,996 | 30.0% |

---

## 5. Numerical Features Analysis

### 5.1 Descriptive Statistics

| Feature | Mean | Std | Min | Max |
|---------|------|-----|-----|-----|
| study_hours_per_day | 3.02 | 1.63 | 0.00 | 7.99 |
| attendance_rate | 85.09 | 13.63 | 40.00 | 100.00 |
| sleep_hours | 7.01 | 1.35 | 2.90 | 11.30 |
| social_media_hours | 2.50 | 2.00 | 0.00 | 10.90 |
| assignment_completion_rate | 80.12 | 19.80 | 0.00 | 100.00 |
| participation_score | 69.97 | 20.30 | 0.00 | 100.00 |
| online_courses_completed | 2.50 | 2.87 | 0 | 9 |
| previous_gpa | 1.98 | 0.74 | 0.00 | 4.00 |

### 5.2 Subject Scores Statistics

| Subject | Mean | Std | Min | Max |
|---------|------|-----|-----|-----|
| Math Score | 49.50 | 13.88 | 0.00 | 100.00 |
| Reading Score | 49.76 | 13.36 | 0.00 | 100.00 |
| Writing Score | 49.65 | 13.44 | 0.00 | 100.00 |
| Science Score | 49.76 | 13.83 | 4.80 | 100.00 |

**Insight:** All subject scores have similar distributions, centered around 50.

---

## 6. Correlation Analysis

### 6.1 Top Correlations with Final Exam Score

| Feature | Correlation | Direction |
|---------|-------------|-----------|
| previous_gpa | +0.8912 | Strong Positive |
| writing_score | +0.8745 | Strong Positive |
| reading_score | +0.8725 | Strong Positive |
| math_score | +0.8639 | Strong Positive |
| science_score | +0.8627 | Strong Positive |
| study_hours_per_day | +0.5758 | Moderate Positive |
| social_media_hours | -0.2463 | Weak Negative |
| assignment_completion_rate | +0.1707 | Weak Positive |
| attendance_rate | +0.1506 | Weak Positive |
| participation_score | +0.1239 | Weak Positive |
| sleep_hours | +0.0279 | Negligible |
| online_courses_completed | -0.0185 | Negligible |
| age | -0.0082 | Negligible |

### 6.2 Strongly Correlated Features (|r| >= 0.5)

The following features have strong correlation with final exam score and are recommended as key predictors:

1. **previous_gpa** (+0.89) - Historical academic performance
2. **writing_score** (+0.87) - Writing subject score
3. **reading_score** (+0.87) - Reading subject score
4. **math_score** (+0.86) - Math subject score
5. **science_score** (+0.86) - Science subject score
6. **study_hours_per_day** (+0.58) - Daily study time

### 6.3 Subject Score Correlations

| | math | reading | writing | science |
|--|------|---------|---------|---------|
| math | 1.000 | 0.745 | 0.742 | 0.761 |
| reading | 0.745 | 1.000 | 0.758 | 0.749 |
| writing | 0.742 | 0.758 | 1.000 | 0.741 |
| science | 0.761 | 0.749 | 0.741 | 1.000 |

**Insight:** All subject scores are highly correlated with each other (r > 0.74), suggesting students who perform well in one subject tend to perform well in others.

---

## 7. Outlier Analysis

### 7.1 Outliers Detected (IQR Method)

| Feature | Outliers | Lower Bound | Upper Bound |
|---------|----------|-------------|-------------|
| study_hours_per_day | 27 | -0.24 | 6.28 |
| attendance_rate | 36 | 57.84 | 112.34 |
| sleep_hours | 63 | 4.31 | 9.72 |
| social_media_hours | 36 | -1.50 | 6.50 |
| assignment_completion_rate | 30 | 40.50 | 119.70 |
| participation_score | 35 | 29.35 | 110.55 |
| final_exam_score | 95 | 17.60 | 81.60 |
| previous_gpa | 62 | 0.50 | 3.46 |

**Insight:** The dataset has relatively few outliers (< 1% for most features), indicating good data quality.

---

## 8. Key Insights and Recommendations

### 8.1 Key Findings

1. **Clean Dataset**: No missing values and minimal outliers make this dataset ready for modeling.

2. **Academic History Matters**: Previous GPA is the strongest predictor (r = 0.89) of final exam performance.

3. **Subject Scores are Predictive**: All four subject scores have strong positive correlations (r > 0.86) with final exam score.

4. **Study Time Impact**: Students who study more hours per day tend to score higher (r = 0.58).

5. **Social Media Distraction**: Higher social media usage correlates with lower exam scores (r = -0.25).

6. **Demographics Have Minimal Impact**: Gender, parental education, and family income show little to no correlation with exam performance.

7. **Imbalanced Grade Distribution**: 90% of students fall into D or F categories, making multi-class classification challenging.

8. **Balanced Pass/Fail**: The binary target (pass/fail) is nearly balanced (48.6% vs 51.4%).

### 8.2 Recommendations for Modeling

#### For Regression Tasks (predicting final_exam_score):
- **Primary Features**: previous_gpa, study_hours_per_day
- **Secondary Features**: All subject scores (if available as predictors)
- **Optional Features**: assignment_completion_rate, attendance_rate

#### For Classification Tasks (predicting pass_fail):
- The balanced dataset is suitable for standard classification algorithms
- Consider using subject scores as features if available before final exam

#### For Multi-class Classification (predicting grade_category):
- Address class imbalance using techniques like:
  - SMOTE (Synthetic Minority Over-sampling)
  - Class weights
  - Focal loss
- Consider grouping A/B and C grades to reduce imbalance

### 8.3 Feature Engineering Suggestions

1. **Average Subject Score**: Create a feature averaging all four subject scores
2. **Study Efficiency**: Ratio of study_hours_per_day to social_media_hours
3. **Engagement Score**: Combined metric from attendance, participation, and assignment completion
4. **Academic Risk Flag**: Binary flag for students with low previous_gpa (< 2.0)

---

## 9. Visualizations Generated

The following visualizations have been saved to the `docs/` folder:

| File Name | Description |
|-----------|-------------|
| categorical_distributions.png | Distribution of all categorical features |
| histograms_key_features.png | Histogram of key numerical features |
| boxplots_key_features.png | Boxplots for outlier detection |
| boxplots_subject_scores.png | Subject score distributions |
| final_exam_score_distribution.png | Distribution with normal curve fit |
| final_score_by_passfail.png | Score distribution by pass/fail status |
| scatterplots_vs_final_score.png | Scatter plots of features vs target |
| regression_plots.png | Regression plots for important features |
| correlation_heatmap.png | Full correlation matrix heatmap |
| correlation_with_target.png | Bar chart of correlations with target |
| pairplot_selected_features.png | Pairwise relationships |
| grade_analysis.png | Grade distribution analysis |

---

## 10. Conclusion

This EDA provides a comprehensive understanding of the student exam performance dataset. The analysis reveals that academic history (previous GPA) and study behavior (study hours) are the most important predictors of exam performance. The dataset is clean and well-structured, making it suitable for various machine learning tasks including regression, binary classification, and multi-class classification (with appropriate handling of class imbalance).

The findings suggest that interventions aimed at increasing study time and reducing social media usage could positively impact student performance. Additionally, students with low previous GPA should be identified early for additional academic support.

---

## 11. Model Building Results

### 11.1 Regression Models Performance

| Model | R² Score | RMSE | MAE |
|-------|----------|------|-----|
| GradientBoosting | 0.9740 | 1.95 | 1.56 |
| Linear | 0.9739 | 1.96 | 1.55 |
| Ridge | 0.9739 | 1.96 | 1.55 |
| RandomForest | 0.9728 | 2.00 | 1.58 |
| Lasso | 0.9671 | 2.19 | 1.74 |
| SVR | 0.9576 | 2.49 | 1.89 |
| DecisionTree | 0.9464 | 2.80 | 2.25 |
| KNN | 0.9271 | 3.27 | 2.60 |

**Best Regression Model:** GradientBoosting with R² = 0.9740

### 11.2 Binary Classification Models Performance

| Model | Accuracy | Precision | Recall | F1 Score |
|-------|----------|-----------|--------|----------|
| SVM | 0.9500 | 0.9504 | 0.9465 | 0.9485 |
| GradientBoosting | 0.9495 | 0.9532 | 0.9424 | 0.9478 |
| LogisticRegression | 0.9470 | 0.9492 | 0.9414 | 0.9452 |
| RandomForest | 0.9470 | 0.9501 | 0.9403 | 0.9452 |
| NaiveBayes | 0.9250 | 0.9014 | 0.9496 | 0.9248 |
| DecisionTree | 0.9250 | 0.9255 | 0.9198 | 0.9226 |
| KNN | 0.9130 | 0.9122 | 0.9084 | 0.9103 |

**Best Classification Model:** SVM with F1 = 0.9485

### 11.3 Multi-Class Classification Performance

| Model | Accuracy | F1 (weighted) |
|-------|----------|---------------|
| RandomForest | 1.0000 | 1.0000 |
| GradientBoosting | 1.0000 | 1.0000 |
| LogisticRegression | 0.9890 | 0.9892 |

**Best Multi-class Model:** RandomForest with 100% accuracy

---

## 12. Hyperparameter Tuning Results

### 12.1 Tuned Regression (GradientBoosting)
- **Best Parameters:** n_estimators=100, max_depth=3, learning_rate=0.1, min_samples_split=2, min_samples_leaf=1
- **Test R²:** 0.9740
- **Test RMSE:** 1.9524

### 12.2 Tuned Classification (SVM)
- **Best Parameters:** kernel='linear', C=0.1, gamma=0.1
- **Test Accuracy:** 0.9470
- **Test F1:** 0.9452

### 12.3 Multi-Class Classification (RandomForest)
- **Accuracy:** 100%
- **F1 (weighted):** 100%
- **Classes:** A, B, C, D, F

---

## 13. Saved Models

| Model File | Description |
|------------|-------------|
| best_regression_model.pkl | Best regression model (GradientBoosting) |
| best_classification_model.pkl | Best binary classification model (SVM) |
| tuned_regression_model.pkl | Tuned GradientBoosting regressor |
| tuned_classification_model.pkl | Tuned SVM classifier |
| best_multiclass_model.pkl | Multi-class classifier (RandomForest) |
| grade_encoder.pkl | Label encoder for grade categories |

---

## 14. Generated Visualizations

| File Name | Description |
|-----------|-------------|
| regression_models_comparison.png | Bar chart comparing regression models |
| feature_importance.png | Top 10 feature importance from best regressor |
| classification_models_comparison.png | Bar chart comparing classification models |
| confusion_matrix.png | Confusion matrix for best binary classifier |
| roc_curve.png | ROC curve with AUC score |
| multiclass_confusion_matrix.png | Confusion matrix for multi-class classification |

---

*Report generated from EDA analysis on Student Exam Performance Dataset*
