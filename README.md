
# Nutri-Score Decision Modeling Project

## Project Overview

This project explores various decision modeling approaches for classifying food products according to the Nutri-Score label system. We implement and compare Multi-Criteria Decision Analysis (MCDA) methods and Machine Learning algorithms to understand and potentially improve nutritional labeling systems.


<img width="487" height="66" alt="Screenshot 2025-10-23 at 11 30 57 PM" src="https://github.com/user-attachments/assets/83944c3f-251d-48ce-abd4-e6cedfed10ae" />



## Team Members
- Melissa Medjahed
- Sihem Boutebal  
- Dilbar Isakova

## Objectives

1. **Build a comprehensive database** of 200+ food products with their Nutri-Score and Eco-Score labels
2. **Develop and test decision models** using ELECTRE-TRI sorting methods
3. **Implement machine learning approaches** for Nutri-Score prediction
4. **Compare model performance** against actual Nutri-Score classifications
5. **Combine Nutri-Score and Eco-Score** in unified decision models

## Repository Structure

```
Nutri-Score-Decision-Modeling/
│
├── 📂 problem_statement/
│   ├── import_dataset.ipynb         # Data import and preprocessing
│   └── limiting_profiles_uta.json   # UTA approach limiting profiles
│
├── 📂 visuals/
│   └── (visualization notebooks)
│
├── 📊 data-nutri-score-project.xlsx # Main database (943 food products)
├── 📈 predictions.csv                # Model predictions output
│
├── 🔧 MCDA Models/
│   ├── MCDA_Nutri-Score_Eco-Score.ipynb  # Combined scoring model
│   ├── MCDA_Pessimistic_Optimistic.ipynb # ELECTRE-TRI implementation
│   └── Comparing_with_other_groups.ipynb  # Cross-validation with other groups
│
├── 🤖 Machine Learning/
│   ├── Machine_learning_approach.ipynb    # ML models implementation
│   └── UTA_approach.ipynb                # UTA method
│
└── README.md                         # This file
```

## Methodology

### 1. Database Creation
- **Source**: [Open Food Facts](https://fr-en.openfoodfacts.org/)
- **Categories**: Breakfast cereals, Snacks, Cookies, Industrial ready-made dishes, Beverages, Dairy products
- **Size**: 943 food products with complete nutritional information
- **Features**: 7 nutritional criteria + Nutri-Score + Eco-Score

### 2. MCDA Approaches

#### Pessimistic Majority Sorting (ELECTRE-TRI-pc)
- Implements pessimistic assignment rule
- Tests with multiple λ thresholds (0.5, 0.6, 0.7)
- Two profile definition methods:
  - Manual setting based on domain expertise
  - Quintile-based automatic segmentation

#### Optimistic Majority Sorting (ELECTRE-TRI-pd)
- Implements optimistic assignment rule
- Enhanced with K-means clustering for profile determination
- Provides data-driven limiting profiles

### 3. Machine Learning Models

#### Decision Tree
- **Accuracy**: 81.3%
- Strong performance for categories A and C
- Interpretable decision rules

#### XGBoost
- **Accuracy**: 89.0%
- Best overall performance
- Balanced predictions across all categories

## Results Summary

| Model | Accuracy | Key Strengths | Limitations |
|-------|----------|--------------|-------------|
| Pessimistic Manual (λ=0.6) | ~60% | Good for category A | Poor for categories D, E |
| Pessimistic Quintile (λ=0.5) | ~45% | Balanced approach | Low overall accuracy |
| Optimistic Clustering (λ=0.6) | ~50% | Data-driven profiles | Tends to predict category A |
| Decision Tree | 81.3% | Interpretable, balanced | Struggles with category E |
| XGBoost | 89.0% | Best accuracy, robust | Less interpretable | 

## Getting Started

### Prerequisites
```python
pandas>=1.3.0
numpy>=1.21.0
scikit-learn>=0.24.0
xgboost>=1.5.0
jupyter>=1.0.0
openpyxl>=3.0.0
matplotlib>=3.4.0
seaborn>=0.11.0
```

### Installation
```bash
# Clone the repository
git clone https://github.com/isakovaad/Nutri-Score-Decision-Modeling.git

# Navigate to project directory
cd Nutri-Score-Decision-Modeling

# Install dependencies
pip install -r requirements.txt
```

### Usage

1. **Data Exploration**:
```python
# Load and explore the database
jupyter notebook import_dataset.ipynb
```

2. **Run MCDA Models**:
```python
# Execute ELECTRE-TRI methods
jupyter notebook MCDA_Pessimistic_Optimistic.ipynb
```

3. **Train ML Models**:
```python
# Train and evaluate machine learning models
jupyter notebook Machine_learning_approach.ipynb
```

## Key Features

- **Multi-method comparison**: MCDA vs ML approaches
- **Flexible weight configurations**: Test different criterion importance
- **Clustering-based profile generation**: Data-driven category boundaries
- **Cross-group validation**: Compare results with other research groups
- **Eco-Score integration**: Combined environmental and nutritional scoring

## Criteria and Weights

| Criterion | Weight | Type |
|-----------|--------|------|
| Energy (KJ) | 4 | Minimize |
| Sugars (g) | 3 | Minimize |
| Saturated Fat (g) | 3 | Minimize |
| Salt (g) | 3 | Minimize |
| Proteins (g) | 2 | Maximize |
| Fiber (g) | 2 | Maximize |
| Fruits/Vegetables (%) | 1 | Maximize | 

## Key Findings

1. **Machine Learning superiority**: XGBoost achieves 89% accuracy, significantly outperforming MCDA methods
2. **Profile sensitivity**: Manual profile setting shows strong bias toward category A
3. **Data-driven benefits**: K-means clustering provides more balanced category distributions
4. **Category imbalance**: All models struggle with category E due to limited samples
5. **Interpretability trade-off**: MCDA methods offer better explainability despite lower accuracy

## References

- Roy, B. & Bouyssou, D. (1993). *Aide multicritère à la décision: Méthodes et Cas*. Economica.
- Almeida-Dias, J., Figueira, J.R., & Roy, B. (2010). ELECTRE TRI-C: A multiple criteria sorting method based on characteristic reference actions. *European Journal of Operational Research*, 204(3), 565-580.
