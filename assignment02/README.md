# Linear and Logistic Modeling on Gene Data

The repository is organized into two assignments.

## Assignment 01  Clustering and Data Preparation

Located in `assignment01/`.

### `DataCleaning.ipynb`

This notebook  

* Loads the GTEx Gene TPMs expression matrix and `Meta.txt`  
* Identifies the top tissues in the metadata and the top variable genes in GTEx  
* Produces a cleaned expression matrix and aligned labels  
* Writes cleaned data to disk for use in both clustering and later modeling tasks  

Before running other notebooks or `assignment02`  

* Open `assignment01/DataCleaning.ipynb` and ensure that the cells that write the cleaned data to file are active so that downstream notebooks can load the processed data.  

## Assignment 02  Linear and Logistic Modeling

Located in `assignment02/`.

### `LinearAndLogisticModeling.ipynb`

This notebook  

* Loads the cleaned and subsetted dataset written by `assignment01/DataCleaning.ipynb`  
* Performs multiple linear regression to study how gene expression relates to tissue type, adjusting for covariates such as age and sex  
* Performs logistic regression where appropriate, for example predicting tissue type from expression features  
* Summarizes and interprets model coefficients, p values, and effect sizes for selected genes  

**Important**  You must run `assignment01/DataCleaning.ipynb` with the write to disk cells enabled before running `assignment02/LinearAndLogisticModeling.ipynb`, so that the modeling notebook can load the processed data.

## Reproducibility

Random seeds (for example `np.random.seed(0)`) are set in the notebooks where appropriate to improve reproducibility of sampling and initialization steps.


## Use of AI disclosure

README file was drafted using chatGPT by describing all steps of the process
requirements.txt file was created with chatGPT by pasting libraries into chatGPT 
General debugging. 

