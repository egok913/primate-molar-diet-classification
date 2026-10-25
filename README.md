# Primate Molar Diet Classification

## Overview

This project uses multivariate statistical analysis and machine learning to speculate about the diet of the extinct primate genus **Teilhardina** based on the shape of its molars.

The dataset contains 116 primate molars represented by four numerical measurements describing tooth curvature and surface area. Some extinct genera have unknown diet labels. The goal of the project was to use the known dietary groups to classify the eight **Teilhardina** samples and assess what diet they most likely had.

This project was completed for **DSK805 – Multivariate Statistical Analysis** at the University of Southern Denmark.

## Dataset

Each molar is described using four numerical features:

* **DNE** — Dirichlet Normal Energy, a measure of overall tooth-surface curvature
* **positive_DNE** — the positive component of DNE
* **surface_area** — total surface area of the tooth
* **positive_surface_area** — surface area associated with positive curvature

The original dataset contains dietary categories including:

* Frugivore
* Folivore
* Omnivore
* Insectivore
* Frugivore-Folivore

Some samples have missing diet labels because they belong to extinct genera whose diets are unknown.

The raw dataset is not included in this repository.

## Methodology

### 1. Comparing dietary groups

Before classification, we investigated whether **Frugivore-Folivore** and **Folivore** should be treated as separate groups.

A **Hotelling's T² permutation test** with 9,999 permutations was used to compare the groups.

* Observed Hotelling's T²: **3.9317**
* Permutation p-value: **0.5040**

Since the result did not provide evidence of a significant difference, the two groups were merged into a single **Folivore** category.

### 2. Choosing classification models

Linear Discriminant Analysis (LDA) was initially considered. However, a **Box's M test** indicated that the covariance structures differed between groups (p < 0.05).

Because LDA assumes equal covariance matrices, the project instead used:

* **Quadratic Discriminant Analysis (QDA)**
* **Random Forest**

The **Genus** variable was not used as a classification feature because it could strongly influence the predictions through taxonomic grouping rather than tooth morphology.

### 3. Data preparation

The analysis:

1. Removed samples with unknown diet labels from the training data.
2. Used the four numerical tooth measurements as predictors.
3. Standardized the features using `StandardScaler`.
4. Trained the models using samples with known diets.
5. Applied the trained models to the eight **Teilhardina** samples.

## Results

### QDA

QDA classified:

| Predicted diet | Number of Teilhardina samples |
| -------------- | ----------------------------: |
| Omnivore       |                             8 |
| Folivore       |                             0 |
| Frugivore      |                             0 |
| Insectivore    |                             0 |

### Random Forest

Random Forest classified:

| Predicted diet | Number of Teilhardina samples |
| -------------- | ----------------------------: |
| Omnivore       |                             7 |
| Folivore       |                             1 |
| Frugivore      |                             0 |
| Insectivore    |                             0 |

Both models therefore strongly support the same overall conclusion: **Teilhardina was probably an omnivore**.

The Random Forest produced one Folivore prediction, but the remaining seven samples were classified as Omnivore.

## Conclusion

The analysis suggests that the extinct primate genus **Teilhardina** most likely had an **omnivorous diet**.

The agreement between QDA and Random Forest provides consistent evidence from the available molar-shape measurements, although the result should be interpreted as a statistical classification-based speculation rather than a definitive biological conclusion.

## Repository Contents

* `primate_molar_diet_classification.ipynb` — cleaned analysis notebook
* `primate_molar_diet_analysis_report.pdf` — project report

The raw `data.csv` dataset is not included.

## Limitations

The classification is based only on four numerical summaries of molar shape, and the true diet of the extinct Teilhardina samples is unknown. Therefore, the predictions cannot be directly validated against ground truth.

The analysis should be understood as an evidence-based statistical inference about the likely diet of Teilhardina.

## Authors

Engin Erkus, Martin Johansen, Shameek Khaled Egok, and William Stevenson.
