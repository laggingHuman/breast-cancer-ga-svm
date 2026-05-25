#  Breast Cancer Classification using Genetic Algorithm + SVM

A machine learning pipeline that combines **Genetic Algorithm (GA)** for optimal feature selection and **Support Vector Machine (SVM)** for binary classification of breast cancer (malignant vs benign), achieving **96.49% test accuracy** with only 18 of 30 features.

---

##  Overview

The Breast Cancer Wisconsin dataset has 30 features — not all of which contribute equally to classification. This project uses a **Genetic Algorithm** to evolve the optimal feature subset, reducing model complexity and avoiding overfitting, before training a final SVM classifier.

---

##  Dataset

| Property | Value |
|---|---|
| Source | `sklearn.datasets.load_breast_cancer()` |
| Total Samples | 569 |
| Features | 30 numerical |
| Classes | 0 = Malignant, 1 = Benign |
| Train / Test Split | 70% / 30% |

---

##  Methodology

```
Load Dataset (569 samples, 30 features)
        ↓
  Train / Test Split (70/20)
        ↓
  Genetic Algorithm (DEAP)
  ├── Chromosome: binary vector length 30
  ├── Fitness: 5-fold CV accuracy on SVM
  ├── Selection: Tournament (size=3)
  ├── Crossover: Two-point (cxpb=0.5)
  └── Mutation: Bit flip (mutpb=0.2, indpb=0.05)
        ↓
  Best Chromosome → 18 selected features
        ↓
  SVM (linear kernel, C=0.1)
        ↓
  Evaluate on unseen test set
```

---

##  GA Configuration

| Parameter | Value |
|---|---|
| Population size | 20 |
| Generations | 10 |
| Crossover probability | 0.5 |
| Mutation probability | 0.2 |
| Bit-flip probability | 0.05 |
| Selection | Tournament (size=3) |
| Fitness function | 5-fold CV accuracy |

---

##  Results

**Selected features:** 18 out of 30 (indices: 0, 3, 4, 6, 7, 8, 9, 12, 17, 20, 21, 22, 23, 25, 26, 27, 28, 29)

| Metric | Value |
|---|---|
| Test Accuracy | **96.49%** |
| Cross-Validation Accuracy | 95.43% |

**Classification Report (171 test samples):**

| Class | Precision | Recall | F1-score |
|---|---|---|---|
| Malignant (0) | 0.97 | 0.94 | 0.95 |
| Benign (1) | 0.96 | 0.98 | 0.97 |

---

##  Comparison with Baseline Methods

| Method | Accuracy |
|---|---|
| Decision Tree | ~93% |
| KNN | ~95% |
| SVM (all 30 features) | ~96–97% |
| **GA + SVM (this project)** | **96.49%** |

> GA + SVM matches full-feature SVM while using 40% fewer features — reducing complexity with no accuracy loss.

---

##  Tech Stack

| Tool | Purpose |
|---|---|
| Python | Core language |
| scikit-learn | SVM, cross-validation, metrics |
| DEAP | Genetic Algorithm framework |
| NumPy | Array operations |
| Google Colab | Development environment |

---



##  Future Improvements

- Increase population size and generations for better feature convergence
- Try RBF kernel SVM for non-linear boundaries
- Compare with other wrappers: PSO, ACO, or Bayesian optimization
- Apply SHAP for interpretability of selected features
- Test on other medical datasets (diabetes, heart disease)

---

## 📄 License

This project is for academic and educational purposes. Dataset sourced from `sklearn.datasets` (public domain).
