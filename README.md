# Predicting survival times in glioblastoma patients using gene expression and treatment data

Because of the low survival rate and introduction of new therpies for glioblastoma (GBM), evaluation of large patient data sets is needed to identify genetic factors that interact with standard treatments to increase survival time. The Cancer Genome Atlas (TCGA), which contains genetic and clinical information from over 600 GBM patients, was used to analyze how certain gene signatures and treatments interact with regard to survival. Additionally, the predictive power of genes (and not treatments) was analyzed in a group of patients who were treated with radiation.

## API
Several glioblastoma datasets were collected from The Cancer Genome Atlas Project using the UCSC Xena API. Keys are not required. 

More information can be found here: 
TCGA: https://www.cancer.gov/about-nci/organization/ccg/research/structural-genomics/tcga
xenaPython API: https://ucsc-xena.gitbook.io/projectoverview-of-features/accessing-data-through-python

## Data

The following information was extracted using xenaPython:
1. Gene expression dataset:
(a) Log2 RNA gene expression levels for 12,040 genes that were measured by microarray experiment

These datasets had to be loaded in manually from https://xenabrowser.net/datapages/?cohort=TCGA%20Glioblastoma%20(GBM)&removeHub=https%3A%2F%2Fxena.treehouse.gi.ucsc.edu%3A443 
1. Phenotype dataset: 
(a) Treatment with radiation, specifically patients who received "adjuvant" (after surgery) or "standard" therapy
(b) Treatment with chemotherapy, specifically patients who received "adjuvant" (after surgery) or "standard" therapy
(c) Treatment with combined radiation/ chemotherapy (chemoradiation), specifically patients who received "adjuvant" (after surgery) or "standard" therapy
2. Survival dataset:
(a) Overall survival, the binary classification that denotes the patient's survial status at the time the study concluded
(b) Overall survival time, the number of days that each patient survived

Patients with data in one of these categories were removed, and two groups were created: 
1. All Patients & Treatments -- used to measure the impact of the treatments and their predictive influence on the models
2. Radiation Patients Only -- used to cut out potentially correlated variables and focus only on gene expression in the group that received radiation

## Models
For the classification problem, patients were grouped into low or high survival groups based on the median survival of approximately 15 months. High/low survival was predicted. For the regression problem, patients' overall survival time was predicted. Genes were downselected using kbest scores. After weeding out models that performed poorly with default parameters, GridSearchCV was used for hyperparameter tuning.

## Requirements
Use the package manager pip to install packages.

```
pip install csv, pandas, xenaPython, numpy, matplotlib, seaborn, dataframe_image, lifelines, sklearn, lightgbm, xgboost
```

## Plots
The following plots are generated:

1. Genes selected through feature selection
2. Distribution of cancer-related genes to check for "real" signal
3. Overall survival by treatment
4. Overall survival for all patients and radiation patients
5. Evaluation of regression (mean absolute error) and classification (accuracy)


## Support
If you have any issues, comments, or questions please contact wernerck@umich.edu.
