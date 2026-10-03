# Titanic Survival Prediction: Problem Definition

## 1. Problem Statement

The goal is to build a supervised machine learning model that predicts whether a passenger survived the Titanic disaster using passenger information available before the survival outcome is known.

For each passenger, the model will predict:

- `1`: Survived
- `0`: Did not survive

This is a **supervised binary classification** problem because the training data contains known outcomes and the target variable has two possible classes.

## 2. Unit of Prediction

Each row represents one passenger, and the model produces one survival prediction for that passenger.

## 3. Target and Candidate Features

### Target

- Column: `Survived`
- Meaning: Whether the passenger survived
- Values: `1` means survived; `0` means did not survive

### Candidate Features

The initial candidate features are passenger attributes such as ticket class, sex, age, family relationships, fare, ticket information, cabin information, and port of embarkation.

Their usefulness, missing values, required transformations, and potential leakage risks will be evaluated during exploratory data analysis.

`PassengerId` is an identifier rather than a meaningful passenger characteristic, so it will not be used as a predictive feature by default.
