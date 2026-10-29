# CL12 – Computational Lab 12: Bioinformatics & Information Retrieval Practicals

> A comprehensive guide to all practicals in the **Bio** and **IR** folders, covering the theory, code workflow, and dataset requirements.

---

## 📂 Folder: `Bio/` — Bioinformatics Practicals

---

### 🧬 Practical 1 — DNA Sequence Analysis

**File:** `1_DNA_Sequence_Analysis.ipynb`
**Dataset Required:** ❌ None (DNA sequence is hardcoded in the code)

#### What is it?
DNA is the blueprint of life. It's made of 4 letters (bases): **A, T, G, C**. This practical teaches you how to analyze a DNA sequence using Python — no external files needed.

#### What the Code Does (Step by Step):

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

#### Key Concepts:
| Term | Meaning |
|------|---------|
| Motif | Short repeated DNA pattern |
| GC Content | % of G and C bases (indicates stability) |
| ORF | Open Reading Frame — a protein-coding region |
| Codon | 3-letter DNA unit that codes for 1 amino acid |

---

### 🧪 Practical 2 — RNA-Seq Data Analysis

**File:** `2_RNA_Seq_Data_Analysis.ipynb`
**Dataset Required:** ❌ None (dataset is created inside the code itself)

#### What is it?
RNA-Seq lets scientists compare which genes are **more active** (upregulated) or **less active** (downregulated) under different conditions (e.g., treated vs. untreated cells).

#### What the Code Does (Step by Step):

1. **Creates a Fake RNA-Seq Dataset** – 10 genes × 6 samples (3 control, 3 treatment):
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

5. **Multiple Testing Correction (FDR BH)** – When testing many genes, we adjust p-values to reduce false positives. Uses the Benjamini-Hochberg method.

6. **Thresholds for Significance:**
   - Adjusted p-value < `0.05`
   - Absolute LFC >= `1` (i.e., at least 2x change)

7. **Volcano Plot** – A scatter plot showing all genes:
   - X-axis = Log2 Fold Change
   - Y-axis = -Log10(Adjusted P-value)
   - Genes in the top corners are the most significant

8. **Saves Results** to `differential_expression_results.csv`

#### Key Concepts:
| Term | Meaning |
|------|---------|
| RNA-Seq | Technique to measure gene expression levels |
| Fold Change | Ratio of expression between two conditions |
| p-value | Probability that the result is due to chance |
| FDR | False Discovery Rate — corrects for multiple comparisons |
| Volcano Plot | Scatter plot for visualizing differential expression |

---

### 🔬 Practical 3 — Protein Structure Prediction

**File:** `3_Protein_Structure_Prediction.ipynb`
**Dataset Required:** ❌ None (fetches data from online PDB database)

#### What is it?
Proteins are 3D molecules. Predicting their structure helps scientists understand their function and design drugs. This practical fetches real protein data and analyzes it.

#### What the Code Does:
- Downloads and analyzes protein structures from the **RCSB Protein Data Bank (PDB)** online
- Performs structural analysis and visualization
- Uses **BioPython** library for protein data handling

#### Key Concepts:
| Term | Meaning |
|------|---------|
| PDB | Protein Data Bank — database of 3D protein structures |
| FASTA | File format for protein/DNA sequences |
| Alpha Helix / Beta Sheet | Common 3D protein shapes |

---

### 💊 Practical 4 — Molecular Docking & Virtual Screening

**File:** `4_Molecular_Docking_Virtual_Screening_Colab_FIXED_v2.ipynb`
**Dataset Required:** ❌ None (downloads from PDB online — PDB ID: `1HVR`)

#### What is it?
Drug discovery involves finding molecules that can "fit" into a protein's active site like a key in a lock. This is **molecular docking** — predicting how well a small drug molecule binds to a protein.

#### What the Code Does (Step by Step):

1. **Downloads HIV-1 Protease** from PDB (ID: `1HVR`) — a protein involved in HIV replication

2. **Prepares Protein** – Removes water molecules, adds hydrogens using `prody` and `meeko`

3. **Defines Binding Site** – Uses the co-crystallized ligand **XK2** to identify the active site location (x, y, z coordinates)

4. **Prepares Drug-like Molecules** – Takes known HIV protease inhibitors from PubChem and converts them to a dockable format using **RDKit**

5. **Runs AutoDock Vina** – The docking engine that:
   - Tries millions of orientations for each drug molecule
   - Scores each one based on binding energy (in kcal/mol)
   - More negative score = better binding

