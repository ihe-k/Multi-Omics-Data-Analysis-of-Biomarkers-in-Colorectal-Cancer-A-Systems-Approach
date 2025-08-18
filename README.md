# Gene Expression and Dimensionality Reduction in Colorectal Cancer

## Overview
This project applies a systems-level bioinformatics approach to explore gene expression profiles in colorectal cancer (CRC). Using multivariate statistics and unsupervised machine learning, we identify key biomarkers, delineate molecular subgroups of patients, and uncover regulatory gene clusters relevant to CRC pathogenesis.

By integrating statistical inference, dimensionality reduction, and clustering techniques (e.g., PCA, MDS, TwoStep, HCA), the analysis supports precision oncology, health systems optimisation, and lays the foundation for future interdisciplinary research into the impact of misinformation on health-seeking behaviour and treatment adherence in the digital age.

* Focus: Molecular and systems-level stratification of CRC patients
* Themes: Cancer genomics, precision medicine, misinformation and systems health modelling 
* Core Methods: PCA, MDS, hierarchical clustering, t-tests, logistic regression and bootstrapping

## Objectives
* Select biologically relevant biomarkers via ΔΔCt thresholds and statistical filtering
* Reduce dimensionality using PCA to uncover functional gene groupings
* Classify CRC patients into subgroups with TwoStep and hierarchical clustering
* Validate clustering and component robustness with bootstrapping and significance tests
* Explore future applications in misinformation modelling and health systems strategy

## Dataset Summary
* Input: ΔΔCt values (relative gene expression from qPCR data)
* Biomarkers: 42 candidate genes → 15 selected via biological filtering and PCA suitability
* Samples: Gene expression profiles from individual colorectal cancer patients

## Methodology
1. Data Preprocessing & Filtering
* Missing values imputed (series mean)
* Z-score standardisation and autoscaling for PCA and clustering
* Range normalisation (–1 to 1) for Euclidean distance calculations
* ΔΔCt threshold of ±0.6 applied to retain meaningful biological signals

2. Principal Component Analysis (PCA)
* Reduced 15 genes to 4 components explaining 67.2% variance
* Varimax rotation enhanced interpretability
* Top-loading genes: TGFB3, MMP2, CDK6, EGFR

3. Multidimensional Scaling (MDS)
* Supported PCA results and revealed gene co-expression distances
* Strong fit (RSQ = 0.90582, Stress = 0.16287)

4. TwoStep Clustering
* Identified two patient subgroups based on expression profiles
* Cluster quality = 0.4 (fair), improved with outlier exclusion
* Clusters corresponded to upregulated vs. downregulated profiles

5. Hierarchical Cluster Analysis (HCA)
* Ward’s Method with Euclidean distance used for nested clustering
* Confirmed gene groupings and patient stratification
* Dendrograms revealed 3 major gene clusters

6. Statistical Testing & Biological Validation
* Paired-sample t-test: Selected genes were more downregulated (p < 0.005)
* Pairwise t-tests (Bonferroni-corrected) showed 16 significant gene pairs
* Volcano plot: Upregulated – EGFR, TGFB1, TGFB3; Downregulated – BID

7. Predictive Modelling
* Logistic regression identified significant predictors (e.g., Gene 03, 21, 37)
* ROC curve AUC analysis confirmed predictive strength (accuracy ~80%)
* Feature elimination balanced interpretability and performance

## Key Findings
* Biologically meaningful clusters emerged from PCA and HCA
* EGFR, TGFB1, TGFB3, and MMP2 were highly influential biomarkers
* Two molecular patient subtypes may inform targeted treatment strategies
* Volcano plot and pairwise tests confirmed expression significance
* Bootstrapping validated component and cluster stability (n = 27,500 iterations)

## Tools & Technologies
* Programming Languages: R, SPSS
* Libraries Used: limma, ggplot2, factoextra, cluster, MASS
* Platforms: RStudio, SPSS for clustering and preprocessing
* Visuals: PCA biplots, dendrograms, volcano plots and MDS plots

## Broader Implications
This analysis illustrates how molecular profiling and dimensionality reduction can:

* Support precision oncology by identifying clinically relevant biomarkers
* Enable health system planning through patient stratification
* Reveal biological pathways for therapeutic development
* Serve as a computational model foundation for studying social determinants, such as the effect of digital misinformation on patient behaviour and outcomes

## Future Directions
1. Multi-Omics Integration
   Combine transcriptomics with proteomics, metabolomics, and epigenetics for a fuller biological picture.
3. Longitudinal Modelling
   Link gene expression with patient outcomes (e.g., survival, treatment response) over time.
5. Machine Learning
    Employ ensemble learning, SVMs, or deep learning for enhanced classification and biomarker discovery.
7. Misinformation and Health Behaviour
* Model how misinformation influences diagnosis delays or treatment refusal
* Integrate social media trends with EHR and molecular data
* Collaborate with platforms (e.g., Google or Microsoft) to link misinformation spread with clinical impact

## Reproducibility
All preprocessing, statistical testing and visualisation scripts are shared in the repository. This project adheres to open science and reproducible research standards.

## Repository Structure

```plaintext
📁 GeneExpression-CRC/
├── README.md                 # Project summary and methodology
├── Report/                  
│   └── Report.pdf     # Full report with detailed results and discussion
├── Tables_Figures/                 # Plots and data visualisations (PCA, MDS, HCA, volcano)
├── .gitignore
```

## Citation & Acknowledgements
Please cite the project if using methods or results. Tools and literature referenced include:

Vaquerizas, J. M., Conde, L., Yankilevich, P., Cabezon, A., Minguez, P., Diaz-Uriarte, R., Al-Shahrour, F., Herrero, J., & Dopazo, J. (2005). GEPAS, an experiment-oriented pipeline for the analysis of microarray gene expression data. Nucleic Acids Research, 33(Web Server), W616–W620. https://doi.org/10.1093/nar/gki500
D’haeseleer, P. (2005). How does gene expression clustering work? Nat Biotechnol. Dec:23(12):1499-501. doi: 10.1038/nbt1205-1499. PMID: 16333293.
Meunier, B., Dumas, E., Piec, I., Béchet, D., Hébraud, M., & Hocquette, J. (2007). Assessment of Hierarchical Clustering Methodologies for proteomic Data Mining J. Proteome Res. 2007, 6 (1), 358−366. Journal of Proteome Research, 6(3), 1215. https://doi.org/10.1021/pr078001e
Gentleman, R.C., Carey, V.J., Bates, D.M., Bolstad, B., Dettling, M., Dudoit, S., Ellis, B., Gautier, L., Ge, Y., Gentry, J., Hornik, K., Hothorn, T., Huber, W., Iacus, S., Irizarry, R., Leisch, F., Li, C., Maechler, M., Rossini, A.J. and Sawitzki, G. (2004). Bioconductor: open software development for computational biology and bioinformatics. Genome Biology, [online] 5(10), p.R80. doi:https://doi.org/10.1186/gb-2004-5-10-r80.
Smyth G., Gentleman R., Carey V., Dudoit S., Irizarry R., Huber W. (2005). Limma: linear models for microarray data, Bioinformatics and Computational Biology Solutions Using R and Bioconductor. New YorkSpringer (pg. 397-420)
