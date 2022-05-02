# Email Analysis
## Data Preprocessing
For each email message, the following features are chosen:
1. sender alias
2. sender user name
3. sender domain
4. subject (Bag-of-Words + tf-idf)
5. body (Bag-of-Words + tf-idf)
6. number of ccs
7. number of urls in subject + body
8. number of attachments

The label is binary: whether the email is read or ignored

## Methodology
First, what are the models we can choose from?
- Non Parametric
    - [x] KNN
- Linear
    - [x] Logistic Regression
    - [x] Naive Bayes
    - [x] LDA (Like Naive Bayes but assumes each p(x|y) follows a normal distribution. Does not have i.i.d assumption)
    - [x] QDA (Like LDA but does not assume k classes share same covariance matrix)
- Non Linear
    - [x] SVM
    - [ ] High-Order Functions, Splines, and GAMs
    - [ ] Tree

Second, what are the available feature selection methods for each model?
- Applicable to Linear:
    - PCA to reduce dimension (in our case features are not quite interpretable. We can try this)
        - With PCA, each principle component is uncorrelated with every other component
    - Partial Least Square (usually works pretty much the same as PCA in practice)
    - Ridge
    - Lasso

Third, what are the hyperparameters of each model?
- KNN
    - n_neighbors (int)
    - weights ("uniform" or "distance")
- Logistic Regression
    - penalty ("l1", "l2", "elasticnet")
    - C (inverse of regularization strength > 0)
    - fit_intercept [True, False]
    - class_weight
    - max_iter
    - warm_start
    use liblinear/saga to first select features (if we don't do PCR)
    for liblinear:
        - dual [True, False]
        - intercept_scaling