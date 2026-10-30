# 🧬 Bio — Bioinformatics Practicals

> A comprehensive guide to all practicals in the **Bio** folder, covering the theory, code workflow, and dataset requirements.

---

## Practicals Overview

| # | Practical | File | Dataset Required | Dataset File |
|---|-----------|------|-----------------|--------------|
| 1 | DNA Sequence Analysis | `1_DNA_Sequence_Analysis.ipynb` | ❌ No | Hardcoded in code |
| 2 | RNA-Seq Data Analysis | `2_RNA_Seq_Data_Analysis.ipynb` | ❌ No | Generated in code |
| 3 | Protein Structure Prediction | `3_Protein_Structure_Prediction.ipynb` | ❌ No | Fetched from PDB online |
| 4 | Molecular Docking & Virtual Screening | `4_Molecular_Docking_Virtual_Screening_Colab_FIXED_v2.ipynb` | ❌ No | Downloaded from PDB (1HVR) |
| 5 | Machine Learning for Genomic Data (SVM) | `5_Genomic_Data_ML_SVM.ipynb` | ✅ Yes | `Leukemia_GSE9476.csv` |
| 6 | Agricultural Genomics & GWAS | `6_Agricultural_Genomics_GWAS.ipynb` | ✅ Yes | `Genotypic_data.csv` + `Phenotypic_data.txt` |

---

## 🧬 Practical 1 — DNA Sequence Analysis

**File:** `1_DNA_Sequence_Analysis.ipynb`
**Dataset Required:** ❌ None (DNA sequence is hardcoded in the code)

### What is it?
DNA is the blueprint of life. It's made of 4 letters (bases): **A, T, G, C**. This practical teaches you how to analyze a DNA sequence using Python — no external files needed.

### What the Code Does (Step by Step):

1. **Input DNA** – A fixed DNA string is defined:
   ```
   ATGCGTACGTTAGCGATCGATGCGCGATATGCTAGCTAGCTAA
   ```

2. **Motif Search** – Finds where a specific short pattern (e.g., `ATG`) appears in the DNA using `re.finditer()`.
   - `ATG` = Start codon (tells the cell where a gene begins)
   - Found at positions: `[0, 19, 28]`

3. **GC Content** – Counts **G** and **C** bases.
   - GC Content = `(G + C) / Total * 100`
   - Higher GC content = more stable DNA
   - Result: `48.84%`

4. **ORF Finding** – ORFs (Open Reading Frames) are potential protein-coding regions.
   - Starts at `ATG` (start codon)
   - Ends at `TAA`, `TAG`, or `TGA` (stop codons)
   - Finds 3 ORFs of lengths 39, 24, and 15 base pairs

### Key Concepts:
| Term | Meaning |
|------|---------|
| Motif | Short repeated DNA pattern |
| GC Content | % of G and C bases (indicates stability) |
| ORF | Open Reading Frame — a protein-coding region |
| Codon | 3-letter DNA unit that codes for 1 amino acid |

---

## 🧪 Practical 2 — RNA-Seq Data Analysis

**File:** `2_RNA_Seq_Data_Analysis.ipynb`
**Dataset Required:** ❌ None (dataset is created inside the code itself)

### What is it?
RNA-Seq lets scientists compare which genes are **more active** (upregulated) or **less active** (downregulated) under different conditions (e.g., treated vs. untreated cells).

### What the Code Does (Step by Step):

1. **Creates a Fake RNA-Seq Dataset** – 10 genes x 6 samples (3 control, 3 treatment):
   ```python
   Control_1, Control_2, Control_3   # normal conditions
   Treatment_1, Treatment_2, Treatment_3  # after applying drug/treatment
   ```

2. **Calculates Mean Expression** – Averages across the 3 control and 3 treatment samples for each gene.

