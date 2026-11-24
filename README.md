# Decision Support System for Drug Distribution Risk Analysis Using Expert Knowledge in Bayesian Parameters

Code and supplementary material for the manuscript submitted to *BitTech*. The study develops a Bernoulli Naive Bayes risk-prioritization model for pharmaceutical distribution transactions, with indicators and rule ordering specified from expert guidance, a prior of 0.15, one-at-a-time (OAT) and Monte Carlo sensitivity analysis, comparison with two baselines, and expert validation.

> **Status:** companion material for a manuscript under revision. It supports review and verification of the reported tables and figures; it is not an operational inspection tool.

## Authors

1. Thea Bayu Revalina
Study Program of Data Science, Faculty of Mathematics and Natural Sciences, Universitas Negeri Surabaya, Surabaya, Indonesia
Email: thea.233035@mhs.unesa.ac.id

2. Yuni Rosita Dewi
Study Program of Data Science, Faculty of Mathematics and Natural Sciences, Universitas Negeri Surabaya, Surabaya, Indonesia
Email: yunidewi@unesa.ac.id

3. Siska Puspitaningsih
Study Program of Data Science, Faculty of Mathematics and Natural Sciences, Universitas Negeri Surabaya, Surabaya, Indonesia
Email: siskapuspitaningsih@unesa.ac.id

4. Setyo Utami
BBPOM in Surabaya, Surabaya, Indonesia
Email: setyo.utami@pom.go.id

Corresponding author: Yuni Rosita Dewi (yunidewi@unesa.ac.id)

## Overview of the study

| Item | Value |
|---|---|
| Data source | e-WAS drug distribution transactions, BBPOM Surabaya |
| Raw records | 208,162 |
| Analysed transactions | 161,728 (after cleaning and standardization) |
| Model | Bernoulli Naive Bayes, prior 0.15, expert-guided likelihood ratios, missing indicators skipped |
| Risk categories | Low, Moderate, High, Unassessable |
| Sensitivity analysis | OAT and Monte Carlo (5,000 draws per scheme, seed 2026) |
| Validation | 9 rated transactions (T001-T012), two stratified expert samples (n = 98 and n = 59) with repeat assessments |

## Repository contents

| File | Description |
|---|---|
| `Cleaning_BBPOM_Final_Colab.ipynb` | Data cleaning: duplicate removal, filters and unit standardization (208,162 raw rows to 161,728 analysed transactions). |
| `KODE_1_FINAL.ipynb` | Indicator construction, Bernoulli Naive Bayes, baselines, OAT and Monte Carlo analysis, validation, and the tables and figures of the manuscript. |
| `tabel_suplemen_artikel.xlsx` | Supplementary Tables S1-S5: IQR limits, indicator frequencies and calibration, confusion matrices and validation measures, Monte Carlo stability, validation strata and weights. |
| `requirements.txt` | Python package versions used. |
| `README.md` | This file. |

## Supplementary Tables (`supplementary_tables.xlsx`)
| Table | Content | Sheets in the workbook |
|---|---|---|
| S1 | Large-quantity IQR thresholds ($Q_3 + 1.5 \times \text{IQR}$) and group sample sizes | `S1_Batas_IQR_E1`, `S1_Batas_IQR_E3` |
| S2 | Indicator eligibility rules, denominators, and calibrated conditional probabilities | `S2_Frekuensi_Indikator`, `S2_Kalibrasi_Prior`, `S2_Parameter_Referensi` |
| S3 | Complete expert-versus-model contingency matrix and binary confusion matrix for Validation 2 | `S3_Confusion_Validasi`, `S3_Ukuran_Validasi` |
| S4 | Pattern-level Monte Carlo sensitivity stability results across Schemes A and B | `S4_Stabilitas_Kategori`, `S4_Stabilitas_Pola`, `S4_MC_Ringkasan` |

## Requirements

- Python 3.11.7
- numpy 1.26.4, pandas 2.1.4, matplotlib 3.8.0, scipy 1.11.4, openpyxl 3.0.10
- Jupyter or Google Colab

```
pip install -r requirements.txt
```

## Reproducing the results

1. Place the input files (see *Data availability*) in the same folder as the notebooks.
2. Run `Cleaning_BBPOM_Final_Colab.ipynb` from top to bottom to produce the cleaned data.
3. Run `KODE_1_FINAL.ipynb` from top to bottom. The first cells check that the required files are present and print SHA-256 checksums of the cleaned data and the four validation files, so inputs can be verified.
4. Tables, figures and `tabel_suplemen_artikel.xlsx` are written to the working folder.

Do not edit the validation key and sheet files, and do not regenerate the validation samples: the notebook uses the original samples. Random seed for the Monte Carlo analysis is 2026.

## Data availability

The raw e-WAS data and the cleaned data belong to BBPOM Surabaya and are not distributed here. The expert assessment sheets and validation keys contain transaction-level records and are also withheld. This repository provides the code, the processing rules, parameter tables and aggregated supplementary tables so that the reported results can be inspected without exposing restricted data. Access to the underlying data for verification may be requested from the corresponding author, subject to approval by BBPOM.

Input files expected by the notebooks:

- `data_mentah_bbpom.csv` (208,162 rows, 18 columns)
- `data_baru_clean.csv` (161,728 rows)
- `kunci_sampel.xlsx`, `kunci_validasi_ulang.xlsx`
- `lembar_penilaian_pakar_terisi.xlsx`, `lembar_validasi_ulang_terisi.xlsx`

## Limitations

- The prior and likelihood ratios are researcher estimates that preserve the ordering of risk given by the expert; they are not numbers stated explicitly by the expert.
- All expert judgments come from a single expert, so repeated assessments measure intra-rater repeatability, not inter-rater reliability.
- The model prioritizes transactions for review. It does not establish that a transaction is a violation, and no outcome labels were available.

## Acknowledgments

The authors thank the Balai Besar Pengawas Obat dan Makanan (BBPOM) in Surabaya for access to e-WAS data, and the expert from BBPOM Surabaya for the indicator definitions, rule confirmations and transaction assessments. We also thank the Bachelor’s Program in Data Science, Faculty of Mathematics and Natural Sciences, Surabaya State University, for academic support and facilities. Their support made this study possible. 

