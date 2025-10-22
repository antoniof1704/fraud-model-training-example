# Fraud Model Development Template

### Background

This model development script was originally created for a fraud detection project. Due to the sensitive nature of that work, parts of the code and input dataset have been modified. The current version uses the Kaggle credit card fraud dataset, and the script has been optimised for F1 score (whereas the original project focused on Recall). Additionally, the Kaggle dataset has been reduced in size to address runtime constraints.

### Setup

If you want to strip the notebook outputs when pushing to Git, use the following command:

```bash
pip install nbstripout
nbstripout --install
```

This ensures notebook outputs are stripped before pushing to Git, preventing potential security incidents.

If you are unsure as to whether it is installed or not in your git repo, run the following in the terminal:

```
nbstripout --status
```

If it is not installed, it will return:

```
nbstripout is NOT installed in Git repository
```


### Process Overview
Open *main_script.ipynb* and update the following parameters in the **Load in Input Dataset** section:

 * training_file: Training dataset to use (example Kaggle credit card fraud dataset)
 * target_flag: Set to target variable in dataset. 

Once these have been updated, click 'Run All'. The notebook reads in the training data, evaluates models, and saves the best-performing one (based on F1 score - metric can be changed) as a .pkl file.

* **Library Imports**: Loads required libraries.
* **Load Input Data**: Update the parameters as instucted above.
* **Model Evaluation Function**:
    * Accepts following arguments:
        * Input dataset
        * Target variable
        * List of columns to drop (e.g., highly correlated or irrelevant features)
        * Overide best model to save/return (specify the model you want to return/save, even if its not the best performing)
        * Option to return best parameters for each model from tuning (default is False, but set to True when function called).
    * Removes non-numeric columns.
    * Generates correlation heatmap.
    * Splits data into train/test sets.
    * Trains five models: Logistic Regression, Random Forest, Gradient Boosting, SVM, KNN.
    * Performs parameter tuning for each model type and returns the best-performing tuned model for each.
    * Applies SMOTE and scaling where needed.
    * Outputs F1 score, classification report, feature importance, and confusion matrix.
    * Returns best model, F1 score, feature list and scaler (if used) - or the model type specified in the model overide.
* **Save Best Model**:
    * Saves model to ~/MODEL_WEIGHTS/YYMMDD_best_model_USERNAME/ as model_type_F1_score.pkl.
    * Saves a .txt file containing metadata and parameters used for the model.

### Future Improvements

* Add an additional parameter to the evaluation function that allows you to choose the optimisation metric (Accuracy, Precision, Recall, or F1 score). Currently, this must be changed manually within the code.
