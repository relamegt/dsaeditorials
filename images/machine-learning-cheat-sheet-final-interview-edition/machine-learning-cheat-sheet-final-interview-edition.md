# Machine Learning Cheat Sheet — Final Interview Edition

A complete, publish-ready reference covering ML fundamentals with full forms and clear working explanations, matching the structure of your OS, CN, and DBMS sheets.

## 1. Basic Terminology

| Term | Full Form / Meaning |
| --- | --- |
| ML | Machine Learning — subset of AI where systems learn patterns from data instead of explicit programming |
| AI | Artificial Intelligence |
| DL | Deep Learning — ML using multi-layer neural networks |
| ANN | Artificial Neural Network |
| CNN | Convolutional Neural Network — for image data |
| RNN | Recurrent Neural Network — for sequential data |
| LSTM | Long Short-Term Memory — RNN variant that handles long sequences |
| SVM | Support Vector Machine |
| KNN | K-Nearest Neighbors |
| PCA | Principal Component Analysis |
| NLP | Natural Language Processing |

## 2. Types of Machine Learning

- **Supervised Learning** — How it works: the model is trained on labeled data (input-output pairs); it learns a mapping function by comparing its predictions to the true labels and adjusting itself to minimize error. Used for regression and classification.
- **Unsupervised Learning** — How it works: the model is given only unlabeled data and must find hidden structure or patterns on its own (e.g., grouping similar points together). Used for clustering and dimensionality reduction.
- **Reinforcement Learning** — How it works: an agent takes actions in an environment and receives rewards or penalties as feedback; it learns a policy that maximizes cumulative reward through trial and error over time.

## 3. Regression vs Classification

- **Regression**: predicts a continuous numeric value (e.g., house price).
- **Classification**: predicts a discrete category/class (e.g., spam or not spam).

## 4. Linear Regression — How It Works

**How it works**: Finds a straight-line equation \(y = mx + c\) that best fits the data by minimizing the sum of squared differences between predicted and actual values (least squares method). The model is trained using Gradient Descent, which iteratively adjusts the slope and intercept to reduce the cost function.

- Pros: simple, interpretable, fast to train.
- Cons: sensitive to outliers, assumes a linear relationship between variables.

## 5. Logistic Regression — How It Works

**How it works**: Despite the name, it's used for binary classification. It applies a linear combination of inputs to a **sigmoid function**, which squashes the output into a probability between 0 and 1; if the probability exceeds a threshold (usually 0.5), the input is classified into one class, otherwise the other.
Trait: Used for binary classification; predicts probability rather than a direct value.

## 6. Decision Trees — How They Work

**How it works**: The algorithm repeatedly splits the dataset into branches based on the feature that best separates the classes at each step. It picks the best split using a purity measure:

- **Gini Impurity**: measures how mixed the classes are in a node; lower is purer.
- **Entropy**: measures disorder/randomness in a node using information theory; the split that reduces entropy the most (highest "information gain") is chosen.

Trait: Easy to interpret and visualize, but prone to overfitting on training data if grown too deep.

## 7. Random Forest — How It Works

**How it works**: Builds many individual decision trees, each trained on a random subset of the data and features (this is called **bagging** — Bootstrap Aggregating). For classification, the final prediction is the majority vote across all trees; for regression, it's the average.
Trait: More accurate and robust than a single decision tree because averaging reduces overfitting/variance.

## 8. Gradient Boosting / XGBoost — How They Work

