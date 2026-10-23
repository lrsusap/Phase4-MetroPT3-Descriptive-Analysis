# Phase 4 – Solution Implementation and Descriptive Analysis

## MetroPT3 Industrial Air Compressor Dataset

**Universidad Nacional Abierta y a Distancia – UNAD**  
**School:** Escuela de Ciencias Básicas, Tecnología e Ingeniería (ECBTI)  
**Course:** Data Analytics  
**Course Code:** 203018207  
**Academic Activity:** Phase 4 – Solution Implementation and Descriptive Analysis  
**Author:** Lewis Rafael Susa Peñate  
**Year:** 2026

---

## 1. Project Overview

This repository documents the implementation of an exploratory and descriptive analysis of the **MetroPT3 (Air Compressor)** dataset using Python and Google Colab.

MetroPT3 contains historical measurements from the Air Production Unit (APU) of a metropolitan train. The dataset includes physical measurements and digital operating signals associated with the behavior of an industrial air compressor.

The main purpose of this project is to transform historical sensor records into structured and interpretable information.

The analysis examines:

- Dataset structure and data quality.
- Statistical characteristics of physical measurements.
- Temporal behavior and sampling intervals.
- Variable distributions and statistical outliers.
- Relationships between analogue measurements.
- Compressor operating states.
- Documented air-leak event periods.
- Methodological limitations and future applications.

This project focuses on **exploratory and descriptive analysis**. It does not implement or validate predictive machine learning models during Phase 4.

---

## 2. Project Objectives

### General Objective

To implement an exploratory and descriptive analysis of the MetroPT3 dataset using Python-based software libraries, examining the statistical, temporal, and multivariate behavior of physical and operational variables to characterize compressor operating conditions and identify relevant patterns and relationships.

### Specific Objectives

**Objective 1 — Dataset Characterization**

Examine the dataset structure, data types, temporal characteristics, variables, and data quality.

**Objective 2 — Descriptive Analysis**

Analyze statistical distributions, temporal behavior, correlations, operating states, and potentially unusual observations.

**Objective 3 — Interpretation**

Interpret the results using the documented operating context of the compressor and identify possible applications and limitations for industrial condition monitoring.

---

## 3. Dataset Description

### 3.1 Dataset Characteristics

The analysis was performed using the supplied MetroPT3 CSV file.

| Characteristic | Verified result |
|---|---|
| Dataset | MetroPT3 (Air Compressor) |
| File format | CSV |
| Number of records | 1,516,948 |
| Original columns | 17 |
| Analogue variables | 7 |
| Digital variables | 8 |
| Timestamp columns | 1 |
| Additional index columns | 1 |
| First timestamp | 2020-02-01 00:00:00 |
| Last timestamp | 2020-09-01 03:59:50 |
| Predominant sampling interval | 10 seconds |
| Missing values | 0 |
| Duplicate complete records | 0 |
| Duplicate timestamps | 0 |

**Important:** The original MetroPT3 documentation describes 15,169,480 records acquired at a nominal frequency of 1 Hz. However, the CSV file analyzed in this academic activity contains 1,516,948 observations, with a predominant sampling interval of approximately 10 seconds.

The results presented in this repository correspond specifically to the supplied CSV version.

### 3.2 Analogue Variables

The dataset includes seven analogue measurements.

| Variable | Unit | Description |
|---|---|---|
| TP2 | bar | Compressor pressure |
| TP3 | bar | Pneumatic panel pressure |
| H1 | bar | Pressure associated with cyclonic separator discharge |
| DV_pressure | bar | Pressure-drop measurement associated with air-dryer discharge |
| Reservoirs | bar | Downstream reservoir pressure |
| Motor_current | A | Electric motor current |
| Oil_temperature | °C | Compressor oil temperature |

### 3.3 Digital Variables

The eight digital variables are:

| Variable | Operational information |
|---|---|
| COMP | Air intake valve control signal |
| DV_eletric | Compressor outlet valve control signal |
| Towers | Active air-drying tower |
| MPG | Pressure-related compressor control signal |
| LPS | Low-pressure signal |
| Pressure_switch | Air-drying tower discharge signal |
| Oil_level | Oil-level control signal |
| Caudal_impulses | Airflow-related pulse signal |

Digital variables are represented by values of 0 and 1.

Their interpretation depends on the documented function of each signal. A value of 1 does not have the same operational meaning for every variable.

---

## 4. Analytical Methodology

The project follows a structured analytical process adapted from the CRISP-DM methodology.

### Stage 1 — Problem Understanding