6. **Virtual Screening** – Ranks all tested molecules by their docking scores
   - Top-ranked molecules are most likely to be effective drugs

7. **Visualization** – Optionally uses PyMOL or UCSF Chimera to see the 3D binding pose

#### Key Concepts:
| Term | Meaning |
|------|---------|
| Ligand | Small molecule drug candidate |
| Binding Site | The pocket in the protein where the drug fits |
| Docking Score | Predicted binding energy (more negative = better) |
| Virtual Screening | Automated testing of many drug candidates |
| AutoDock Vina | Popular software for molecular docking |

> Note: This is a computational prediction only. Real drug efficacy requires lab experiments.

---

### 🤖 Practical 5 — Machine Learning for Genomic Data (SVM)

**File:** `5_Genomic_Data_ML_SVM.ipynb`
**Dataset Required:** ✅ **`Leukemia_GSE9476.csv`** (present in `Bio/` folder)

#### What is it?
Gene expression data has thousands of features (genes). Machine learning can use this data to classify cancer subtypes. This practical compares **Random Forest** vs **SVM** for classifying leukemia types.

#### Dataset:
- **64 samples**, **22,283 gene expression features**
- Classes: `AML`, `Bone_Marrow`, `Bone_Marrow_CD34`, `PB`, `PBSC_CD34`
- From **CuMiDa** — Curated Microarray Database (GSE9476)

#### What the Code Does (Step by Step):

1. **Load Data:**
   ```python
   DATA_PATH = r"Leukemia_GSE9476.csv"
   ```

2. **Preprocess:**
   - Separate features (genes) from labels (cancer type)
   - Drop non-numeric columns (`samples`)
   - Encode class names to numbers using `LabelEncoder`
   - Handle missing values with median imputation

3. **Train/Test Split:**
   - 80% training, 20% testing (stratified)
   - Result: 51 train samples, 13 test samples

4. **Train Two Models:**
   - **Random Forest** – 200 decision trees, votes for best class
   - **SVM (Linear)** – Finds optimal hyperplane to separate classes; uses `StandardScaler` inside a pipeline

5. **Evaluate:**
   - Metrics: Accuracy, Precision, Recall, F1-Score
   - 5-fold Cross-Validation for reliability
   - Results on this dataset: SVM = 100%, RF = 92.3%

6. **Confusion Matrices** – Visual grid showing correct vs. incorrect predictions

7. **Feature Importance (RF)** – Top genes most useful for classification

8. **Dimensionality Reduction (PCA)** – Reduces 22,000+ genes to 2D for scatter plot visualization

#### Key Concepts:
| Term | Meaning |
|------|---------|
| SVM | Support Vector Machine — finds optimal decision boundary |
| Random Forest | Ensemble of many decision trees |
| Cross-Validation | Tests model on multiple splits for reliability |
| Confusion Matrix | Shows where model makes correct/wrong predictions |
| PCA | Principal Component Analysis — reduces dimensions |

---

### 🌾 Practical 6 — Agricultural Genomics & GWAS

**File:** `6_Agricultural_Genomics_GWAS.ipynb`
**Dataset Required:** ✅ **`Genotypic_data.csv`** + **`Phenotypic_data.txt`** (both present in `Bio/` folder)

#### What is it?
GWAS (Genome-Wide Association Study) finds which genetic variants (SNPs) are linked to a specific trait (e.g., wheat water absorption). Like finding which "genetic word" in a wheat plant's DNA determines how it absorbs water.

#### Dataset:
- **337 hard winter wheat lines** with GBS (Genotyping by Sequencing) SNPs
- **Genotypic data:** `Genotypic_data.csv` — each row = 1 SNP, each column = 1 wheat line
- **Phenotypic data:** `Phenotypic_data.txt` — traits: `SRC-W`, kernel diameter, hardness, flour yield
- From Dryad: `doi:10.5061/dryad.6wwpzgn71`

#### What the Code Does (Step by Step):

1. **Load Data:**
   ```python
   GENO_PATH  = r"Genotypic_data.csv"
   PHENO_PATH = r"Phenotypic_data.txt"
   TRAIT_COL  = "SRC-W"  # water absorption capacity
   ```

2. **Data QC (Quality Control):**
   - Match wheat lines between genotype and phenotype files (496 lines matched)
   - Encode SNPs: convert letter codes (A, G, C, T, R...) to numeric (0, 1, 2)
   - Filter SNPs with too many missing values or no variation

