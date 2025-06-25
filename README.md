# motor-adaptation-ml
# Motor Adaptation Predictive Model  
**Explaining neural mechanisms of motor adaptation using EEG and machine learning**  

## 📌 Overview  
This repository contains code to **predict motor adaptation** from EEG signals, using the [PhysioNet EEG Motor Movement/Imagery Dataset](https://physionet.org/content/eegmmidb/). Key components:  
- **Preprocessing**: Filtering, epoching, and artifact removal for 64-channel EEG.  
- **Feature Extraction**: Mu/beta power (8–30 Hz) in sensorimotor cortex (C3/C4).  
- **Interpretable ML**: RandomForest + SHAP to link EEG features to behavior.  

**Hypothesis**: Sensorimotor rhythms (mu, 8–12 Hz) predict trial-to-trial motor errors during adaptation.  

---

## 🛠️ Installation  

bash
pip install -r requirements.txt
Download PhysioNet data (first 3 subjects):

bash
wget -r -np -nH --cut-dirs=5 -A edf https://physionet.org/files/eegmmidb/1.0.0/S00{1..3}/
🚀 Usage
Run the pipeline end-to-end:

1. Preprocess EEG Data
bash
python scripts/preprocess.py --subject S001 --run R01
Output: processed/S001_epochs.fif (MNE epochs).

2. Extract Features
bash
python scripts/extract_features.py --bands mu beta
Output: processed/features.csv (mu/beta power + reaction time).

3. Train and Interpret Model
bash
python scripts/train_model.py --target task --explainer shap
Outputs:

models/rf_model.pkl (trained RandomForest).

results/shap_summary.png (feature importance).

📂 Directory Structure
markdown
motor-adaptation-ml/
├── data/                   # Raw PhysioNet EDF files (S001-S003)
├── processed/              # Processed data
│   ├── S001_epochs.fif     # Epochs for Subject 1
│   └── features.csv        # Extracted features
├── scripts/                # Modular Python scripts
│   ├── preprocess.py       # EEG preprocessing
│   ├── extract_features.py # Time-frequency analysis
│   └── train_model.py      # ML training + SHAP
├── notebooks/              # Exploratory analysis
│   ├── 1_Data_Exploration.ipynb
│   └── 2_Model_Validation.ipynb
├── models/                 # Saved models
├── requirements.txt        # Python dependencies
└── README.md


