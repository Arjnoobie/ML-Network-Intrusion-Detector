# ML Network Intrusion Detector

**IBM SkillsBuild Cyber Security 2026 (BharatCares) – Capstone Project**
**Author:** Arjun Pundir

## Project Description
A machine-learning intrusion detection system built with Scikit-learn. It classifies network connection records as **normal** or **attack**, and also identifies the attack family (**DoS, Probe, R2L, U2R**). Three models (Logistic Regression, Decision Tree, Random Forest) are trained on the NSL-KDD training set and evaluated on a separate test set that contains attack types not seen during training, giving a realistic view of how well the detector generalises.

## Dataset
**NSL-KDD** (improved version of KDD'99, duplicate records removed)
- Official page: https://www.unb.ca/cic/datasets/nsl.html
- Mirror used by the notebook (downloaded automatically): https://github.com/defcom17/NSL_KDD
- Files: `KDDTrain+.txt` (125,973 records) and `KDDTest+.txt` (22,544 records), 41 features each.

## Technologies Used
Python 3 · Jupyter Notebook · Scikit-learn · Pandas · NumPy · Matplotlib · Seaborn · Joblib

## Project Structure
| File | Purpose |
|---|---|
| `ArjunPundir_NetworkIntrusionDetector.ipynb` | Complete code: EDA, preprocessing, training, evaluation |
| `requirements.txt` | Python dependencies |
| `ArjunPundir_ProjectReport.docx` | Full project documentation |
| `README.md` | This file |

## Setup and Run
```bash
# 1. (Optional) create a virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 2. Install dependencies
pip install -r requirements.txt

# 3. Launch the notebook
jupyter notebook ArjunPundir_NetworkIntrusionDetector.ipynb
```
Run all cells (**Kernel → Restart & Run All**). An internet connection is needed on the first run so the notebook can download the dataset; it is then cached as `train.csv` and `test.csv`. Total runtime is a few minutes. The trained pipeline is saved as `intrusion_detector_model.joblib`.

## Key Results (on KDDTest+)
| Model | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|
| Logistic Regression | 0.7537 | 0.9174 | 0.6234 | 0.7424 |
| **Decision Tree** | **0.7831** | 0.9583 | 0.6471 | **0.7725** |
| Random Forest | 0.7677 | 0.9676 | 0.6123 | 0.7500 |

## Key Information
- High precision (92–97%) but modest recall (61–65%): about one in three attacks is missed.
- Models score F1 > 0.97 in cross-validation on the training file but about 0.74–0.77 on the test file, showing that unseen attack variants are the main challenge.
- DoS and Probe attacks are detected well; R2L and U2R are rarely caught because of very few training samples.
- NSL-KDD is dated; results should not be taken as production performance.

## Future Work
Class balancing (SMOTE), threshold tuning for higher recall, gradient boosting, and retraining on modern datasets such as CIC-IDS2017.