**How it works**: Builds trees **sequentially** (unlike Random Forest's parallel trees) — each new tree is trained specifically to correct the errors (residuals) made by the previous trees, gradually improving overall accuracy. **XGBoost** (Extreme Gradient Boosting) is an optimized, faster implementation of this idea with regularization built in to prevent overfitting.
Trait: Very high accuracy on structured/tabular data, but more prone to overfitting and slower to train than Random Forest if not tuned carefully.

## 9. Bagging vs Boosting

| Aspect | Bagging | Boosting |
| --- | --- | --- |
| Training | Parallel — trees trained independently | Sequential — each tree learns from previous errors |
| Goal | Reduce variance | Reduce bias |
| Example | Random Forest | XGBoost, AdaBoost, Gradient Boosting |

## 10. K-Nearest Neighbors (KNN) — How It Works

**How it works**: To classify a new data point, KNN looks at the "k" closest points in the training data (using a distance metric like Euclidean distance) and assigns the class that is most common among those neighbors (majority vote). For regression, it averages their values.
Trait: Simple, no training phase needed, but slow at prediction time on large datasets and sensitive to feature scaling.

## 11. Support Vector Machine (SVM) — How It Works

**How it works**: Finds the optimal hyperplane that separates classes with the **maximum margin** (largest possible distance to the nearest data points of each class, called support vectors). For data that isn't linearly separable, SVM uses the **kernel trick** to project data into a higher dimension where a linear separator becomes possible.
Trait: Effective in high-dimensional spaces, but computationally expensive on large datasets.

## 12. Naive Bayes — How It Works

**How it works**: Applies Bayes' Theorem to calculate the probability of each class given the input features, assuming all features are independent of each other (the "naive" assumption). The class with the highest posterior probability is chosen.
Trait: Fast and works well for text classification (e.g., spam detection), despite its simplifying independence assumption often being unrealistic.

## 13. K-Means Clustering — How It Works

**How it works**:

1. Randomly initialize "k" cluster centers (centroids).
2. Assign each data point to its nearest centroid.
3. Recalculate each centroid as the mean of all points assigned to it.
4. Repeat steps 2–3 until centroids stop moving significantly.

**Elbow Method**: Used to choose the optimal value of k — plot the within-cluster sum of squares (WCSS) against different k values; the point where the decrease sharply slows (forming an "elbow") is the best k.

## 14. Hierarchical & DBSCAN Clustering

- **Hierarchical Clustering**: How it works — builds a tree of clusters (dendrogram) by either progressively merging the closest pairs of points/clusters (agglomerative) or splitting one big cluster into smaller ones (divisive); no need to predefine k.
- **DBSCAN (Density-Based Spatial Clustering)**: How it works — groups points that are closely packed together (dense regions), marking points in sparse regions as outliers/noise. Doesn't require specifying the number of clusters in advance and can find irregularly shaped clusters.

## 15. PCA — Dimensionality Reduction

**How it works**: Identifies the directions (principal components) in the data along which variance is maximized, then projects the data onto a smaller number of these components — reducing dimensions while preserving as much information as possible. Useful for speeding up training and visualizing high-dimensional data.
PCA creates new reduced features (a transformation), unlike Feature Selection which just picks the best existing ones.

## 16. Bias-Variance Tradeoff

- **Bias**: error from overly simplistic assumptions — causes **underfitting** (model too simple to capture patterns).
- **Variance**: error from being overly sensitive to training data fluctuations — causes **overfitting** (model memorizes training data, fails on new data).
- **Goal**: find the balance point where both bias and variance are minimized, giving the best generalization to unseen data.

## 17. Overfitting vs Underfitting — Fixes

| Problem | Fix |
| --- | --- |
| Overfitting | Cross-validation, regularization, dropout (in NN), pruning (in trees), more training data |
| Underfitting | Use a more complex model, add more relevant features, reduce regularization |

## 18. Regularization — How It Works

**How it works**: Adds a penalty term to the loss function based on the magnitude of model coefficients, discouraging the model from becoming too complex and overfitting.

- **L1 (Lasso)**: penalty = sum of absolute values of coefficients; can shrink some coefficients to exactly zero, effectively performing feature selection.
- **L2 (Ridge)**: penalty = sum of squared coefficients; shrinks coefficients toward zero but rarely to exactly zero.

## 19. Gradient Descent — How It Works

**How it works**: An optimization algorithm that minimizes the cost function by repeatedly calculating the gradient (slope) of the cost function with respect to each model parameter, then adjusting the parameters a small step in the opposite direction of the gradient (downhill), until it converges to a minimum.

| Variant | How It Differs |
| --- | --- |
| Batch Gradient Descent | Uses the entire dataset for each update step — accurate but slow |
| Stochastic Gradient Descent (SGD) | Uses just one random sample per update — fast but noisy |
| Mini-Batch Gradient Descent | Uses small batches per update — balances speed and stability |

## 20. Feature Engineering & Preprocessing

- **Feature Scaling**: Rescales features to a similar range; important for distance-based (KNN, SVM) and gradient-based (Gradient Descent) algorithms since large-scale features would otherwise dominate.
- **Normalization**: rescales values to a fixed range like .
- **Standardization**: rescales values to have mean 0 and standard deviation 1.
- **Encoding Categorical Variables**:
- **Label Encoding**: assigns each category an integer (e.g., Male=0, Female=1).
- **One-Hot Encoding**: creates a separate binary column per category (e.g., Male=, Female=) — avoids implying false ordinal relationships.
- **Handling Missing Values**: drop rows/columns, fill with mean/median/mode, or use model-based imputation like KNN Imputer.
- **Imbalanced Data**: when one class vastly outnumbers another.
- **Oversampling** (e.g., SMOTE): duplicate/synthesize minority class samples.
- **Undersampling**: remove majority class samples.
- **Class Weights**: penalize misclassifying the minority class more heavily during training.

## 21. Model Evaluation — Classification

**Confusion Matrix**: a table showing True Positives (TP), False Positives (FP), True Negatives (TN), False Negatives (FN) — the foundation for most classification metrics.

| Metric | Formula | Meaning |
| --- | --- | --- |
| Accuracy | (TP+TN)/(TP+TN+FP+FN) | Overall correctness |
| Precision | TP/(TP+FP) | Of predicted positives, how many were correct |
| Recall (Sensitivity) | TP/(TP+FN) | Of actual positives, how many were caught |
| F1-Score | 2×(Precision×Recall)/(Precision+Recall) | Harmonic balance of precision and recall |

**ROC-AUC Curve**: plots True Positive Rate vs False Positive Rate at different thresholds; AUC (Area Under Curve) closer to 1 indicates a better-performing classifier.

## 22. Model Evaluation — Regression

| Metric | Formula | Meaning |
| --- | --- | --- |
| MSE | \(\frac{1}{n}\sum(y_i-\hat{y}_i)^2\) | Average squared error; penalizes large errors more |
| MAE | \(\frac{1}{n}\sum\lvert y_i-\hat{y}_i\rvert\) | Average absolute error; more robust to outliers |
| RMSE | \(\sqrt{MSE}\) | Same units as the target variable |
| R² | \(1 - \frac{\sum(y_i-\hat{y}_i)^2}{\sum(y_i-\bar{y})^2}\) | Percentage of variance explained by the model; R²=0 means the model doesn't fit at all |

## 23. Cross-Validation

**How it works**: Splits the dataset into multiple "folds" (commonly k=5 or 10); the model trains on all folds except one, tests on the held-out fold, and this repeats until every fold has served as the test set once. The average performance across folds gives a more reliable estimate of generalization than a single train-test split.

## 24. Loss Functions

- **Cross-Entropy Loss**: measures how well a classification model's predicted probability distribution matches the true labels; formula \(L = y\log(p) + (1-y)\log(1-p)\) for binary classification.
- **Hinge Loss**: used in SVM; penalizes predictions that are on the wrong side of the margin, formula \(L = \max(0, 1-y\hat{y})\).

## 25. Neural Networks Basics

- **ANN (Artificial Neural Network)**: layers of interconnected "neurons," each applying weights, a bias, and an activation function to inputs before passing output to the next layer.
- **Activation Functions**: introduce non-linearity so the network can learn complex patterns.
- **ReLU**: outputs the input if positive, else zero — fast and widely used.
- **Sigmoid**: squashes output between 0 and 1 — used for binary outputs.
- **Tanh**: squashes output between -1 and 1.
- **Backpropagation**: How it works — after a forward pass produces a prediction, the error is calculated and propagated backward through the network, computing gradients layer by layer via the chain rule, which are then used to update weights via gradient descent.
- **CNN**: uses convolutional filters to detect spatial patterns (edges, textures) in images, mainly for computer vision tasks.
- **RNN/LSTM**: process sequential data by maintaining a "memory" of previous inputs; LSTM adds gating mechanisms to better retain long-term dependencies compared to plain RNNs.

## 26. Quick Interview Traps

- Bagging reduces variance (parallel trees); Boosting reduces bias (sequential trees).
- L1 (Lasso) can zero out coefficients (feature selection); L2 (Ridge) shrinks but rarely zeros them.
- Decision Tree overfits easily; Random Forest reduces this via averaging multiple trees.
- PCA creates new transformed features; Feature Selection picks from existing features.
- High bias = underfitting; high variance = overfitting — the tradeoff is central to model selection.
- Precision matters more when false positives are costly; Recall matters more when false negatives are costly.
- KNN and SVM require feature scaling since they rely on distance calculations; tree-based models generally don't.

