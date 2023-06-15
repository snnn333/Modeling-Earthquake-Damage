# [Competition: Richter's Predictor: Modeling Earthquake Damage](https://www.drivendata.org/competitions/57/nepal-earthquake/page/134/)

## Methods
### Data preprocessing
The first step in our analysis was data preprocessing. The dataset contains 41 features, including 1 meaningless feature called building id, 8 categorical features, and 32 numerical features.

**Numerical feature** : Log transformation + StandardScaler
	| Numerical Features |
| ----------- |
| count_floors_pre_eq |
| age |
| area_percentage |
| height_percentage |
| count families |

**Geo level**: Target Encoding
**Categorical feature**:One-Hot Encoding

### PCA
Since our dataset contained up to 81 features after encoding, we explored the use of principal component analysis (PCA) to reduce the dimensionality of the data. PCA is a common technique used to simplify complex data by identifying patterns and relationships between features. After applying PCA, we examined the first 20 features of the first component to determine their importance in predicting building damage levels. However, this process did not result in a significant improvement in accuracy, so we decided to keep all features for the final process.

## Model Selection
**Random Forest** Random forest is commonly used in classification problems, which can be more accurate than decision tree algorithm. Therefore, random forest can be used as a good initialization model. The parameters of our model are as follows.

| Parameters | Value |
| ----------- | ----------- |
| n_estimators | 200 |
| max_depth | 10 |

**XGBoost** XGBoost is a complex model compared to the random forest, and usually performs better than RF when there is a class imbalance.

| Parameters | Value |
| ----------- | ----------- |
| n_estimators | 1000 |
| learning_rate | 0.1 |
| max_depth | 5 |

**LightGBM** For Lgbm, the best hyperparameters were "num_leaves," "learning_rate," "max_depth," "lambda_l2," and "max_bin." By setting "is_unbalance" to "True" to address the imbalanced dataset, we achieved a validation set F1-score of 0.7527 and a training set F1-score of 0.8231.

| Parameters | Value |
| ----------- | ----------- |
| n_estimators | 1400 |
| num_leaves | 230 |
| learning_rate | 0.1 |
| lambda_l2 | 5 |
| max_bin | 90 |
| max_depth | 30 |
| is_unbalance | True |

**CatBoost** For Catboost, the best hyperparameters were "n_estimators," "learning_rate," "l2_leaf_reg," and "max_depth." By setting the hyperparameter "class_weights" to "[1,2,2.5]" to balance the data, we achieved a validation set F1-score of 0.752.

| Parameters | Value |
| ----------- | ----------- |
| n_estimators | 1500 | 
| learning_rate | 0.1 |
| l2_leaf_reg | 10 |
| max_depth | 7 | 
| class_weights | [1,2,2.5] |

**Model Comparison**
| Model | F1-Score |
| ----------- | ----------- |
| Random Forest | 0.7341 |
| XGBoost | 0.7422 |
| LightGBN | 0.7445 |
| CatBoost | 0.7448 |

   
