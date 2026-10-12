# Machine Learning-Based Metabolic Cost Prediction

##  Overview

This project uses machine learning regression algorithms to predict metabolic cost during human walking using biomechanical measurements and walking-condition data.

The objective is to compare different regression models, evaluate their predictive performance, and identify which combination of input features and model provides the lowest prediction error.

The project also includes exploratory data analysis, visualizations, and feature-importance analysis to help understand the dataset and model predictions.

## Objectives

- Predict metabolic cost from walking-related measurements.
- Compare five regression models.
- Investigate the effect of different feature groups on prediction performance.
- Evaluate models using Leave-One-Subject-Out Cross-Validation.
- Analyse prediction errors using regression metrics.
- Visualize actual versus predicted values and feature importance.

##  Machine Learning Models

The project evaluates the following five models:

| Model | Description |
|---|---|
| Dummy Mean Regressor | Provides a baseline by predicting the mean target value from the training data. |
| Ridge Regression | Learns linear relationships with regularization to control model complexity. |
| Support Vector Regression (SVR) | Uses an RBF kernel to model nonlinear relationships. |
| Random Forest Regressor | Combines predictions from multiple decision trees. |
| Gradient Boosting Regressor | Builds trees sequentially to improve predictions by correcting errors. |

##  Dataset

The project uses a prepared CSV dataset containing walking-related measurements and metabolic-cost values.

**Target variable:** `metabolic_cost_J_kg_m`

The target represents metabolic cost in joules per kilogram per metre walked (J/kg/m).

### Feature groups

The notebook evaluates four feature groups:

1. **Context:** Walking conditions such as speed, incline, and trial duration.
2. **Kinematics + GRF:** Context features combined with joint angles, velocities, moments, and ground reaction forces.
3. **EMG:** Context features combined with muscle-activation measurements.
4. **All:** Context, kinematics, ground reaction forces, and muscle-activation features.

The exact features included depend on the columns available in the prepared dataset.

##  Methodology

The project follows these steps:

1. **Data loading:** Load the prepared CSV file using Pandas.
2. **Data inspection:** Examine columns, dataset dimensions, missing values, and subject information.
3. **Data cleaning:** Remove rows with missing target values and remove verified duplicate left/right measurement columns.
4. **Feature selection:** Construct the four feature groups.
5. **Preprocessing:** Impute missing input values using training-set medians and standardize features where required.
6. **Model training:** Train the five regression models using the selected feature groups.
7. **Cross-validation:** Evaluate predictions using Leave-One-Subject-Out Cross-Validation.
8. **Evaluation:** Calculate MSE, RMSE, MAE, and R².
9. **Model comparison:** Select the non-baseline model–feature configuration with the lowest RMSE.
10. **Visualization:** Generate plots for model comparison, target distribution, correlation, actual versus predicted values, and feature importance.
11. **Export:** Save evaluation tables, predictions, and feature-importance results.

##  Evaluation Strategy

### Leave-One-Subject-Out Cross-Validation (LOSO-CV)

The project uses subject-wise cross-validation to evaluate generalization to unseen subjects.

In each fold:
- All trials belonging to one subject are held out for testing.
- Trials from the remaining subjects are used for training.
- The trained model predicts metabolic cost for the held-out subject.
- The process repeats until each subject has been held out once.

This reduces the risk of overly optimistic evaluation caused by placing trials from the same subject in both training and testing sets.

### Evaluation metrics

| Metric | Meaning | Preferred value |
|---|---|---|
| MSE | Mean Squared Error; average squared prediction error | Lower |
| RMSE | Root Mean Squared Error; error expressed in the target's units | Lower |
| MAE | Mean Absolute Error; average absolute prediction error | Lower |
| R² | Coefficient of determination; compares squared prediction error with a mean-prediction baseline | Higher |

RMSE is the primary metric used to select the best non-baseline configuration.

**Note:** R² is not classification accuracy. It can be negative when a model performs worse than the mean-prediction baseline.

##  Visualizations

The notebook generates the following visualizations:

