# Predicting Mortality in Primary Biliary Cholangitis (PBC) with Machine Learning

Final project of the Postgraduate Degree in Data Science in Biotechnology (School of Biotechnology, Catholic University of Portugal) — 19/20.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/inesalexsilvajorge/Machine-Learning-Models-to-predict-Primary-Biliary-Cholangitis/blob/main/Modelo_machine_learning_para_previsao_de_mortalidade_por_CBP.ipynb)

## 🎯 Objective

Develop and compare classification models capable of predicting mortality risk in patients with Primary Biliary Cholangitis (PBC), a rare chronic liver disease, based on clinical and laboratory data collected during patient follow-up.

## 📊 Dataset

- **Source:** Primary Biliary Cirrhosis (PBC) Dataset, Mayo Clinic — publicly available on the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/878/primary+biliary+cirrhosis). *(The data file is not included in this repository; it should be downloaded directly from the source.)*
- **Size:** 418 patients, 20 variables (age, sex, bilirubin, cholesterol, albumin, copper, alkaline phosphatase, platelets, prothrombin, disease staging, among others).
- **Original target variable:** patient status at the end of the study — `C` (censored/alive), `CL` (censored due to liver transplant) or `D` (death).
- **Approach used in this project:** binary classification of death vs. non-death, excluding cases censored due to liver transplant ("Approach A, without CL").

## 🔧 Methodology

1. **Preprocessing:** conversion of age from days to years, analysis and handling of missing values, encoding of categorical variables with One-Hot Encoding.
2. **Train/test split:** 212 patients for training, 54 for testing.
3. **Normalization:** standardization of numerical variables (StandardScaler).
4. **Feature selection:** comparison of three scenarios — full feature set (17 features) vs. two feature-reduction thresholds (0.2 and 0.3) — to assess whether reducing dimensionality improved model performance.
5. **Models tested:** Decision Trees, K-Nearest Neighbors, Naive Bayes, Linear/Quadratic Discriminant Analysis, Logistic Regression (with and without automatic regularization via CV), SVM (linear and non-linear), SGD, and ensemble models — Bagging, Extra Trees, Random Forest and **AdaBoost** — as well as Neural Networks (MLP).
6. **Hyperparameter optimization:** GridSearchCV applied to the three best-performing models, across each of the three feature scenarios, with cross-validation.
7. **Final evaluation:** training of the winning model with the best hyperparameters found, followed by bootstrap validation to obtain robust confidence intervals.

## 🏆 Result

The final selected model was an **AdaBoost Classifier** (`n_estimators=50`, `learning_rate=0.5`), trained on the full set of 17 features:

| Metric | Value |
|---|---|
| AUC-ROC | **0.907** |
| C-index (concordance index) | **0.907** |
| Number of features | 17 |
| N (train) | 212 |
| N (test) | 54 |

The confidence interval for the C-index was calculated via bootstrap (1,000 iterations), confirming the robustness of the result. An AUC-ROC of 0.907 indicates excellent discriminative ability of the model between patients at higher and lower risk of mortality. The five most important predictors were ascites, copper, bilirubin, prothrombin time, and age, together explaining 80.9% of the model's discriminative capacity.

## 🛠️ Technologies

Python · Pandas · NumPy · Scikit-learn · Matplotlib · Seaborn · Lifelines (for C-index calculation)

## 📁 Structure

- `Modelo_machine_learning_para_previsao_de_mortalidade_por_CBP.ipynb` — full notebook covering the entire pipeline, from preprocessing to final evaluation.

## ✍️ Author

**Inês Jorge** — [LinkedIn](#) · [email](mailto:ines.silva.jorge@gmail.com)
