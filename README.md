# Multi-Omics-Data-Analysis-of-Biomarkers-in-Colorectal-Cancer-A-Systems-Approach
This project applied a systems-level approach to identify key biomarkers in colorectal cancer (CRC), utilising advanced statistical methods and multi-omics data to uncover patterns in gene expression. The findings enhance our understanding of tumour biology and support precision medicine and health system optimisation.

## Executive Summary
This project applied a systems-level approach to identify key biomarkers in colorectal cancer (CRC), utilising advanced statistical methods and multi-omics data to uncover patterns in gene expression. The findings enhance our understanding of tumour biology and support precision medicine and health system optimisation.  Importantly, this study lays the groundwork for future research that extends beyond molecular analysis, recognising the growing impact of misinformation on patient health-seeking behaviour and disease progression. Integrating biological insights with social and behavioural factors will be critical to developing comprehensive strategies for improving CRC diagnosis, treatment adherence and outcomes in the digital age.

## 1. Introduction and Background
Colorectal cancer (CRC) remains a leading cause of cancer morbidity and mortality worldwide. Advances in molecular profiling and systems biology have improved our ability to identify biomarkers that support early diagnosis, patient stratification, and targeted therapies. This study leverages cutting-edge statistical and bioinformatics methods to analyse gene expression patterns, revealing biologically meaningful clusters and regulatory networks relevant to CRC pathogenesis.  However, clinical outcomes are influenced not only by molecular factors but also by patient behaviour and information environments. The rapid spread of misinformation through digital platforms poses a significant challenge, potentially affecting treatment decisions and disease progression. While this project focuses on the molecular characterisation of CRC, it also acknowledges the critical need for future interdisciplinary research that integrates biological data with the dynamics of misinformation and health-seeking behaviours. Such integrated approaches are essential for designing effective interventions and policies that improve patient outcomes in an increasingly complex healthcare landscape.

## 2. Data Preprocessing and Biomarker Selection

### 2.1 Data Cleaning and Transformation
All preprocessing and cleaning procedures were performed in SPSS, ensuring a consistent and reproducible analysis pipeline. The following data cleaning steps were applied:

* Missing Value Handling: Missing gene expression values were addressed using series mean imputation in SPSS to preserve sample size while minimising bias.
* Z-Score Standardisation: Continuous variables were transformed into z-scores using the "Descriptives" function (Analyse > Descriptive Statistics > Descriptives), standardising gene expression values by subtracting the mean and dividing by the standard deviation. This allowed for comparison across genes with different scales and ensured a mean of 0 and standard deviation of 1.
* Autoscaling for PCA and Clustering: Prior to PCA and MDS, autoscaling (standardising to unit variance) was conducted to prevent variables with larger variances from dominating the principal components.
* Range Normalisation (-1 to 1): For hierarchical clustering, expression values were rescaled using min-max normalisation to a standard range of [-1, 1], which is particularly important for Euclidean-based distance metrics in SPSS clustering procedures.
* Log Transformation (ΔCt to ΔΔCt): Gene expression levels were already represented in ΔΔCt format, a logarithmic transformation based on PCR cycle thresholds, negating the need for further transformation to address skewness.
* Outlier Detection: Extreme values (z > ±3.0) were flagged and reviewed. In cases where biological plausibility or technical error could not be determined, values were winsorised or excluded depending on influence on overall patterns.
This structured approach ensured that statistical models were based on clean, normalised data, supporting valid biological inference and reliable computational results.

### 2.2 Biomarker Selection and Dimensional Adequacy
Initially, 17 biomarkers were selected based on biological relevance. The Kaiser-Meyer-Olkin (KMO) measure yielded 0.76, indicating sampling adequacy for PCA. After excluding overlapping genes CREB1 (Gene17) and PIK3R3 (Gene33) based on low uniqueness and functional redundancy, the KMO improved to 0.79, with explained variance rising to 67.2% across four components.
Filtering was applied using a ΔΔCt threshold of ±0.6 to retain biologically relevant biomarkers. A paired-samples t-test confirmed significant downregulation in selected genes compared to excluded ones (t = -3.198, p < 0.005).
PCA with Varimax rotation revealed four principal components. In this process, a covariance matrix was first computed to capture the relationships between the biomarkers. From this matrix, the eigenvectors and eigenvalues were derived. The eigenvectors represent the directions (principal components) in which the data varies the most, while the eigenvalues indicate the amount of variance explained by each component. To maximise interpretability, the Varimax rotation matrix was applied, transforming the principal components to make them more interpretable by ensuring the components are orthogonal (uncorrelated) and maximise variance along each axis.

