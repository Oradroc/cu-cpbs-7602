# Ensemble Based Modeling on Gene Data

## Methodologic Error Notice

I applied normalization prior to the splits which creates data leakage. The correct method would be to normalize each to itself. I do not have time to rerun everything, so this disclaimer will need to suffice

## Repository Organization

This repository is organized into two assignments.

## Assignment 01 Clustering and Data Preparation

**Location:** `assignment01/`

### `DataCleaning.ipynb`

This notebook

1. Loads the GTEx gene TPM expression matrix and `Meta.txt`
2. Identifies the top tissues in the metadata and the top variable genes in GTEx
3. Produces a cleaned expression matrix and aligned labels
4. Writes cleaned data to disk for use in clustering and later modeling tasks

## Environment

A `requirements.txt` file is included with required dependencies

Create conda virtual environment

conda create -n gene-Pred python=3.11
conda activate gene-Pred
pip install -r requirements.txt
**Important prerequisite for Assignment 03**

Before running anything in `assignment03/`, open `assignment01/DataCleaning.ipynb` and ensure that the cells that write the cleaned data to file are enabled so downstream notebooks can load the processed data.

## Assignment 03 Ensemble Based Models

**Location:** `assignment03/`

### `EnsembleGeneExpression_Tissue.ipynb`

This notebook

1. Loads the cleaned and subsetted dataset (ClusterDataset.csv) written by `assignment01/DataCleaning.ipynb`
2. Performs dimensionality reduction and visualizes samples using PCA plots
3. Tests clustering in PCA space using Agglomerative Clustering across multiple component counts
4. Evaluates clustering performance across component settings using NMI and selects the best clustering based on NMI
5. Builds supervised models to predict tissue of origin for the top 10 tissues using projected features
6. Compares ensemble classifiers including `RandomForestClassifier` and `AdaBoostClassifier` with decision tree base estimators
7. Includes a `DummyClassifier` baseline for comparison
8. Uses stratified train test splits to keep class frequency similar across train and test
9. Does not explicitly adjust for class imbalance
10. Evaluates generalization on held out test data using `classification_report` and confusion matrices

### `EnsembleGeneExpression_AGE.ipynb`

This notebook

1. Loads the cleaned and subsetted dataset (ClusterDataset.csv) written by `assignment01/DataCleaning.ipynb`
2. Prepares a continuous age target by converting age bins into a numeric value using the midpoint of each bin
3. Trains and compares regression models to predict age from gene expression features
4. Uses `DummyRegressor` with mean prediction as a baseline
5. Compares `RandomForestRegressor` and `AdaBoostRegressor` with `DecisionTreeRegressor` base estimators
6. Performs parameter search over a similar space as the tissue classifier models
7. Evaluates models on held out test data using MAE, RMSE, and R2

## Reproducibility

Random seeds are set in notebooks where appropriate to improve reproducibility of data splits, sampling, and model initialization.



