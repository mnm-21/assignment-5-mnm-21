# DA5401 Assignment 5 — Manifold Learning for Data Veracity Analysis (Yeast Multi-Label Classification)

This repository contains my submission for **DA5401 Assignment 5**, where I explore **manifold learning techniques** to analyze **data veracity challenges** in the Yeast multi-label classification dataset using **t-SNE** and **Isomap** visualizations.

The dataset contains **2417 samples, 103 features, and 14 labels**, presenting significant challenges for classification due to label overlap, noisy annotations, and complex manifold structure.

---

## 📂 Repository Contents

- `A5_Yeast_tSNE_Isomap.ipynb` — Main notebook exploring manifold learning techniques for data veracity analysis
- `yeast.arff` — Original Yeast dataset (ARFF format)
- `yeast.xml` — Dataset metadata
- `requirements.txt` — Python dependencies to run the notebook
- `README.md` — This file

---

## 👨‍🎓 Author

- **Name**: Mayank Chandak
- **Roll No.**: ME22B224

---

## 📊 Problem Overview

The Yeast dataset presents unique challenges for multi-label classification:

- **Extreme label imbalance**: Most samples have multiple labels, with only 32 samples having a single label (Class1)
- **Complex label combinations**: The most frequent combination is (Class3, Class4, Class12, Class13) with 237 samples
- **High-dimensional features**: 103 gene expression features require careful preprocessing
- **Data veracity issues**: Noisy labels, outliers, and overlapping class distributions

We investigate whether manifold learning techniques can reveal:
- **Noisy or ambiguous labels** through local neighborhood analysis
- **Outliers** that may indicate measurement errors or atypical samples
- **Hard-to-learn samples** in regions of high class overlap
- **Global manifold structure** that explains classification difficulty

---

## ⚙️ Setup & Usage

### Prerequisites
- Python 3.8 or higher
- pip (Python package installer)

### Installation Steps

1. Create and activate a virtual environment (recommended):
```bash
python -m venv venv

# On Windows:
venv\Scripts\activate

# On macOS/Linux:
source venv/bin/activate
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Launch Jupyter Notebook and run:
```bash
jupyter notebook
```
- Open `A5_Yeast_tSNE_Isomap.ipynb`
- Run cells sequentially

### Alternative: Using Conda
```bash
conda create -n da5401-a5 python=3.10 -y
conda activate da5401-a5
pip install -r requirements.txt
jupyter notebook
```

---

## 📋 Dependencies

The key packages used (see `requirements.txt`):
- `numpy`, `pandas`, `scipy` — core numeric/data stack
- `scikit-learn` — manifold learning (t-SNE, Isomap), preprocessing
- `matplotlib`, `seaborn` — visualization and plotting
- `jupyter`, `ipykernel` — notebook support

---

## 📁 File Structure

```
assignment-5-mnm-21/
├── A5_Yeast_tSNE_Isomap.ipynb    # Main analysis notebook
├── yeast.arff                     # Original dataset
├── yeast.xml                      # Dataset metadata
├── requirements.txt               # Python dependencies
└── README.md                      # This file
```

---

## 🔬 Methodology

### Data Preprocessing
1. **Feature-Label Separation**: Split 103 features from 14 binary labels
2. **Label Simplification**: Reduce 14 labels to 4 categories for visualization:
   - Class1 (single-label, 32 samples)
   - Class12 (most frequent, 1579 samples)
   - Class3+Class4+Class12+Class13 (common combination, 237 samples)
   - Other (remaining cases, 569 samples)
3. **Feature Scaling**: Apply StandardScaler for distance-based algorithms

### Manifold Learning Analysis

#### t-SNE (t-Distributed Stochastic Neighbor Embedding)
- **Purpose**: Preserve local neighborhoods to identify noisy labels and outliers
- **Parameters**: Perplexity values [0.2, 5, 30, 100, 1000]
- **Key Findings**: 
  - Perplexity 30 provides optimal balance between local structure and global coherence
  - Reveals embedded off-class points and isolated samples
  - Highlights regions of heavy class overlap

#### Isomap (Isometric Mapping)
- **Purpose**: Preserve global geodesic structure to understand manifold curvature
- **Parameters**: Neighbors [5, 10, 30, 100, 1000]
- **Key Findings**:
  - k=30 provides best compromise between connectivity and structure preservation
  - Reconstruction error decreases with larger neighborhoods
  - Reveals continuous curved manifold underlying the data

---

## 🔧 Troubleshooting

1. **Import Errors**
   - Ensure dependencies are installed: `pip install -r requirements.txt`
   - Check Python version (≥3.8)

2. **Memory Issues**
   - t-SNE and Isomap can be memory-intensive for large datasets
   - Consider reducing perplexity/neighbors for initial exploration
   - Use `random_state` parameter for reproducible results

3. **Visualization Clarity**
   - Adjust figure sizes and alpha values for better visibility
   - Consider different color schemes for better contrast
   - Use legends and titles for clear interpretation

4. **Performance Optimization**
   - Use `learning_rate='auto'` for t-SNE
   - Consider PCA initialization for faster convergence
   - Monitor reconstruction errors for Isomap parameter selection

---

## 📊 Dataset Information

- **Source**: Yeast Multi-Label Classification Dataset (ARFF format)
- **Characteristics**: 
  - 2417 samples
  - 103 gene expression features
  - 14 binary functional class labels
  - Extreme multi-label nature (most samples have multiple labels)
- **Objective**: Analyze data veracity challenges through manifold visualization to inform classification strategy

---

## 🎯 Key Insights

### Data Veracity Challenges Identified
1. **Noisy Labels**: Samples with rare labels embedded within dense regions of common labels
2. **Outliers**: Isolated samples that may indicate measurement errors or atypical experiments
3. **Hard-to-Learn Regions**: Areas of heavy class overlap requiring complex decision boundaries
4. **Manifold Curvature**: Global structure suggests non-linear relationships between features

### Implications for Classification
- **Linear models will underfit** due to manifold curvature
- **Multi-label aware losses** are essential for handling label overlap
- **Robust preprocessing** needed to handle outliers and noisy samples
- **Class-balanced sampling** may help with extreme imbalance
- **Label auditing** recommended for samples identified as outliers or mislabeled

---

## 📚 References

- Scikit-learn Documentation: TSNE, Isomap, preprocessing
- van der Maaten, L. & Hinton, G. (2008). Visualizing Data using t-SNE
- Tenenbaum, J.B. et al. (2000). A Global Geometric Framework for Nonlinear Dimensionality Reduction
- Research on multi-label classification and data veracity in bioinformatics