- **Model Comparison:** Compares the best RMSE achieved by each machine learning model across feature groups.
- **Target Distribution:** Shows the distribution of metabolic-cost values.
- **Correlation Heatmap:** Illustrates linear correlations between numerical variables.
- **Actual vs Predicted Plot:** Compares measured metabolic cost with model predictions. Points closer to the diagonal indicate more accurate predictions.
- **Feature Importance:** Shows the features most heavily used by the fitted Gradient Boosting model according to its feature-importance scores.

These visualizations support model comparison and exploratory analysis.

##  Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- SciPy
- Google Colab / Jupyter Notebook

##  Getting Started

### Prerequisites

- Python 3.10 or a compatible Python environment
- The prepared CSV dataset
- Jupyter Notebook or Google Colab

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
cd YOUR_REPOSITORY
```

Replace the placeholders with your GitHub username and repository name.

### 2. Install dependencies

```bash
pip install numpy pandas matplotlib seaborn scikit-learn scipy
```

### 3. Prepare the dataset

Ensure that your prepared CSV file is available.

Expected filename:

```text
metabolic_cost_ml_dataset.csv
```

The dataset must contain the target column `metabolic_cost_J_kg_m`, the subject identifier column `subject`, and the measurement columns required by the notebook.

### 4. Run the notebook

Open `Metabolic_Cost_ML_Corrected(1).ipynb` in Google Colab or Jupyter Notebook.

In Google Colab:

1. Upload the notebook.
2. Run the cells in order.
3. Upload the prepared CSV file when prompted.
4. Wait for preprocessing, cross-validation, model comparison, and plotting to finish.
5. Download the generated results archive when prompted.

##  Expected Project Structure

```text
metabolic-cost-ml/
│
├── README.md
├── Metabolic_Cost_ML_Corrected(1).ipynb
├── metabolic_cost_ml_dataset.csv
│
└── metabolic_cost_results/
    ├── cleaned_dataset.csv
    ├── model_comparison.csv
    ├── cross_validated_predictions.csv
    └── feature_importance.csv
```

The results directory and CSV files are generated when the notebook runs successfully. They do not need to exist before execution.

## Output Files

| File | Purpose |
|---|---|
| `cleaned_dataset.csv` | Contains the cleaned dataset used by the notebook. |
| `model_comparison.csv` | Stores evaluation metrics for model–feature configurations. |
| `cross_validated_predictions.csv` | Stores actual and predicted values from cross-validation. |
| `feature_importance.csv` | Stores feature-importance scores from Gradient Boosting. |

##  Model Selection

The notebook compares all tested model–feature configurations and sorts them by RMSE.

The best non-baseline configuration is the one with the lowest RMSE among the tested machine learning models.

Actual performance values should be reported from the completed notebook execution rather than assumed in advance.

##  Limitations

- Model performance depends on the dataset and the subjects represented.
- Fixed hyperparameters may not provide the best possible performance.
- Selecting a model using the same cross-validation results used for comparison can introduce selection bias.
- An independent subject-level test set or nested cross-validation would provide stronger evidence of generalization.
- Feature importance and correlation do not establish causation.

##  Future Improvements

- Tune hyperparameters using nested cross-validation.
- Evaluate the final model on an independent group of subjects.
- Compare additional regression algorithms.
- Analyse prediction errors across walking conditions and subjects.
- Investigate model interpretation methods such as permutation importance and SHAP.
- Develop a simple interface for entering walking measurements and obtaining predictions.

##  Applications

Potential applications include:
- Biomechanical data analysis.
- Human walking and movement research.
- Predictive modelling of metabolic cost.
- Comparative evaluation of machine learning regression algorithms.

These are potential applications; the project does not by itself establish clinical validity.

##  License

Choose an appropriate open-source license before distributing this project. Ensure that the dataset's license permits redistribution before uploading the dataset to a public repository.

## Acknowledgements

This project uses open-source Python libraries, including Pandas, NumPy, Matplotlib, Seaborn, SciPy, and Scikit-learn.

