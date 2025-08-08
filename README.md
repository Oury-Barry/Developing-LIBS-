# Developing Laser-Induced Breakdown Spectroscopy (LIBS) for an Improved Identification and Quantification of ALuminium Alloys
## 🔍 Project Overview
This project applies Laser-Induced Breakdown Spectroscopy (LIBS) to quantify elemental concentrations in aluminium alloys, supporting better scrap classification. The workflow combines:

- Spectral pre-processing (baseline correction, normalization)

- Feature extraction from emission peaks

- Supervised regression modeling (PLSR, Lasso, Ridge, ElasticNet)

- Leave-One-Out Cross-Validation for performance validation

<div style="text-align: justify;"> Models were trained using certified reference (BAM/ERM-EB) and industrial alloys (Oetinger). The best-performing model (PLSR + SNV) achieved R² > 0.90 for Cu, Mg, and Si. The final pipeline was used to predict concentrations in automotive scrap samples and classify them into cast, wrought, or composite categories.</div>


## Objective 
<div style="text-align: justify;">This research focuses on developing Laser-Induced Breakdown Spectroscopy (LIBS) for an improved identification and quantification of aluminium alloys. 
The study was limited to at least five elements commonly found in aluminium alloys. These elements included copper, manganese, magnesium, silicon, and zinc. 
All measurements were carried out at room temperature at Helios Lab+ Helmholtz Institute for Resource Technology, Freiberg, Germany. The scope of the research included the following:</div>
<br></br>

🧪 Materials 
- Certified reference materials provided by Bundesargentur für Materialforschung.
- Reference materials provided by OETINGER Aluminium GmbH
- End-of-life aluminium scrap (BMW) 

✔️ Data Acquisition
- >More than 40,000 spectral lines collected using LIBS
-  Measurements at room temperature at Helmholtz Institute for Resource Technology, Freiberg, Germany

📁 Tools Used
- Python (Pandas, Scikit-learn, Matplotlib, Seaborn, Pybaselines etc.)
- Jupyter Notebooks
- Excel

🧼 Spectral Pre-processing
- Baseline Correction: Asymmetric Least Squares (ALS)
- Normalization:
  - Standard Normal Variate (SNV)
  - Multiplicative Scatter Correction (MSC)
  - Total Sum Normalization (TSN)

✔️ Correlation Analysis

To support model development, a correlation analysis between the normalised intensity for individual line and the known grade was conducted for the combined (BAM/ERM-EB and Oetinger), BAM/ERM-EB, and Oetinger samples. Key emission lines were selected based on their signal intensity, and minimal interference, supported by the NIST Atomic Spectral Database. 
-  Copper (Cu): Strong emission lines at 324.75 nm, 327.40 nm, and 510.55 nm showed high correlation (R² > 0.90) across all datasets.
-  Silicon (Si): Peaks at 251.61 nm, 288.16 nm, and 390.55 nm correlated well (R² > 0.95) in combined and BAM/ERM-EB datasets, but correlations dropped slightly in Oetinger samples, likely due to sample variability.
-  Magnesium (Mg): Four peaks (285.21, 383.23, 383.83, 518.36 nm) showed strong correlations (R² = 0.95–0.97) in combined and BAM/ERM-EB datasets using SNV normalization. Correlation decreased in Oetinger samples, especially at 285.21 nm (R² = 0.67), but improved with multiplicative scatter correction (MSC) up to R² = 0.80.
-  Manganese (Mn): Peaks at 403.08 nm and 403.31 nm had moderate correlations (R² = 0.75–0.85) in BAM/ERM-EB and combined datasets with SNV. In commmrcial cast-alloys (Oetinger samples), correlations were stronger (R² = 0.94–0.95) using SNV and MSC, indicating more stable Mn signals in industrial alloys.
-  Zinc (Zn): Showed poor correlation in commercial cast-alloys (Oetinger samples) and was excluded from modeling for that group.

✔️ Model Development and Validation 
 - Development and comparison of regression models included:
    - Partial Least Squares Regression (PLSR)
    - Least Absolute Shrinkage and Selection Operator (LASSO)
    - Ridge Regression
    - Elasticnet Regression
    - Validation: Leave-One-Out Cross-Validation (LOOCV)

🥇  Best Performance 


- For certified reference material (BAM/ERM-EB)
  
