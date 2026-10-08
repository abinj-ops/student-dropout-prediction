# 🎓 Student Dropout Prediction System

A machine learning–based Streamlit web application that predicts whether a student is at risk of dropping out using academic, personal, financial, attendance, and lifestyle-related attributes.

The project combines a trained **Random Forest Classifier** with **StandardScaler** preprocessing and **SelectKBest** feature selection, and provides a multi-page interface for prediction, dataset overview, student information, model performance, and project details.

## 📌 Project Objective

The main objective is to identify students who may be at risk of dropping out at an early stage so that educational institutions can take appropriate preventive measures.

## ✨ Features

- 🔮 **Dropout Prediction** – Enter student details and obtain a dropout-risk prediction.
- 📊 **Student & Dataset Dashboard** – View dataset size and dropout/non-dropout distribution.
- 👤 **Student Profile** – Understand the academic, personal, and lifestyle attributes used by the model.
- 📈 **Model Performance** – View the final model metrics and class-wise classification report.
- ℹ️ **About Project** – Overview of the objective, technology stack, and machine learning workflow.
- 📊 **Prediction Probability** – Displays dropout and non-dropout probabilities along with the decision threshold.
- 🌲 **Random Forest Model** – Final classifier used for prediction.

## 🧠 Machine Learning Workflow

The application describes the following workflow:

**Data Collection → Data Preprocessing → Exploratory Data Analysis → Feature Engineering → Train-Test Split → Feature Selection → Model Training → Hyperparameter Tuning → Model Evaluation → Prediction**

For deployment, the saved model object contains:

**StandardScaler → SelectKBest → Random Forest**

The deployed model uses **27 input features**, selects the **best 10 features**, and then generates the dropout probability.

## 📋 Input Features

The prediction interface uses the following 27 features:

### Numerical Features

- Age
- Family Income
- Daily Study Hours
- Attendance Rate
- Assignment Delay Days
- Travel Time (Minutes)
- Stress Index
- GPA
- Semester GPA
- CGPA
- Total Daily Commitment (Minutes)

### Categorical / Encoded Features

- Gender
- Internet Access
- Part-Time Job
- Scholarship
- Semester Year
- Department
- Parental Education
- Performance Category

Categorical values are converted into the encoded feature columns expected by the trained model.

## 🎯 Prediction Process

When a user clicks **Predict Dropout**, the application:

1. Collects the student's input values.
2. Converts categorical selections into the model's encoded feature columns.
3. Arranges the 27 features in the exact order stored with the deployed model.
4. Applies the saved `StandardScaler`.
5. Applies the saved `SelectKBest` feature selector.
6. Uses the saved `RandomForestClassifier` to calculate dropout probability.
7. Compares the dropout probability with the saved decision threshold.
8. Displays the final risk prediction and probability chart.

The deployed model uses a decision threshold of **0.30**.

- Probability `>= 0.30` → **High Risk: Student may Drop Out**
- Probability `< 0.30` → **Low Risk: Student is Not Predicted to Drop Out**

## 📊 Dataset Overview

According to the dashboard included in the project:

| Item | Value |
|---|---:|
| Total Students | 10,000 |
| Not Dropout | 7,646 |
| Dropout | 2,354 |
| Dropout Rate | 23.54% |
| Input Features | 27 |
| Target Column | Dropout |
| Target Classes | `0 = Not Dropout`, `1 = Dropout` |

> **Note:** The original dataset file is not included in the uploaded project files used to prepare this README. The figures above are taken from the project's dashboard implementation.

## 📈 Model Performance

The application reports the following final model metrics:

| Metric | Score |
|---|---:|
| Accuracy | 79.95% |
| Precision | 78.00% |
| Recall | 79.95% |
| F1 Score | 77.96% |
| ROC-AUC | 80.20% |

### Class-wise Classification Report

| Class | Precision | Recall | F1 Score | Support |
|---|---:|---:|---:|---:|
| Not Dropout | 0.83 | 0.93 | 0.88 | 1529 |
| Dropout | 0.63 | 0.37 | 0.46 | 471 |

The project notes that the model identifies **Not Dropout** students more effectively, while the **Dropout** class is more difficult to identify, as reflected by its lower recall.

## 🏗️ Project Structure

