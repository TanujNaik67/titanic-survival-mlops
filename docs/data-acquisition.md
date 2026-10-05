# Titanic Dataset Acquisition

## 1. Dataset Source

- **Provider:** Kaggle
- **Competition:** Titanic - Machine Learning from Disaster
- **Source URL:** https://www.kaggle.com/competitions/titanic/data
- **Acquisition date:** 2026-10-04
- **Acquisition method:** Manual download from the Kaggle competition page
- **License:** Subject to Kaggle competition rules

## 2. Downloaded Files

| File | Purpose | Rows | Columns |
|---|---|---:|---:|
| `train.csv` | Model training data containing the target | 891 | 12 |
| `test.csv` | Unseen passenger data requiring predictions | 418 | 11 |
| `gender_submission.csv` | Example Kaggle submission format | 418 | 2 |
| `titanic.zip` | Original downloaded source archive | Not applicable | Not applicable |

## 3. Target Availability

- `train.csv` contains the target column `Survived`.
- `test.csv` does not contain `Survived`.
- The trained model will predict `Survived` for every passenger in `test.csv`.

## 4. Storage Policy

The downloaded files are stored locally under:

```text
data/raw/
```

Raw data must remain unchanged. Any cleaning, transformation, or feature-engineering output will be stored separately under:

```text
data/processed/
```

The raw files are excluded from Git through `.gitignore`. This prevents downloaded datasets and archives from being committed to GitHub.

## 5. Reproduction Steps

1. Visit the Kaggle Titanic competition page.
2. Join the competition and accept its rules.
3. Open the Data tab.
4. Download the dataset as a ZIP archive.
5. Copy `titanic.zip` into `data/raw/`.
6. Extract the archive inside `data/raw/`.
7. Validate the files using pandas.

## 6. Initial Validation Results

- Training dataset shape: `(891, 12)`
- Test dataset shape: `(418, 11)`
- Sample-submission shape: `(418, 2)`
- `Survived` exists in the training dataset.
- `Survived` does not exist in the test dataset.