3. **Association Test per SNP:**
   - For each SNP (23,130 total), runs a **linear regression** between SNP genotype and trait value
   - Gets a p-value for each SNP — lower = more significant association

4. **Multiple Testing Correction:**
   - Applies **Bonferroni correction** (very strict) and **FDR (BH)** correction
   - Reduces false positives across thousands of tests

5. **Manhattan Plot:**
   - X-axis = SNP position on chromosomes
   - Y-axis = -log10(p-value)
   - Peaks (hits) above the threshold line = significant SNPs
   - Named "Manhattan" because the peaks look like a city skyline

6. **QQ Plot (Quantile-Quantile Plot):**
   - Checks if the test results follow expected statistics
   - A good GWAS should follow the diagonal closely until the true hits deviate

7. **Reports Top SNPs** – Lists the most strongly associated genetic markers

#### Key Concepts:
| Term | Meaning |
|------|---------|
| SNP | Single Nucleotide Polymorphism — a single letter change in DNA |
| GWAS | Genome-Wide Association Study — links SNPs to traits |
| Bonferroni | Very strict correction for multiple testing |
| Manhattan Plot | Visualization of GWAS results across chromosomes |
| QQ Plot | Checks statistical assumptions of the test |
| GBS | Genotyping by Sequencing — modern SNP genotyping method |

---

---

## 📂 Folder: `IR/` — Information Retrieval Practicals

---

### 📝 Practical 6 — Text Preprocessing

**File:** `6_Text_PreProcessing.ipynb`
**Dataset Required:** ❌ None (text is hardcoded in the code)

#### What is it?
Before a computer can understand text, it needs to be cleaned and simplified. This practical covers the essential **NLP (Natural Language Processing)** preprocessing steps.

#### What the Code Does (Step by Step):

**Input text:**
```
"Programmers are programming different programs with programming languages."
```

1. **Tokenization** – Splits the sentence into individual words (tokens):
   ```python
   words = word_tokenize(text)
   # ['Programmers', 'are', 'programming', ...]
   ```