Mathematically, the PCA can be represented as:
X = T ⋅ P<sub>T</sub> + E

where:
* X is the data matrix (gene expression values)
* T is the matrix of scores (coordinates of the data in the principal component space),
* P<sub>T</sub> is the matrix of eigenvectors (the loading vectors corresponding to each component),
* E is the residual matrix (error or unexplained variance).

The rotation matrix R was then used to adjust the principal component axes:

T<sub>rot</sub> = T ⋅ R

where T<sub>rot</sub> represents the rotated component scores. The goal of Varimax rotation is to make the component scores (the columns of Trot) as interpretable as possible by maximising the variance in each component across the biomarkers.

TGFB3, MMP2, CDK6, and EGFR were found to be dominant in Component 1 (explaining 32% of the variance), highlighting their key regulatory roles in colorectal cancer. Cross-loading was observed in multifunctional genes such as TGFB1 and EGF, which showed significant contributions to more than one component, reflecting inter-pathway interactions and suggesting their involvement in multiple molecular processes.

Additionally, the covariance matrix and eigenvectors were calculated during PCA to ensure that the variance-covariance relationships between biomarkers were appropriately captured. The eigenvectors corresponding to the highest eigenvalues were used to identify the most informative principal components that explain the majority of the variability in the gene expression data. This technique enabled dimensional reduction while retaining the biological meaning of the dataset.  The eigenvalue decomposition of the covariance matrix leads to the identification of the most informative principal components:

## Principal Component Analysis (PCA) Equation

$$
\Sigma \cdot \boldsymbol{v} = \lambda \cdot \boldsymbol{v}
$$

where:

* Σ is the covariance matrix
* **v** represents the eigenvectors (directions of maximum variance)
* λ represents the eigenvalues (magnitude of variance along each eigenvector)

This technique, through dimensionality reduction, allowed me to retain the biological significance of the gene expression data while reducing its complexity. By focusing on the top principal components I captured the major sources of variability in the dataset without losing meaningful biological information.

## 3. Statistical Analysis and Clustering of Gene Expression Profiles
Multidimensional scaling (MDS) visually confirmed clustering of biomarkers aligned with PCA components, illustrating functional similarity among genes. Distance measures and stress values indicated a strong model fit (RSQ = 0.90582, stress = 0.16287), reinforcing the validity of the clustering approach.
For patient stratification, TwoStep Cluster Analysis was performed. This method combines pre-clustering with agglomerative hierarchical clustering, making it ideal for mixed-type biomedical data such as gene expression and patient-level variability. The resulting dendrogram and silhouette analysis revealed two dominant patient groups, corresponding primarily to upregulated and downregulated biomarker profiles.

Although the cluster cohesion score was rated as fair (0.4), excluding outlier biomarkers (Genes 07 and 28) improved clarity and model fit. The model’s RSQ (0.90150) and stress value (0.20503) further validated its robustness. The hierarchical components of the TwoStep algorithm helped identify nested structure in the data, reflecting biologically relevant subgrouping.

This multi-method clustering approach, supported by PCA, MDS, and hierarchical TwoStep Cluster Analysis, enhances the interpretability of gene expression data and supports applications in precision oncology and health system stratification. Such insights can guide resource allocation, screening policies, and personalised treatment interventions.

### 3.1 Dimensionality Reduction and Visualisation
To explore high-dimensional gene expression data, Principal Component Analysis (PCA) and Multidimensional Scaling (MDS) were employed. PCA reduced the dimensionality of the 15 selected biomarkers, preserving approximately 67.2% of the total variance across four principal components. A 3D biplot visually separated biomarkers based on functional clustering, with key genes (e.g., TGFB1, TGFB3, EGFR, MMP2) heavily loading on Component 1.

