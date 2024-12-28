# Machine Learning Fundamentals Reference Sheet

## Types of Machine Learning

### Supervised Learning
1. **Classification**
   - Binary classification
   - Multi-class classification
   - Multi-label classification
   Examples:
   ```
   Binary: Spam Detection (0/1)
   Multi-class: Image Classification (Cat/Dog/Bird)
   Multi-label: Movie Genre Classification
   ```

2. **Regression**
   - Linear regression
   - Polynomial regression
   - Multiple regression
   Examples:
   ```
   House price prediction
   Stock price forecasting
   Temperature prediction
   ```

### Unsupervised Learning
1. **Clustering**
   - K-means
   - Hierarchical clustering
   - DBSCAN
   - Gaussian Mixture Models

2. **Dimensionality Reduction**
   - Principal Component Analysis (PCA)
   - t-SNE
   - UMAP
   - Autoencoders

### Semi-Supervised Learning
- Combination of labeled and unlabeled data
- Self-training
- Co-training
- Label propagation

### Reinforcement Learning
- Agent-environment interaction
- State-action pairs
- Rewards and penalties
- Policy optimization

## Data Preprocessing

### Feature Engineering
1. **Numerical Features**
   ```
   Scaling methods:
   - Min-Max scaling: (x - min)/(max - min)
   - Standard scaling: (x - μ)/σ
   - Robust scaling: (x - median)/(Q₃ - Q₁)
   ```

2. **Categorical Features**
   ```
   Encoding methods:
   - One-hot encoding
   - Label encoding
   - Ordinal encoding
   - Target encoding
   ```

3. **Text Features**
   ```
   - Bag of words
   - TF-IDF
   - Word embeddings
   - N-grams
   ```

### Missing Data
1. **Detection**
   ```
   - Null values
   - NaN
   - Missing indicators
   ```

2. **Handling Methods**
   ```
   - Mean/median imputation
   - Mode imputation
   - Forward/backward fill
   - Model-based imputation
   ```

### Feature Selection
1. **Filter Methods**
   ```
   - Correlation analysis
   - Chi-square test
   - Information gain
   - Variance threshold
   ```

2. **Wrapper Methods**
   ```
   - Recursive feature elimination
   - Forward selection
   - Backward elimination
   ```

3. **Embedded Methods**
   ```
   - Lasso regularization
   - Ridge regularization
   - Random forest importance
   ```

## Model Evaluation

### Performance Metrics
1. **Classification**
   ```
   Accuracy = (TP + TN)/(TP + TN + FP + FN)
   Precision = TP/(TP + FP)
   Recall = TP/(TP + FN)
   F1-Score = 2 × (Precision × Recall)/(Precision + Recall)
   ROC-AUC = Area under ROC curve
   ```

2. **Regression**
   ```
   MAE = (1/n)Σ|yᵢ - ŷᵢ|
   MSE = (1/n)Σ(yᵢ - ŷᵢ)²
   RMSE = √MSE
   R² = 1 - (SSres/SStot)
   ```

### Cross-Validation
1. **K-Fold**
   ```
   Split data into k folds
   Train on k-1 folds
   Test on remaining fold
   Rotate k times
   ```

2. **Stratified K-Fold**
   ```
   Maintains class distribution
   Used for imbalanced datasets
   ```

3. **Time Series CV**
   ```
   Forward chaining
   Rolling window
   ```

### Bias-Variance Tradeoff
1. **Components**
   ```
   Error = Bias² + Variance + Irreducible Error
   ```

2. **Characteristics**
   ```
   High Bias: Underfitting
   High Variance: Overfitting
   Optimal: Balance between bias and variance
   ```

## Common Algorithms

### Linear Models
1. **Linear Regression**
   ```
   y = wx + b
   Loss = MSE = (1/n)Σ(y - ŷ)²
   ```

2. **Logistic Regression**
   ```
   p(y=1) = 1/(1 + e^(-wx - b))
   Loss = -Σ(y log(p) + (1-y)log(1-p))
   ```

### Decision Trees
1. **Split Criteria**
   ```
   Gini impurity = Σp(1-p)
   Entropy = -Σp log₂(p)
   MSE for regression
   ```

2. **Pruning**
   ```
   Pre-pruning: Early stopping
   Post-pruning: Cost complexity
   ```

### Ensemble Methods
1. **Random Forest**
   ```
   Bagging + Random feature selection
   Multiple trees
   Majority vote/Average
   ```

2. **Gradient Boosting**
   ```
   Sequential tree building
   Learning from residuals
   Examples: XGBoost, LightGBM
   ```

### Support Vector Machines
1. **Linear SVM**
   ```
   Maximize margin between classes
   w·x + b = 0 (decision boundary)
   ```

2. **Kernel SVM**
   ```
   Kernel functions:
   - RBF: exp(-γ||x-y||²)
   - Polynomial: (γx·y + r)ᵈ
   ```

## Model Optimization

### Hyperparameter Tuning
1. **Grid Search**
   ```
   Exhaustive search
   Parameter combinations
   Cross-validation
   ```

2. **Random Search**
   ```
   Random parameter sampling
   Often more efficient than grid search
   ```

3. **Bayesian Optimization**
   ```
   Sequential optimization
   Probabilistic model
   Acquisition function
   ```

### Regularization
1. **L1 (Lasso)**
   ```
   Penalty = λΣ|wᵢ|
   Feature selection
   Sparse solutions
   ```

2. **L2 (Ridge)**
   ```
   Penalty = λΣwᵢ²
   Weight decay
   No feature selection
   ```

3. **Elastic Net**
   ```
   Combination of L1 and L2
   Penalty = λ₁Σ|wᵢ| + λ₂Σwᵢ²
   ```

## Best Practices

### Data Splitting
```
Training set: 60-80%
Validation set: 10-20%
Test set: 10-20%
```

### Model Selection
1. **Considerations**
   ```
   - Dataset size
   - Feature types
   - Problem complexity
   - Interpretability needs
   - Computational resources
   ```

2. **Validation Strategy**
   ```
   - Hold-out validation
   - Cross-validation
   - Nested cross-validation
   ```

### Pipeline Design
1. **Components**
   ```
   1. Data preprocessing
   2. Feature engineering
   3. Model training
   4. Model evaluation
   5. Model deployment
   ```

2. **Best Practices**
   ```
   - Reproducibility
   - Modularity
   - Scalability
   - Version control
   - Documentation
   ```

## Common Issues

### Class Imbalance
1. **Detection**
   ```
   Class ratio analysis
   Performance metrics per class
   ```

2. **Solutions**
   ```
   - Oversampling (SMOTE)
   - Undersampling
   - Class weights
   - Ensemble methods
   ```

### Overfitting/Underfitting
1. **Detection**
   ```
   Training vs. validation curves
   Learning curves
   ```

2. **Solutions**
   ```
   Overfitting:
   - More data
   - Regularization
   - Dropout
   - Early stopping

   Underfitting:
   - More complex model
   - Feature engineering
   - Longer training
   ```

### Feature Engineering Challenges
1. **High Cardinality**
   ```
   - Feature hashing
   - Target encoding
   - Dimensionality reduction
   ```

2. **Missing Data**
   ```
   - MCAR analysis
   - MAR analysis
   - Multiple imputation
   ```