2. **Stop Word Removal** – Removes common words that don't carry meaning:
   - Removed: `are`, `with` (from NLTK's English stop words list)
   - Kept: `['Programmers', 'programming', 'different', 'programs', 'programming', 'languages', '.']`

3. **Stemming (Porter Stemmer)** – Reduces words to their root form:
   - `programming` -> `program`
   - `Programmers` -> `programm`
   - `different` -> `differ`
   - `languages` -> `languag`

#### Libraries Used:
```python
import nltk
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize
from nltk.stem import PorterStemmer
```

#### Key Concepts:
| Term | Meaning |
|------|---------|
| Tokenization | Splitting text into words or sentences |
| Stop Words | Common words like "the", "is", "are" that are often removed |
| Stemming | Cutting words to their root (e.g., "running" -> "run") |
| Lemmatization | Smarter version of stemming using vocabulary (e.g., "ran" -> "run") |
| NLP | Natural Language Processing — making computers understand text |

---

### 🗂️ Practical 7 — Inverted Files (Inverted Index)

**File:** `7_Inverted_Files.ipynb`
**Dataset Required:** ❌ None (3 documents are hardcoded in the code)

#### What is it?
Search engines like Google use an **Inverted Index** to find documents containing a word instantly. Instead of scanning every document for every query, the index maps each word to the list of documents it appears in — like a book's index.

#### What the Code Does (Step by Step):

**3 hardcoded documents:**
```
Document 1: "The quick brown fox jumped over the lazy dog."
Document 2: "The lazy dog slept in the sun."
Document 3: "The quick fox is running in the forest."
```

1. **Tokenization** – Each document is lowercased and split into words:
   ```python
   tokens1 = document1.lower().replace(".", "").split()
   ```

2. **Build Inverted Index** – Creates a dictionary mapping each word to the documents it appears in:
   ```python
   inverted_index = {
       "brown": ["Document 1"],
       "dog":   ["Document 1", "Document 2"],
       "fox":   ["Document 1", "Document 3"],
       "lazy":  ["Document 1", "Document 2"],
       ...
   }
   ```

3. **Display Index** – Prints all words alphabetically with their document lists

4. **Document Retrieval** – User enters a query word:
   ```
   Enter a word to search: lazy
   -> Documents containing lazy: Document 1, Document 2
   ```

#### Sample Inverted Index Output:
```
brown  -> Document 1
dog    -> Document 1, Document 2
fox    -> Document 1, Document 3
lazy   -> Document 1, Document 2
quick  -> Document 1, Document 3
the    -> Document 1, Document 2, Document 3
```

#### Key Concepts:
| Term | Meaning |
|------|---------|
| Inverted Index | Maps words to documents (opposite of a document to words map) |
| Posting List | The list of documents for a given word |
| Forward Index | Maps documents to words |
| Boolean Retrieval | Search by AND/OR/NOT logic using the inverted index |

---

### ❤️ Practical 8 — Bayesian Network for Heart Disease Diagnosis

**File:** `8_Bayesian_Network_Heart_Data.ipynb`
**Dataset Required:** ✅ **`heart.csv`** (present in `IR/` folder)

#### What is it?
A **Bayesian Network** is a probabilistic graph where nodes are variables and edges represent cause-effect relationships. This practical uses it to diagnose heart disease — given symptoms, what's the probability of having heart disease?

#### Dataset (`heart.csv`):
- **303 patients**, **14 features** from the **Cleveland Heart Disease dataset**
- Key columns: `age`, `sex`, `cp` (chest pain), `trestbps` (blood pressure), `chol` (cholesterol), `heartdisease`

#### What the Code Does (Step by Step):

1. **Load & Clean Data:**
   ```python
   heartDisease = pd.read_csv('heart.csv')
   heartDisease = heartDisease.replace('?', np.nan)
   ```

2. **Discretize Continuous Features** – Converts numbers into categories (e.g., age: Young/Middle/Old) because Bayesian Networks need discrete values.

3. **Define Network Structure** – Defines the directed acyclic graph (DAG) showing which variables affect others:
   - e.g., `age -> heartdisease`, `cp -> heartdisease`, etc.

4. **Learn Parameters (MLE)** – Learns the Conditional Probability Tables (CPTs) from data using **Maximum Likelihood Estimation**:
   ```python
   model.fit(data, estimator=MaximumLikelihoodEstimator)
   ```

5. **Inference (Variable Elimination)** – Given known evidence, predicts unknown variables:
   ```python
   # Given: age=63, sex=Male, chest_pain=typical_angina
   # Query: What's P(heartdisease = 1)?
   result = inference.query(variables=['heartdisease'], evidence={'age': ..., 'cp': ...})
   ```

6. **Visualize the Network** – Uses `networkx` and `matplotlib` to draw the DAG

#### Key Concepts:
| Term | Meaning |
|------|---------|
| Bayesian Network | Probabilistic graphical model with directed edges |
| CPT | Conditional Probability Table — P(node given parents) |
| DAG | Directed Acyclic Graph — arrows show cause-effect, no cycles |
| Variable Elimination | Algorithm for inference in Bayesian Networks |
| MLE | Maximum Likelihood Estimation — learns probabilities from data |

---

### 📊 Practical 9 — Agglomerative Hierarchical Clustering

**File:** `9_Agglomerative_Hierarchical_Clustering.ipynb`
**Dataset Required:** ✅ **`CC_GENERAL.csv`** (present in `IR/` folder — downloads automatically if missing)

#### What is it?
Clustering groups similar data points together without any labels. **Agglomerative** clustering starts with each point as its own cluster and progressively merges the closest clusters. This is applied to credit card customer data to find customer segments.

#### Dataset (`CC_GENERAL.csv`):
- **~8,950 credit card customers**
- **17 numeric behavioral attributes** (balance, purchases, cash advance, payments, etc.)
- Goal: Group customers into segments for targeted marketing

#### What the Code Does (Step by Step):

1. **Load & Clean Data:**
   ```python
   df = pd.read_csv("CC_GENERAL.csv")
   df.drop(columns=["CUST_ID"], inplace=True)  # remove non-numeric ID
   df.fillna(df.mean(), inplace=True)           # fill missing values
   ```

2. **Preprocess:**
   - **StandardScaler** – Scales all features to mean=0, std=1
   - **Normalize** – Makes each row have unit length (for better clustering)

3. **PCA** – Reduces 17 features to 2 dimensions for visualization

4. **Dendrogram** – Tree diagram showing the hierarchical merging of clusters:
   ```python
   shc.dendrogram(shc.linkage(X, method='ward'))
   ```
   - The cut point on the Y-axis determines how many clusters to use

5. **Fit Clustering for k = 2 to 6** – Tests different numbers of clusters:
   ```python
   AgglomerativeClustering(n_clusters=k, linkage='ward')
   ```

6. **Silhouette Score** – Measures how well-separated the clusters are (higher = better):
   - Score ranges from -1 to 1
   - Best k = k with highest silhouette score

7. **Visualize Clusters** – Scatter plot of customers colored by cluster (using PCA 2D projection)

#### Key Concepts:
| Term | Meaning |
|------|---------|
| Agglomerative | Bottom-up: starts with individual points, merges them |
| Dendrogram | Tree diagram showing the merging hierarchy |
| Ward Linkage | Merge strategy that minimizes within-cluster variance |
| Silhouette Score | Measures cluster quality (between -1 and 1) |
| PCA | Used here to reduce to 2D for visualization |

---

### 🌐 Practical 10 — PageRank Algorithm

**File:** `10_Page_Rank_Algorithm.ipynb`
**Dataset Required:** ❌ None (graph is hardcoded in the code)

#### What is it?
**PageRank** is the algorithm Google originally used to rank web pages. A page is "important" if many other important pages link to it. This practical implements it on a small web-like graph.

#### What the Code Does (Step by Step):

1. **Create a Directed Graph:**
   ```python
   G = nx.DiGraph()
   G.add_edges_from([
       ("A", "B"), ("A", "C"), ("B", "C"), ("B", "D"),
       ("C", "A"), ("C", "D"), ("D", "C"), ("D", "E"),
       ("E", "D"), ("E", "F"), ("F", "C")
   ])
   ```
   - 6 nodes (A-F), 11 edges
   - Edge A->B means "page A links to page B"

2. **Visualize the Graph** – Draws the network with arrows

3. **Compute PageRank:**
   ```python
   pagerank = nx.pagerank(G, alpha=0.85)
   ```
   - `alpha = 0.85` is the **damping factor** (probability that a random user follows a link vs. jumps randomly)
   - Scores are iteratively computed until convergence
   - All scores sum to ~1.0

4. **Display Results** – Shows each node's PageRank score (sorted)

5. **Visualize PageRank** – Node sizes and colors are proportional to their PageRank score (bigger = more important)

6. **Bar Chart** – Compares PageRank values across all nodes

#### The PageRank Formula:
```
PR(A) = (1 - d) / N + d * Sum [PR(B) / OutLinks(B)]
```
Where:
- `d` = damping factor (0.85)
- `N` = total number of pages
- Sum is over all pages B that link to A

#### Key Concepts:
| Term | Meaning |
|------|---------|
| PageRank | Score measuring importance based on incoming links |
| Damping Factor | Probability of following a link (0.85 is standard) |
| Directed Graph | Graph where edges have direction (A->B is different from B->A) |
| Convergence | When PageRank scores stop changing between iterations |
| Centrality | General term for how "central" or "important" a node is |

---

## 📋 Dataset Summary

| Practical | File | Dataset Needed | Dataset File |
|-----------|------|----------------|--------------|
| Bio P1 | `1_DNA_Sequence_Analysis.ipynb` | ❌ No | Hardcoded |
| Bio P2 | `2_RNA_Seq_Data_Analysis.ipynb` | ❌ No | Generated in code |
| Bio P3 | `3_Protein_Structure_Prediction.ipynb` | ❌ No | Fetched from PDB online |
| Bio P4 | `4_Molecular_Docking_Virtual_Screening_Colab_FIXED_v2.ipynb` | ❌ No | Downloaded from PDB (1HVR) |
| Bio P5 | `5_Genomic_Data_ML_SVM.ipynb` | ✅ Yes | `Leukemia_GSE9476.csv` |
| Bio P6 | `6_Agricultural_Genomics_GWAS.ipynb` | ✅ Yes | `Genotypic_data.csv` + `Phenotypic_data.txt` |
| IR P6 | `6_Text_PreProcessing.ipynb` | ❌ No | Hardcoded |
| IR P7 | `7_Inverted_Files.ipynb` | ❌ No | Hardcoded |
| IR P8 | `8_Bayesian_Network_Heart_Data.ipynb` | ✅ Yes | `heart.csv` |
| IR P9 | `9_Agglomerative_Hierarchical_Clustering.ipynb` | ✅ Yes | `CC_GENERAL.csv` |
| IR P10 | `10_Page_Rank_Algorithm.ipynb` | ❌ No | Hardcoded |