MDS provided a complementary visualisation by projecting biomarker distances into two dimensions. The spatial distribution mirrored PCA-derived clusters, showing tight grouping of functionally related genes alongside identifiable outliers (e.g., Gene 07, Gene 28). Model fit was strong (RSQ = 0.90582, Stress = 0.16287), supporting the validity of the dimensionality reduction approach.

### 3.2 Gene Expression Filtering and Feature Selection
To enhance biological interpretability and statistical power, a filtering step was introduced based on ΔΔCt thresholds. Biomarkers exhibiting expression changes beyond ±0.6 ΔΔCt were retained, narrowing the focus to genes with the most biologically meaningful regulation. This reduced noise, improved PCA factor loadings, and aligned selected genes with known oncogenic pathways, such as EGFR, PI3K-AKT, and TGF-β signalling.

### 3.3 Patient Stratification via Clustering
TwoStep Cluster Analysis combines k-means pre-clustering with agglomerative hierarchical clustering, enabling automatic detection of subgroup structure in mixed-type datasets. This unsupervised method accommodates both continuous and categorical variables and determines the optimal number of clusters. Results revealed two distinct patient groups, broadly corresponding to upregulated and downregulated gene expression patterns.

Cluster quality score was 0.4 (fair), improving after exclusion of outlier biomarkers (Genes 07 and 28). This supports refined feature engineering as a means to enhance interpretability and classification accuracy.

This stratification highlights the potential for precision medicine, enabling molecular phenotypes to be mapped onto clinical subgroups — critical for health systems optimising resource allocation, screening protocols, and targeted therapies.

### 3.4 Validating a Hierarchical Cluster Analysis
To further strengthen patient stratification and gene expression profiling, Hierarchical Cluster Analysis (HCA) was conducted. This approach complements previous multivariate techniques like PCA and MDS by enabling visual and statistical exploration of nested clustering structures.

### 3.4.1 Methodology
The analysis employed Ward’s Method as the clustering algorithm, using Euclidean distance as the dissimilarity measure. Prior to clustering, all values were range-standardised from –1 to 1 to mitigate the impact of scale differences and ensure meaningful biological comparison.
Ward’s method was selected due to its strong statistical basis and proven utility in proteomics (Key, 2012). In comparison studies, it consistently outperformed other aggregation strategies—particularly when combined with Pearson-based or Euclidean distance metrics (Meunier et al., 2007).
“87% of 28 reviewed proteomic studies used either Euclidean distance or the Pearson coefficient for HCA” (Meunier et al., 2007).

### 3.4.2 Biological and Analytical Rationale
HCA is especially valuable when:

* Grouping genes with similar expression profiles to discover co-regulated biomarkers
* Classifying tumour samples without prior biological assumptions
* Visualising the hierarchical relationships between variables in complex, high-dimensional data (Vaquerizas et al. 2005; D’haeseleer, 2005)

In two-way HCA, both patients (columns) and genes (rows) are clustered, enabling simultaneous observation of patient subgrouping and biomarker co-expression patterns. The result is a dendrogram that reveals biological structure in the form of branching clusters. Genes or patients connected by shorter branches are mathematically more similar—this aids in the discovery of functionally coherent gene groups or clinically relevant patient subsets.

Ward’s method minimises the total error sum of squares (ESS) within clusters at each iteration, combining the two clusters that result in the smallest increase in ESS. The goal is to reduce the amount of information lost at every merging step:

