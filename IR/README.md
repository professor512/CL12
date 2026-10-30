# 📄 IR — Information Retrieval Practicals

> A comprehensive guide to all practicals in the **IR** folder, covering the theory, code workflow, and dataset requirements.

---

## Practicals Overview

| # | Practical | File | Dataset Required | Dataset File |
|---|-----------|------|-----------------|--------------|
| 6 | Text Preprocessing | `6_Text_PreProcessing.ipynb` | ❌ No | Hardcoded in code |
| 7 | Inverted Files (Inverted Index) | `7_Inverted_Files.ipynb` | ❌ No | Hardcoded in code |
| 8 | Bayesian Network for Heart Disease | `8_Bayesian_Network_Heart_Data.ipynb` | ✅ Yes | `heart.csv` |
| 9 | Agglomerative Hierarchical Clustering | `9_Agglomerative_Hierarchical_Clustering.ipynb` | ✅ Yes | `CC_GENERAL.csv` |
| 10 | PageRank Algorithm | `10_Page_Rank_Algorithm.ipynb` | ❌ No | Hardcoded in code |

---

## 📝 Practical 6 — Text Preprocessing

**File:** `6_Text_PreProcessing.ipynb`
**Dataset Required:** ❌ None (text is hardcoded in the code)

### What is it?
Before a computer can understand text, it needs to be cleaned and simplified. This practical covers the essential **NLP (Natural Language Processing)** preprocessing steps.

### What the Code Does (Step by Step):

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

### Libraries Used:
```python
import nltk
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize
from nltk.stem import PorterStemmer
```

### Key Concepts:
| Term | Meaning |
|------|---------|
| Tokenization | Splitting text into words or sentences |
| Stop Words | Common words like "the", "is", "are" that are often removed |
| Stemming | Cutting words to their root (e.g., "running" -> "run") |
| Lemmatization | Smarter version of stemming using vocabulary (e.g., "ran" -> "run") |
| NLP | Natural Language Processing — making computers understand text |

---

## 🗂️ Practical 7 — Inverted Files (Inverted Index)

**File:** `7_Inverted_Files.ipynb`
**Dataset Required:** ❌ None (3 documents are hardcoded in the code)

### What is it?
Search engines like Google use an **Inverted Index** to find documents containing a word instantly. Instead of scanning every document for every query, the index maps each word to the list of documents it appears in — like a book's index.

### What the Code Does (Step by Step):

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

### Sample Inverted Index Output:
```
brown  -> Document 1
dog    -> Document 1, Document 2
fox    -> Document 1, Document 3
lazy   -> Document 1, Document 2
quick  -> Document 1, Document 3
the    -> Document 1, Document 2, Document 3
```

### Key Concepts:
| Term | Meaning |
|------|---------|
| Inverted Index | Maps words to documents (opposite of a document to words map) |
| Posting List | The list of documents for a given word |
| Forward Index | Maps documents to words |
| Boolean Retrieval | Search by AND/OR/NOT logic using the inverted index |

---

## ❤️ Practical 8 — Bayesian Network for Heart Disease Diagnosis

**File:** `8_Bayesian_Network_Heart_Data.ipynb`
**Dataset Required:** ✅ **`heart.csv`** (present in `IR/` folder)

### What is it?
A **Bayesian Network** is a probabilistic graph where nodes are variables and edges represent cause-effect relationships. This practical uses it to diagnose heart disease — given symptoms, what's the probability of having heart disease?

### Dataset (`heart.csv`):
- **303 patients**, **14 features** from the **Cleveland Heart Disease dataset**
- Key columns: `age`, `sex`, `cp` (chest pain), `trestbps` (blood pressure), `chol` (cholesterol), `heartdisease`

### What the Code Does (Step by Step):

1. **Load & Clean Data:**
   ```python
   heartDisease = pd.read_csv('heart.csv')
   heartDisease = heartDisease.replace('?', np.nan)
   ```