Definition of the analytical problem, objectives, scope, and research questions.

### Stage 2 — Data Understanding

Inspection of the dataset structure, variables, measurement units, temporal coverage, and operational context.

### Stage 3 — Data Preparation

Validation of data types, missing values, duplicated records, timestamps, numerical measurements, and digital signals.

The original source data are preserved, while a separate analytical dataset is prepared.

### Stage 4 — Exploratory and Descriptive Analysis

Application of statistical and graphical techniques, including:

- Mean and median.
- Standard deviation.
- Minimum and maximum.
- Percentiles and interquartile range.
- Histograms and box plots.
- Temporal analysis.
- Pearson and Spearman correlations.
- Digital signal frequencies.
- Grouped operating-state analysis.
- Descriptive comparison of documented air-leak periods.

### Stage 5 — Evaluation and Interpretation

Interpretation of the analytical findings according to the documented operating conditions of the compressor.

Statistical relationships are distinguished from causal relationships and confirmed equipment failures.

### Stage 6 — Documentation and Communication

Organization of the notebook, technical report, figures, results, academic evidence, and explanatory video.

---

## 5. Main Descriptive Findings

### 5.1 Analogue Measurements

Selected results from the descriptive analysis are presented below.

| Variable | Mean | Standard deviation |
|---|---:|---:|
| Oil_temperature | 62.644 °C | 6.516 °C |
| Motor_current | 2.050 A | 2.302 A |
| TP3 | 8.985 bar | 0.639 bar |
| Reservoirs | 8.985 bar | 0.638 bar |

These global statistics summarize the recorded observations but do not represent a single operating condition.

### 5.2 Statistical Outliers

The conventional 1.5 × IQR method produced the following results.

| Variable | Observations outside IQR limits |
|---|---:|
| TP2 | 17.772% |
| H1 | 15.909% |
| DV_pressure | 7.456% |
| Motor_current | 0.000% |

Statistical outliers are not automatically considered sensor errors or confirmed equipment failures.

### 5.3 Correlation Analysis

Selected Pearson correlation coefficients include:

| Variable pair | Pearson correlation |
|---|---:|
| TP3 / Reservoirs | Approximately +1.000 |
| TP2 / H1 | -0.961 |
| TP2 / Motor_current | +0.697 |
| Oil_temperature / Motor_current | +0.529 |

These results reveal relevant statistical relationships between compressor measurements.

However, correlation does not establish causality.

### 5.4 Operating-State Analysis

The digital signals COMP and DV_eletric were used to provide additional context for interpreting physical measurements.

| Operating signal | State | Mean motor current | Mean oil temperature |
|---|---:|---:|---:|
| DV_eletric | 0 | 1.356 A | 61.955 °C |
| DV_eletric | 1 | 5.681 A | 66.244 °C |
| COMP | 0 | 5.604 A | 66.094 °C |
| COMP | 1 | 1.358 A | 61.972 °C |

The contingency analysis identified:

- **98.89%** of observations with complementary COMP and DV_eletric states.
- **1.11%** of observations with non-complementary states.

These results support the interpretation of different compressor operating regimes.

The non-complementary records require additional investigation and must not automatically be classified as abnormal operation.

### 5.5 Documented Air-Leak Events

Four documented air-leak periods were examined as contextual references.

The analysis identified 29,954 observations within these periods.

Compared with observations outside the reported event intervals, the event groups exhibited:

- Higher average motor current.
- Higher average oil temperature.
- Lower average TP3 and Reservoirs pressures.

These differences are descriptive associations. They do not independently establish the causes of the reported events or demonstrate predictive performance.

---

## 6. Tools and Technologies

The analytical implementation uses the following technologies:

| Tool | Purpose |
|---|---|
| Python | Programming language |
| Google Colab | Notebook development and execution |
| pandas | Data manipulation and descriptive analysis |
| NumPy | Numerical computation |
| Matplotlib | Statistical visualization |
| Google Drive | Dataset and analytical file storage |
| GitHub | Code versioning, documentation, and publication |

Additional dependencies must be verified against the final notebook before publication.

---

## 7. Repository Structure

The proposed organization is:

```text
Phase4-MetroPT3-Descriptive-Analysis/
│
├── README.md
│
├── notebooks/
│   └── Phase4_MetroPT3_Descriptive_Analysis_Final.ipynb
│
├── documentation/
│   ├── Phase4_Technical_Report.pdf
│   └── MetroPT3_Technical_Code_Annex.pdf
│
├── evidence/
│   └── README.md
│
├── requirements.txt
│
└── .gitignore
```