3. **Log2 Fold Change (LFC)** – How much a gene's expression changed:
   ```
   LFC = log2(Treatment_Mean / Control_Mean)
   ```
   - Positive LFC = upregulated (more active)
   - Negative LFC = downregulated (less active)
   - A pseudocount of `1` is added to avoid division by zero

4. **T-Test (Statistical Test)** – Checks if the difference between control and treatment is statistically significant (not just random chance).

5. **Multiple Testing Correction (FDR BH)** – Adjusts p-values to reduce false positives using the Benjamini-Hochberg method.

6. **Thresholds for Significance:**
   - Adjusted p-value < `0.05`
   - Absolute LFC >= `1` (i.e., at least 2x change)

7. **Volcano Plot** – A scatter plot showing all genes:
   - X-axis = Log2 Fold Change
   - Y-axis = -Log10(Adjusted P-value)
   - Genes in the top corners are the most significant

8. **Saves Results** to `differential_expression_results.csv`

### Key Concepts:
| Term | Meaning |
|------|---------|
| RNA-Seq | Technique to measure gene expression levels |
| Fold Change | Ratio of expression between two conditions |
| p-value | Probability that the result is due to chance |
| FDR | False Discovery Rate — corrects for multiple comparisons |
| Volcano Plot | Scatter plot for visualizing differential expression |

---

## 🔬 Practical 3 — Protein Structure Prediction

**File:** `3_Protein_Structure_Prediction.ipynb`
**Dataset Required:** ❌ None (fetches data from online PDB database)

### What is it?
Proteins are 3D molecules. Predicting their structure helps scientists understand their function and design drugs. This practical fetches real protein data and analyzes it.

### What the Code Does:
- Downloads and analyzes protein structures from the **RCSB Protein Data Bank (PDB)** online
- Performs structural analysis and visualization
- Uses **BioPython** library for protein data handling

### Key Concepts:
| Term | Meaning |
|------|---------|
| PDB | Protein Data Bank — database of 3D protein structures |
| FASTA | File format for protein/DNA sequences |
| Alpha Helix / Beta Sheet | Common 3D protein shapes |

---

## 💊 Practical 4 — Molecular Docking & Virtual Screening

**File:** `4_Molecular_Docking_Virtual_Screening_Colab_FIXED_v2.ipynb`
**Dataset Required:** ❌ None (downloads from PDB online — PDB ID: `1HVR`)

### What is it?
Drug discovery involves finding molecules that can "fit" into a protein's active site like a key in a lock. This is **molecular docking** — predicting how well a small drug molecule binds to a protein.

### What the Code Does (Step by Step):

1. **Downloads HIV-1 Protease** from PDB (ID: `1HVR`) — a protein involved in HIV replication

2. **Prepares Protein** – Removes water molecules, adds hydrogens using `prody` and `meeko`

3. **Defines Binding Site** – Uses the co-crystallized ligand **XK2** to identify the active site location (x, y, z coordinates)

4. **Prepares Drug-like Molecules** – Takes known HIV protease inhibitors from PubChem and converts them to a dockable format using **RDKit**

5. **Runs AutoDock Vina** – The docking engine that:
   - Tries millions of orientations for each drug molecule
   - Scores each one based on binding energy (in kcal/mol)
   - More negative score = better binding

6. **Virtual Screening** – Ranks all tested molecules by their docking scores

7. **Visualization** – Optionally uses PyMOL or UCSF Chimera to see the 3D binding pose

### Key Concepts:
| Term | Meaning |
|------|---------|
| Ligand | Small molecule drug candidate |
| Binding Site | The pocket in the protein where the drug fits |
| Docking Score | Predicted binding energy (more negative = better) |
| Virtual Screening | Automated testing of many drug candidates |
| AutoDock Vina | Popular software for molecular docking |

> Note: This is a computational prediction only. Real drug efficacy requires lab experiments.

---

## 🤖 Practical 5 — Machine Learning for Genomic Data (SVM)