(https://github.com/ihe-ke/Multi-Omics-Data-Analysis-of-Biomarkers-in-Colorectal-Cancer-A-Systems-Approach/Wards_eq.png)

3.3.4 Preprocessing Considerations
A key challenge in hierarchical clustering, particularly in omics data, is the presence of systematic technical variation, which can obscure true biological patterns. To mitigate this, data were standardised before clustering, and missing values were imputed where necessary. This ensures clustering is driven by biological signal rather than noise.
A good clustering method:
Preserves biological relevance of distance metrics
Improves pattern discovery in heatmaps or dendrograms
Minimises bias from instrumentation artifacts

3.3.5 Results and Interpretation
HCA confirmed three primary gene clusters, broadly aligning with PCA loadings and previously identified co-expression groups.
Outlier biomarkers (e.g., Genes 07 and 28) formed isolated branches, validating their exclusion in other models.
The dendrogram structure supports the notion of nested regulatory networks and is consistent with known biological roles of TGFB, EGFR, CDK, and BID pathways in colorectal cancer.
Inclusion of hierarchical clustering validates previously discovered gene clusters and enhances biological interpretability of patient stratification. As a complementary technique to PCA and TwoStep analysis, HCA adds robustness to unsupervised classification and supports systems-level exploration of tumour heterogeneity—aligning with broader goals in precision oncology and health system modelling.

4 Statistical Testing and Biological Validation
4.1 Statistical Tests
A paired samples t-test was conducted to compare expression between selected and excluded genes:
t = –3.198, p < 0.005
Mean ΔΔCt difference = –0.395 (95% CI [–0.57, –0.13])
Interpretation: Selected genes were significantly more downregulated, reinforcing the validity of the filtering approach.
Using R’s limma package, pairwise t-tests (Bonferroni-adjusted) were performed on gene pairs (n = 105 combinations). Sixteen gene pairs showed significant differential expression after correction. Key examples include:
BID (Gene05) vs. TGFB1 (Gene37)
CDK6 (Gene14) vs. EGFR (Gene21)
A volcano plot illustrated both the magnitude and significance of expression differences:
Top upregulated genes: EGF, EGFR, TGFB1, TGFB3
Top downregulated gene: BID
These results support these biomarkers as potential targets for diagnostic panels or therapeutic development.

4.2 Validation and Model Robustness
Bootstrapping with resampling (n = 27,500 replicates) was performed to validate the stability of biomarker clustering and component structure (Fig. 18). Confidence intervals confirmed the reliability of key PCA components and gene groupings.
4.2.1 Statistical Testing and Data Normality
To evaluate robustness of gene expression analysis and explore associations between biomarker profiles and cancer diagnosis, multiple statistical tests were applied:
Normality Assessment: The Shapiro-Wilk test assessed data distribution. Based on outcomes, appropriate parametric (Independent T-Test) or non-parametric (Mann-Whitney U Test) methods compared patient subgroups.
Correlation Analysis: Spearman’s rank correlation was chosen to explore biomarker relationships due to its robustness to non-normality and outliers, providing more reliable correlation estimates for high-dimensional, skewed biological data.
5. Predictive Modelling
5.1 Logistic Regression
Binary logistic regression identified several genes as significant predictors of cancer diagnosis. Genes 03, 11, 15, 21, 23, and 37 exhibited strong associations with cancer, with Gene 03 showing a 63% higher likelihood of diagnosis per unit increase in expression. This highlights the potential of these genes in predictive frameworks.
5.2 ROC Curve and AUC Analysis
Receiver Operating Characteristic (ROC) curves and Area Under the Curve (AUC) calculations demonstrated reasonable discriminative power for genes like Gene 03, Gene 21, and Gene 37, though Gene 21 showed limited statistical significance (p = 0.08). Model refinement through feature elimination resulted in a slight decrease in predictive accuracy from 80% to 78%.
5.3 Model Refinement and Feature Elimination
To improve model interpretability and reduce overfitting, non-significant variables were removed:
Genes 08, 15, 21, 23, and 31 were excluded based on their p-values and limited contribution to classification (Table 39, Table 40).
After refinement, the model's prediction accuracy decreased slightly from 80% to 78%, indicating a marginal trade-off between parsimony and predictive power.
This finding suggests that while certain variables may not be individually significant, they may contribute to model stability through weak interaction effects.

6. Implications for Systems Medicine and Health Systems Modelling
This study exemplifies the integration of systems thinking into health systems research by applying multivariate statistical methods to gene expression data. The findings suggest that identifying CRC biomarkers at the molecular level can guide patient stratification, improve therapeutic targeting, and optimise health system planning. The model developed here could inform resource allocation, early diagnosis, and personalised treatment strategies, ultimately improving patient outcomes.
Beyond identifying molecular biomarkers and stratifying patient subgroups, the systems approach presented here can be expanded to understand the broader impact of misinformation on patient health behaviours, such as treatment-seeking and adherence. Misinformation propagated through social media platforms can lead to delays in diagnosis, refusal of effective treatments, or adoption of harmful alternatives thereby affecting patient outcomes and health system burdens.
Leveraging the computational and statistical techniques applied in this study, future interdisciplinary projects could:
Model how misinformation clusters correlate with patterns of healthcare avoidance or non-adherence in colorectal cancer or other diseases.
Use social media and electronic health record (EHR) data integration to identify populations most vulnerable to misinformation-driven delays or treatment refusal.
Develop predictive frameworks to anticipate misinformation-induced health disparities, guiding targeted educational or policy interventions.
Collaborate with platforms such as Meta and Google to design real-time monitoring systems that link misinformation spread with measurable health impacts.
This translational perspective highlights the synergy between biomarker-based precision medicine and systems-level analysis of sociotechnical information flows, critical for improving both clinical and public health outcomes.

7. Reproducibility and Future Directions
This analysis was designed with reproducibility in mind. All data preprocessing scripts, statistical analyses, and visualisation code are made available in the repository. Future research should focus on:
Integrating multi-omics data (e.g., transcriptomics, proteomics, metabolomics) for deeper biological insights.
Incorporating clinical phenotypes and electronic health records (EHRs) to refine patient stratification.
Expanding the sample size and including longitudinal patient data for causal inference.
Employing advanced machine learning techniques for improved predictive accuracy and model interpretability.
Potential for Exploring Misinformation Impact on Disease Progression Building on the systems approach demonstrated here, future work could investigate how misinformation—especially on social media—affects disease progression and treatment outcomes in colorectal cancer. By integrating molecular biomarker data with patient behaviour metrics and misinformation exposure indices, researchers can model the influence of misinformation on treatment adherence, delays in diagnosis, and clinical trajectories. This interdisciplinary approach can inform targeted interventions to mitigate misinformation’s adverse effects, improving both individual patient outcomes and broader health system efficiency.
Additionally, collaborations across biomedical, computational social science, and health informatics fields will be essential to develop predictive frameworks and real-time monitoring systems linking misinformation dynamics to clinical impacts, advancing precision medicine and public health in tandem.
8. Conclusion
This project successfully applied a systems-level approach to identify key biomarkers in CRC, utilising advanced statistical methods to uncover patterns in gene expression data. The findings provide valuable insights for precision medicine and health system optimisation, demonstrating the power of multi-omics data analysis in transforming clinical and health policy practices.
Future research should build on these findings, incorporating broader datasets and advanced modelling techniques to further refine our understanding of CRC and its clinical implications, while also exploring the critical intersection of misinformation dynamics and health-seeking behaviour in the digital age. Investigating how misinformation influences patient outcomes and treatment adherence could enhance intervention strategies and health system resilience.
9. Appendix and References
Full tables, figures, and detailed statistical outputs are available in the project repository. Key references supporting the biological and computational methods used in this study are cited throughout the report.

10. Suggestions for Future Work
Integration with Proteomics and Metabolomics: Expanding the analysis to include proteomic and metabolomic data will provide a more comprehensive view of CRC biomarkers, capturing post-transcriptional modifications and metabolic alterations that may not be reflected in gene expression alone.
Longitudinal Studies: Incorporating longitudinal clinical outcomes would allow for a more nuanced understanding of how gene expression changes over time and its association with CRC progression, treatment response, and survival.
Machine Learning Approaches: Advanced machine learning models, such as ensemble methods or neural networks, could enhance predictive accuracy and identify new patterns in the data that might be missed by traditional statistical methods.
Broader Clinical Applications: The integration of genetic data with clinical data (e.g., patient demographics, treatment histories, and imaging data) could further refine patient stratification, leading to more precise and individualised treatment plans.
Exploring the Impact of Misinformation: Future work could investigate how misinformation, particularly on social media platforms, impacts disease progression, patient decision-making, and treatment adherence. Combining molecular biomarker data with behavioural and social data may provide new insights into mitigating misinformation’s effects on health outcomes.