The structure will be completed as the verified files are uploaded.

The repository will not include simulated analytical results presented as actual outputs.

---

## 8. How to Reproduce the Analysis

The analytical workflow was developed using Google Colab.

To reproduce the procedures:

1. Download or open the final Jupyter notebook.
2. Obtain the correct MetroPT3 dataset version.
3. Upload the CSV file to an accessible location in Google Drive or the Colab environment.
4. Check and update the dataset file path when necessary.
5. Install or import the required Python libraries.
6. Run the notebook cells in the documented order.
7. Verify the dataset structure and integrity checks.
8. Generate the descriptive tables and figures.
9. Compare the results with the technical report.

### Important Reproducibility Considerations

The supplied dataset version contains 1,516,948 records.

Using a different dataset version may produce different results.

The notebook may require access to a user-specific Google Drive location. Its file paths must be adapted to the environment used for reproduction.

The repository will document the final dataset access procedure and required dependencies.

A complete reproduction in an independent execution environment must be verified before claiming full external reproducibility.

---

## 9. Academic Participation and Forum Evidence

The project is developed within the Data Analytics course at Universidad Nacional Abierta y a Distancia.

The Phase 4 learning guide establishes academic discussion and collaborative planning as part of the activity.

The evidence section is intended to document actual contributions published in the official course forum.

Planned evidence includes:

- Initial academic contribution.
- Technical progress contribution.
- Presentation of descriptive findings.
- Tutor feedback, if received.
- Student response to tutor feedback, if applicable.

Only verified communications and actual screenshots will be included.

Evidence will be incorporated into the repository once available and reviewed.

---

## 10. Project Deliverables

The main academic deliverables are:

### 10.1 Code Repository

A public GitHub repository containing the final computational notebook, documentation, and supporting evidence.

### 10.2 Explanatory Video

An English-language video explaining:

- The selected analytical problem.
- The MetroPT3 dataset.
- The analytical methodology.
- The main descriptive findings.
- Operating-state relationships.
- Conclusions and methodological limitations.

The planned video duration is between 8 and 10 minutes, within the official 5–10 minute requirement.

**Video link:** To be added after publication.

### 10.3 Technical Report

The complete academic report documents the methodology, computational procedures, statistical findings, interpretation, limitations, and supporting evidence.

**Report file:** To be added after uploading the final PDF.

---

## 11. Analytical Limitations

The principal limitations of this study include:

- The supplied CSV has a lower effective temporal resolution than the nominal original dataset.
- Some intervals between observations are irregular.
- Consecutive observations are not necessarily statistically independent.
- Global descriptive statistics combine different operating regimes.
- Correlations do not establish causal relationships.
- The dataset does not provide independently verified failure labels for every observation.
- The documented air-leak periods do not allow direct conclusions about the cause of each measurement change.
- The findings cannot automatically be generalized to other compressors or industrial assets.

This phase does not evaluate predictive model accuracy or demonstrate a reduction in equipment failures.

---

## 12. Future Work

Potential extensions of the analysis include:

- Operating-state-specific statistical baselines.
- Improved temporal analysis and event characterization.
- Feature selection for predictive models.
- Anomaly detection methods.
- Machine learning and deep learning applications.
- Integration of sensor measurements with maintenance records.
- Application of the analytical methodology to other electromechanical assets.

These activities are proposed future developments and are not presented as validated results of Phase 4.

---

## 13. Data Source and References

The project uses the MetroPT3 (Air Compressor) dataset and its accompanying technical documentation.

The analysis is also supported by official documentation for Python, pandas, NumPy, and Matplotlib, together with the academic materials supplied by UNAD.

The complete bibliography, formatted according to APA 7, is included in the technical report.

The original MetroPT3 source and its distribution conditions must be checked before redistributing the dataset through this repository.

---

## 14. Academic Integrity and AI Assistance

Artificial intelligence tools were used as academic support during the development process, including assistance with explanations, writing, code review, and methodological organization.

The reported statistical findings correspond to the documented analysis of the MetroPT3 dataset and must be verified against the executable notebook.

The author remains responsible for reviewing the code, understanding the methods, validating the results, and ensuring the academic integrity of the submitted work.

---

## 15. Author and Institution

**Lewis Rafael Susa Peñate**  
Data Analytics – Phase 4  
Universidad Nacional Abierta y a Distancia – UNAD  
2026

**Project focus:** From raw industrial data to meaningful information for understanding compressor operating behavior.

---

*This repository is intended for academic documentation, reproducible descriptive analysis, and continuous methodological improvement.*
