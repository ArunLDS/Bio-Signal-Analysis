# Bio-Signal Analysis Project

## Overview
This project involves analyzing a dataset containing bio-signals data to understand factors influencing smoking behavior. The objective is to build a machine learning model that accurately 
classifies the presence or absence of smoking based on the bio-signals collected over several years.

## EDA Key Steps

### Data Loading and Inspection

- Imported necessary libraries and loaded the dataset.
- The dataset contains 55,692 entries and 27 columns, including both numerical and categorical data.
- No null values or duplicates were present.

### Initial Data Analysis

- Examined the distribution of categorical variables (gender, oral, tartar).
- Performed descriptive statistics on numerical features.
- Identified and removed non-informative columns (ID and oral).

### Data Visualization

- Visualized the distribution of each variable and identified skewness and outliers.
- Plotted relationships between smoking status and various features using histograms, boxenplots, bar plots, and count plots.
- Found that the majority of smokers are men, with fewer smokers among women, primarily between ages 20 and 30.
- Detected class imbalance, with non-smokers being more prevalent.

### Feature Selection

- Calculated Mutual Information (MI) scores to identify features most relevant to smoking behavior.
- Removed the Cholesterol feature due to its zero MI score.

### Pairwise Relationships

- Analyzed pairwise relationships among the top 7 numerical features with high MI scores using scatter plots, histograms, and KDE plots.

## Model Training and Evaluation Key Info

- Since the classes of this dataset are somewhat imbalanced, the model will be evaluated with recall, because in this particular scenario we want to reduce False Negatives which is crucial in scenarios like healthcare

### Feature Engineering

- Conducted PCA and added KMeans clustering labels as a new feature.
- Further created more new features based on PCA loadings.

### Resampling Techniques

- Experimented with Random Oversampling, SMOTE, and SMOTETomek to try to handle class imbalance effectively.

### Hyperparameter Tuning with Optuna (Optimization)

- Used Optuna for automated hyperparameter optimization, focusing on maximizing recall and then later AUCPR.

### Model Selection

- The model with the best recall used SMOTETomek resampled data during training and achieved a recall of 95.25% but it came with a huge drop in precision.
- On the other hand, the tuned baseline model balanced had a good enough balance precision and recall, performing decently in both aspects.
- Made a Radar plot to compare the two models
- If our priority is to avoid missing smokers, then choosing the model trained on SMOTETomek resampled and optimized for recall performs best.
- if both precision and recall are equally important, then Baseline (No Resampling) model optimized for AUCPR performs better.