**File:** `5_Genomic_Data_ML_SVM.ipynb`
**Dataset Required:** ✅ **`Leukemia_GSE9476.csv`** (present in `Bio/` folder)

### What is it?
Gene expression data has thousands of features (genes). Machine learning can use this data to classify cancer subtypes. This practical compares **Random Forest** vs **SVM** for classifying leukemia types.

### Dataset:
- **64 samples**, **22,283 gene expression features**
- Classes: `AML`, `Bone_Marrow`, `Bone_Marrow_CD34`, `PB`, `PBSC_CD34`
- From **CuMiDa** — Curated Microarray Database (GSE9476)

### What the Code Does (Step by Step):

1. **Load Data:**
   ```python
   DATA_PATH = r"Leukemia_GSE9476.csv"
   ```

2. **Preprocess:**
   - Separate features (genes) from labels (cancer type)
   - Drop non-numeric columns (`samples`)
   - Encode class names to numbers using `LabelEncoder`
   - Handle missing values with median imputation

3. **Train/Test Split:** 80% training, 20% testing (stratified)

4. **Train Two Models:**
   - **Random Forest** – 200 decision trees, votes for best class
   - **SVM (Linear)** – Finds optimal hyperplane to separate classes

5. **Evaluate:** Accuracy, Precision, Recall, F1-Score + 5-fold Cross-Validation

6. **Confusion Matrices** – Visual grid showing correct vs. incorrect predictions

7. **Feature Importance (RF)** – Top genes most useful for classification

8. **Dimensionality Reduction (PCA)** – Reduces 22,000+ genes to 2D for visualization

### Key Concepts:
| Term | Meaning |
|------|---------|
| SVM | Support Vector Machine — finds optimal decision boundary |
| Random Forest | Ensemble of many decision trees |
| Cross-Validation | Tests model on multiple splits for reliability |
| Confusion Matrix | Shows where model makes correct/wrong predictions |
| PCA | Principal Component Analysis — reduces dimensions |

---

## 🌾 Practical 6 — Agricultural Genomics & GWAS

**File:** `6_Agricultural_Genomics_GWAS.ipynb`
**Dataset Required:** ✅ **`Genotypic_data.csv`** + **`Phenotypic_data.txt`** (both present in `Bio/` folder)

### What is it?
GWAS (Genome-Wide Association Study) finds which genetic variants (SNPs) are linked to a specific trait (e.g., wheat water absorption).

### Dataset:
- **337 hard winter wheat lines** with GBS (Genotyping by Sequencing) SNPs
- **Genotypic data:** `Genotypic_data.csv` — each row = 1 SNP, each column = 1 wheat line
- **Phenotypic data:** `Phenotypic_data.txt` — traits: `SRC-W`, kernel diameter, hardness, flour yield
- Source: Dryad `doi:10.5061/dryad.6wwpzgn71`

### What the Code Does (Step by Step):

1. **Load Data** – genotypic CSV + phenotypic TXT file
2. **Data QC** – Match wheat lines, encode SNPs numerically, filter low-quality SNPs
3. **Association Test** – Linear regression between each SNP and trait (p-value per SNP)
4. **Multiple Testing Correction** – Bonferroni and FDR (BH) corrections
5. **Manhattan Plot** – Visualize significant SNPs across chromosomes
6. **QQ Plot** – Verify statistical assumptions
7. **Report Top SNPs** – List most strongly associated genetic markers

### Key Concepts:
| Term | Meaning |
|------|---------|
| SNP | Single Nucleotide Polymorphism — a single letter change in DNA |
| GWAS | Genome-Wide Association Study — links SNPs to traits |
| Bonferroni | Very strict correction for multiple testing |
| Manhattan Plot | Visualization of GWAS results across chromosomes |
| QQ Plot | Checks statistical assumptions of the test |
| GBS | Genotyping by Sequencing — modern SNP genotyping method |
