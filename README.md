# Summer_prac
The repository with my summer practice in machine learning. Work was carried out with data from the cardiology center.
Data: https://docs.google.com/spreadsheets/d/1RBeg3MbIcY3qDUxdceGVDfBQzDC39HGc/edit?usp=sharing&ouid=110453465962436740825&rtpof=true&sd=true

The aim of the project was to reduce the dimension and build an interpretable model predicting the outcome of coronary angiography of patients (degree of stenosis). The work was performed on the basis of a medical dataset containing more than 150 signs, including clinical, laboratory and angiographic parameters.

The task is divided into 5 sub-tasks: 

1)Predicting the result of coronary angiography: take signs from the following graphs — from J to BJ and from CI to GJ (of these, indicators from graphs from CZ to GJ are especially needed).

2)Classification of patients into 4 classes (multiclass classification) according to all criteria (column CH).

3.1)Predicting the patient's entry into group 3 (column CH) according to clinical data — graphs G-K, O-AD, AL-AR, AX-BJ, CJ, CK.

3.2)Prediction of the patient's entry into group 3 (column CH) according to the stress echocardiography graph CR-GJ.

4)Prediction of a bad prognosis is the value of 1 in the MH graph according to the stress echocardiography graph CR-GJ.

The project is implemented in Google Colab and published as Jupyter Notebook.

The main stages of work
1. Import and primary data processing
Download of an Excel file with medical data.
Removing irrelevant and duplicate features.
Categorical feature processing (OrdinalEncoder, string value conversion).
Removing features with omissions of more than 50%.

2. Processing of missing values (imputation)
To improve the quality of the subsequent analysis, various methods of filling in gaps were used.:
SimpleImputer (by median),
KNNImputer,
IterativeImputer (MICE),
missForest (based on RandomForestRegressor).
Each method was used with subsequent verification of the quality of the models on the relevant data.

3. Dimension reduction 
3.1. PCA (Principal Component Method)
The PCA method is used to estimate the proportion of explained variance.
The features that most strongly influence the first components have been selected.

3.2. Methods of feature selection
Several approaches have been tested:
RFE (Recursive Feature Elimination) — based on the randomForest and XGBoost models.
RFECV is an automatic selection of the number of features with cross-validation.
ANOVA (f_classif) is an assessment of the statistical relationship of features with the target variable.
LassoCV is regularization with automatic alpha selection.
Plot feature importance of the CatBoost and XGBoost models.
The intersection of features selected by different methods was also performed.

4. Building models
The CatBoostClassifier model is designed to work with categorical features without coding.
The XGBoost model is trained on the final signs (after selection).
Checking quality metrics: accuracy, recall, confusion matrix.
Construction of a correlation matrix between selected features to identify multicollinearity.
Pipeline and GridSearchCV were used for cross-validation configuration.

5. Final result
As a result of the work:
The dimension has been reduced from ~160 to 6-10 features.
Features directly related to the target variable are excluded to avoid leakage.
High classification accuracy was achieved (accuracy ≈ 86%, recall ≈ 94%).
The interpretation of the results was carried out taking into account medical logic.
The possibility of using the model as a calculator for doctors (set of values → prognosis) is proposed.

Used libraries
pandas, numpy, matplotlib, seaborn

scikit-learn

xgboost, catboost

fancyimpute, missingpy (MissForest)

optuna (hyperparametric optimization is optional)

scipy