2. **Discretize Continuous Features** – Converts numbers into categories (e.g., age: Young/Middle/Old) because Bayesian Networks need discrete values.

3. **Define Network Structure** – Defines the directed acyclic graph (DAG) showing which variables affect others:
   - e.g., `age -> heartdisease`, `cp -> heartdisease`, etc.

4. **Learn Parameters (MLE)** – Learns the Conditional Probability Tables (CPTs) from data:
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

### Key Concepts:
| Term | Meaning |
|------|---------|
| Bayesian Network | Probabilistic graphical model with directed edges |
| CPT | Conditional Probability Table — P(node given parents) |
| DAG | Directed Acyclic Graph — arrows show cause-effect, no cycles |
| Variable Elimination | Algorithm for inference in Bayesian Networks |
| MLE | Maximum Likelihood Estimation — learns probabilities from data |

---

## 📊 Practical 9 — Agglomerative Hierarchical Clustering

**File:** `9_Agglomerative_Hierarchical_Clustering.ipynb`
**Dataset Required:** ✅ **`CC_GENERAL.csv`** (present in `IR/` folder)

### What is it?
Clustering groups similar data points together without any labels. **Agglomerative** clustering starts with each point as its own cluster and progressively merges the closest clusters. Applied to credit card customer data to find customer segments.

### Dataset (`CC_GENERAL.csv`):
- **~8,950 credit card customers**
- **17 numeric behavioral attributes** (balance, purchases, cash advance, payments, etc.)
- Goal: Group customers into segments for targeted marketing

### What the Code Does (Step by Step):

1. **Load & Clean Data:**
   ```python
   df = pd.read_csv("CC_GENERAL.csv")
   df.drop(columns=["CUST_ID"], inplace=True)
   df.fillna(df.mean(), inplace=True)
   ```

2. **Preprocess:**
   - **StandardScaler** – Scales all features to mean=0, std=1
   - **Normalize** – Makes each row have unit length (for better clustering)

3. **PCA** – Reduces 17 features to 2 dimensions for visualization

4. **Dendrogram** – Tree diagram showing the hierarchical merging of clusters:
   ```python
   shc.dendrogram(shc.linkage(X, method='ward'))
   ```

5. **Fit Clustering for k = 2 to 6** – Tests different numbers of clusters:
   ```python
   AgglomerativeClustering(n_clusters=k, linkage='ward')
   ```

6. **Silhouette Score** – Measures how well-separated the clusters are (higher = better):
   - Score ranges from -1 to 1
   - Best k = k with highest silhouette score

7. **Visualize Clusters** – Scatter plot of customers colored by cluster (using PCA 2D projection)

### Key Concepts:
| Term | Meaning |
|------|---------|
| Agglomerative | Bottom-up: starts with individual points, merges them |
| Dendrogram | Tree diagram showing the merging hierarchy |
| Ward Linkage | Merge strategy that minimizes within-cluster variance |
| Silhouette Score | Measures cluster quality (between -1 and 1) |
| PCA | Used here to reduce to 2D for visualization |

---

## 🌐 Practical 10 — PageRank Algorithm

**File:** `10_Page_Rank_Algorithm.ipynb`
**Dataset Required:** ❌ None (graph is hardcoded in the code)

### What is it?
**PageRank** is the algorithm Google originally used to rank web pages. A page is "important" if many other important pages link to it. This practical implements it on a small web-like graph.

### What the Code Does (Step by Step):

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

### The PageRank Formula:
```
PR(A) = (1 - d) / N + d * Sum [PR(B) / OutLinks(B)]
```
Where:
- `d` = damping factor (0.85)
- `N` = total number of pages
- Sum is over all pages B that link to A

### Key Concepts:
| Term | Meaning |
|------|---------|
| PageRank | Score measuring importance based on incoming links |
| Damping Factor | Probability of following a link (0.85 is standard) |
| Directed Graph | Graph where edges have direction (A->B is different from B->A) |
| Convergence | When PageRank scores stop changing between iterations |
| Centrality | General term for how "central" or "important" a node is |