| Element | R²    | RMSE (%) | MAE (%) | Rel. RMSE (%) | Model | Pre-Pro |
|---------|-------|-----------|----------|----------------|--------|---------|
| Cu      | 0.957 | 0.282     | 0.226    | 16.33          | PLSR   | SNV     |
| Mn      | 0.745 | 0.116     | 0.065    | 30.00          | PLSR   | SNV     |
| Mg      | 0.945 | 0.256     | 0.210    | 15.87          | PLSR   | SNV     |
| Si      | 0.967 | 0.817     | 0.607    | 27.99          | PLSR   | SNV     |
| Zn      | 0.989 | 0.289     | 0.241    | 11.27          | PLSR   | MSC     |



- For Commercial cast-alloys (Oetinger)

| Element | R²    | RMSE (%) | MAE (%) | Rel. RMSE (%) | Model | Pre-Pro |
|---------|-------|-----------|----------|----------------|--------|---------|
| Cu      | 0.844 | 0.439     | 0.316    | 40.65          | PLSR   | SNV     |
| Mn      | 0.906 | 0.055     | 0.042    | 20.60          | PLSR   | MSC     |
| Mg      | 0.633 | 0.062     | 0.048    | 23.26          | LASSO  | MSC     |
| Si      | 0.951 | 0.371     | 0.250    | 4.21           | PLSR   | TSN     |


- For combined (BAM/ERM-EB and Oetigner)

| Element | R²    | RMSE (%) | MAE (%) | Rel. RMSE (%) | Model | Pre-Pro |
|---------|-------|-----------|----------|----------------|--------|----------|
| Cu      | 0.920 | 0.369     | 0.311    | 25.43%         | PLSR   | SNV      |
| Mn      | 0.574 | 0.137     | 0.100    | 50.87%         | PLSR   | SNV      |
| Mg      | 0.959 | 0.216     | 0.166    | 20.80%         | PLSR   | SNV      |
| Si      | 0.939 | 1.139     | 0.924    | 20.92%         | PLSR   | SNV      |

<br></br>🔍 LOOCV Performance Summary

### ✅ Leave-One-Out Cross-Validation (LOOCV) Performance

| Element | R² (CV) | RMSE (%) | MAE (%) | Model | Pre-Pro |
|---------|---------|-----------|----------|--------|----------|
| Cu      | 0.714   | 0.728     | 0.460    | PLSR   | SNV      |
| Mn      | 0.412   | 0.176     | 0.131    | PLSR   | SNV      |
| Mg      | 0.823   | 0.462     | 0.360    | PLSR   | SNV      |
| Si      | 0.961   | 0.888     | 0.681    | PLSR   | SNV      |
| Zn      | 0.962   | 0.538     | 0.422    | PLSR   | MSC      |


🔁 Leave-One-Out Cross-Validation for commercial cast-alloys (Oetinger)

| Element | R²    | RMSE (%) | MAE (%) | Model | Pre-Pro |
|---------|-------|-----------|----------|--------|----------|
| Cu      | 0.605 | 0.697     | 0.540    | PLSR   | SNV      |
| Mn      | 0.855 | 0.068     | 0.054    | PLSR   | MSC      |
| Mg      | 0.224 | 0.090     | 0.070    | LASSO  | MSC      |
| Si      | 0.889 | 0.553     | 0.433    | PLSR   | TSN      |


🔬 LOOCV performance for BAM/ERM-EB and Oetinger combined

| Element | R²    | RMSE (%) | MAE (%) | Model | Pre-Pro |
|---------|-------|-----------|----------|--------|----------|
| Cu      | 0.834 | 0.515     | 0.427    | PLSR   | SNV      |
| Mn      | 0.470 | 0.153     | 0.115    | PLSR   | SNV      |
| Mg      | 0.910 | 0.319     | 0.235    | PLSR   | SNV      |
| Si      | 0.916 | 1.337     | 1.081    | PLSR   | SNV      |


📌 Key Skills Demonstrated

- LIBS Data Analysis
- Spectral Signal Pre-processing
- Regression Modeling & Validation
- Programming in Python
- Data Visualization

🗺️ Applications
While designed for aluminium alloys, the workflow is adaptable to other materials (e.g., drill cores, rock samples), supporting geological exploration, mining, and materials recycling.
To adapt the workflow to such analytical tasks, reference samples with representative matrices and relevant grades of the element of interest are required.

✳️ Project Walk-through

<img width="600" height="600" alt="Final Diagram " src="https://github.com/user-attachments/assets/30db7e23-038b-4e01-bd8f-20645ca9cda2" />
