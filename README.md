# Breast Cancer Prediction (Streamlit App)

An interactive Streamlit application that predicts whether a breast mass is benign or malignant using a Logistic Regression model trained on the Wisconsin Breast Cancer dataset. The app visualizes user‑provided cell nuclei measurements with a radar chart and returns the predicted class along with class probabilities.


## Key Features
- Streamlit UI with sliders for 30 standard breast‑cancer features
- Interactive radar chart (Plotly) for mean, standard error, and worst values
- Logistic Regression model with StandardScaler preprocessing
- Clear probabilities for Benign vs. Malignant predictions


## Quick Start

Prerequisites:
- Python 3.9+ (3.10/3.11 also typically fine)
- pip

Install dependencies (from the project root):

```bash
pip install -r requirements.txt
```

Run the Streamlit app:

```bash
streamlit run Streamlit_app/app.py
```

Then open the URL printed in the terminal (usually http://localhost:8501).


## Repository Structure

```
Breast_Cancer_Prediction/
├─ Streamlit_app/
│  └─ app.py                    # Streamlit UI, radar chart, prediction logic
├─ data/
│  └─ data.csv                  # Wisconsin Breast Cancer dataset (includes id)
├─ models/
│  ├─ model.pkl                 # Trained Logistic Regression model (generated)
│  └─ scaler.pkl                # Fitted StandardScaler (generated)
├─ logistic_regression_model.ipynb  # Training & evaluation notebook
├─ requirements.txt
└─ README.md
```


## Data

- Source: Wisconsin Breast Cancer dataset (commonly used in ML demos).
- The provided CSV (data/data.csv) includes the following:
  - An `id` column
  - `diagnosis` label: `M` (malignant) or `B` (benign)
  - 30 feature columns grouped as mean, se, and worst metrics
  - An extraneous column `Unnamed: 32` that is dropped during preprocessing


## Model Training and Re‑generating Artifacts

Training steps are captured in `logistic_regression_model.ipynb`.

High‑level flow in the notebook:
1. Load data from `data/data.csv`.
2. Drop `Unnamed: 32`.
3. Map labels: `{'M': 1, 'B': 0}` to create a binary target variable.
4. IMPORTANT: Keep `id` in the feature matrix `X` so the scaler is fit on 31 columns (id + 30 features).
5. Fit `StandardScaler` on `X` and split into train/test.
6. Train `LogisticRegression` on the scaled training set.
7. Evaluate and save artifacts to `models/model.pkl` and `models/scaler.pkl`.


## Using the App

1. Start the app: `streamlit run Streamlit_app/app.py`.
2. Adjust the sliders in the sidebar. Each slider is initialized from the dataset’s min/mean/max for that feature.
3. The main panel shows a radar chart for mean/se/worst groups.
4. The right panel displays the predicted class and probabilities.
5. Important: This tool is for educational/demo purposes and should not replace professional medical diagnosis.


## Development Notes

- Streamlit app key modules: `Streamlit_app/app.py`
- Core libraries: pandas, numpy, scikit‑learn, streamlit, plotly
- The app internally scales inputs using the saved `StandardScaler` and then predicts via the saved model.



## Author 
Eya Bargouth