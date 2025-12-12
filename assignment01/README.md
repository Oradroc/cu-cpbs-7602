# Gene Expression Clustering

This repository contains notebooks for cleaning GTEx bulk tissue expression data and performing clustering analysis to see whether samples group by tissue of origin.

## Data

The raw expression matrix is **not** included in this repository because of its size. The only data file tracked here is the metadata file `Meta.txt`. You will need to download the expression matrix yourself.

1. Go to the GTEx Portal bulk tissue expression downloads page:  
   https://gtexportal.org/home/downloads/adult-gtex/bulk_tissue_expression

2. Under **Downloads → Open Access Data → Bulk Tissue Expression**, select **GTEx Analysis v8**.

3. Download the **“Gene TPMs”** file.

4. Place the downloaded “Gene TPMs” file in the same data location expected by the notebooks (for example a `data/` folder alongside `Meta.txt`), and make sure the file path used in `DataCleaning.ipynb` matches where you saved it.

   A simple layout might be:
   - `data/Meta.txt`  
   - `data/<GTEx_Analysis_20170605_v8_RNASeQCv1.1.9_gene_tpm.gct>` (or similar)

Adjust the exact paths in the notebooks if your filenames differ, but keep them relative to the repository (no absolute machine-specific paths).

## Environment

A `requirements.txt` file is included with required dependencies

Create conda virtual environment

conda create -n gene-cluster python=3.11
conda activate gene-cluster
pip install -r requirements.txt

## Workflow

Run the notebooks in this order:

1. `DataCleaning.ipynb`  

   This notebook:

   * Loads the GTEx “Gene TPMs” expression matrix and `Meta.txt`  
   * Finds the top ten tissues in meta and top 5k genes in GTEx
   * Produces a cleaned expression matrix and aligned labels  
   * Optionally writes cleaned data to disk  

   **Before running:**  
   - Open the notebook and **uncomment the lines that write the cleaned data to file**, so downstream notebooks can load the processed data.

2. `ClusterAssignment.ipynb`  

   This notebook:

   * Loads the cleaned data produced by `DataCleaning.ipynb`  
   * Performs clustering using methods such as KMeans and AgglomerativeClustering (with PCA reduction)
   * Computes internal metrics such as silhouette and Davies–Bouldin scores  
   * Computes external metrics such as Adjusted Rand Index (ARI) and Normalized Mutual Information (NMI) against tissue labels  

3. `ImportantGenes.ipynb`  

   This notebook:

   * Uses the clustering results and tissue labels  
   * Identifies genes that drive the clustering structure (e.g., via one-way ANOVA across clusters)  
   * Identifies important genes for each tissue separately (e.g., one-vs-rest analyses)  
   * Summarizes and visualizes the top genes per cluster and per tissue

Make sure you run all cells in `DataCleaning.ipynb` (with write lines uncommented) before running `ClusterAssignment.ipynb` and `ImportantGenes.ipynb`.

## Reproducibility

np.random.seed is set to 42, for cluster stability on kmeans random state is fixed

## Use of AI disclosure

All LaTeX tables were created using chatGPT
README file was drafted using chatGPT by describing all steps of the process
requirements.txt file was created with chatGPT by pasting libraries into chatGPT 
Conda environment was tested based on the requirements file generated.
General debugging. 