```text
student-dropout-prediction/
│
├── app.py
├── student_dropout_deployment.pkl
├── requirements.txt
│
├── 1_🏠_Home.py
├── 2_📊_Dashboard.py
├── 3_🔮_Prediction.py
├── 4_👤_Student_Profile.py
├── 5_📈_Model_Performance.py
└── 6_ℹ️_About_Project.py
```

### File Description

| File | Purpose |
|---|---|
| `app.py` | Main Streamlit prediction application. Loads the deployed model and performs end-to-end prediction. |
| `student_dropout_deployment.pkl` | Serialized deployment object containing the scaler, feature selector, Random Forest model, threshold, and feature names. |
| `requirements.txt` | Python dependencies required to run the application. |
| `1_🏠_Home.py` | Home page and project overview. |
| `2_📊_Dashboard.py` | Dataset overview and target distribution dashboard. |
| `3_🔮_Prediction.py` | Multi-page prediction interface. |
| `4_👤_Student_Profile.py` | Explanation of student attributes used by the model. |
| `5_📈_Model_Performance.py` | Model metrics, classification report, and ROC-AUC display. |
| `6_ℹ️_About_Project.py` | Project objective, technologies, workflow, and final model summary. |

## 🛠️ Technologies Used

- **Python**
- **Pandas**
- **NumPy**
- **Scikit-learn**
- **Streamlit**
- **Joblib**
- **Google Colab** (used in the project workflow)

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/<your-repository>.git
cd <your-repository>
```

### 2. Create a virtual environment (recommended)

**Windows:**

```bash
python -m venv venv
venv\Scripts\activate
```

**macOS/Linux:**

```bash
python -m venv venv
source venv/bin/activate
```

### 3. Install the dependencies

```bash
pip install -r requirements.txt
```

The provided `requirements.txt` includes:

```text
streamlit
pandas
numpy
scikit-learn
joblib
```

## ▶️ Run the Application

From the project root directory, run:

```bash
streamlit run app.py
```

Streamlit will open the application in your browser.

For the multipage layout, keep the numbered `.py` page files in the same project structure shown above so that Streamlit can discover the pages.

## 🔮 Using the Prediction Module

1. Open the **Prediction** page.
2. Enter the student's academic information.
3. Enter personal and lifestyle information.
4. Click **Predict Dropout**.
5. Review:
   - Dropout Probability
   - Not Dropout Probability
   - Decision Threshold
   - Final risk classification
   - Probability bar chart

The prediction code uses the same feature names, preprocessing objects, feature-selection object, model, and threshold saved inside `student_dropout_deployment.pkl`.

## 📦 Model Deployment Object

The file `student_dropout_deployment.pkl` stores these components:

```python
{
    "scaler": ...,
    "selector": ...,
    "model": ...,
    "threshold": ...,
    "feature_names": ...
}
```

The deployed classifier is a `RandomForestClassifier`. The saved feature selector is `SelectKBest`, and the scaler is `StandardScaler`.

## ⚠️ Important Notes

- The model file **`student_dropout_deployment.pkl` is required** for prediction.
- Keep the model file in the expected project directory so the application can load it with `joblib.load(...)`.
- Prediction inputs must match the feature names and feature order stored in the deployment object.
- The model output is a **prediction of risk**, not a guarantee that a student will actually drop out.
- The class-wise report shows considerably lower recall for the dropout class than for the non-dropout class. This should be considered when interpreting predictions.

## 🚀 Possible Future Improvements

- Add the original dataset to the repository or provide a documented download/source location.
- Add interactive charts for feature distributions and student clusters.
- Add explainable-AI functionality such as feature importance or SHAP explanations.
- Improve detection of the dropout class by addressing class imbalance and optimizing the decision threshold.
- Add authentication and role-based access for institutional use.
- Store prediction history in a database.
- Add downloadable prediction reports for counselors or administrators.

## 📚 Project Summary

This project demonstrates how a trained machine learning model can be integrated into a user-friendly Streamlit application for student dropout-risk prediction. It covers the complete workflow from preprocessing and feature selection to model training, evaluation, serialization, and deployment.

---

## 👨‍💻 Author

**Student Dropout Prediction System**

Built using Python, Scikit-learn, Streamlit, Pandas, NumPy, and Joblib.

> This project is intended for educational and demonstration purposes. Predictions should be interpreted as decision-support information and not as a definitive assessment of a student's future outcome.
