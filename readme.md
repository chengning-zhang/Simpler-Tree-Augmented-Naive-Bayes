# Simpler TAN + Ensemble TAN


A custom implementation of Bayesian network written from scratch in Python 3, API inspired by SciKit-learn. 
This module implements 4 Bayesian classifiers: 
* [Naive Bayes(NB)](https://scikit-learn.org/stable/modules/naive_bayes.html)
* [Tree-Augmented Naive Bayes(TAN)](http://www.cs.technion.ac.il/~dang/journal_papers/friedman1997Bayesian.pdf)
* [Simpler TAN(STAN)](https://github.com/chengning-zhang/Simple-TAN-and-Ensemble-TAN)
* [Ensemble TAN(ETAN)](https://github.com/chengning-zhang/Simple-TAN-and-Ensemble-TAN)

Note that Naive Bayes has been incorporated into Sklearn module, while Tree-augmented Naive bayes not. 
Our Naive Bayes classifier is same as sklearn.naive_bayes.CategoricalNB, which requires all features be categorical.

## Current features

### Tree-Based Structure Learning
- Naive Bayes - Tree-Augmented Naive Bayes - Chow-Liu
- Simpler TAN - Ensemble TAN - Chengning Zhang

### Multi-class Classification
- Naive Bayes - Tree-Augmented Naive Bayes - 
- Simpler TAN - Ensemble TAN -

### Network Visualization
- Naive Bayes - Tree-Augmented Naive Bayes - 
- Simpler TAN - Ensemble TAN -


### Cross Validation/Model Selection
- Stratified K-fold CV-
- K fold CV-
- Accuracy, Recall, Precision, Conditional log likelihood-

### SHAP 
- Feature importance scores-
- Kernel Explaner-


## Using classifiers

Toy example on Naive Bayes

```javascript
import numpy as np
Y = np.array([1, 1, 1, 2, 2, 2])
X = np.array([[-1, -1], [-2, -1], [-3, -2], [1, 1], [2, 1], [3, 2]])
import NB
nb = NB(alpha = 1)
nb.fit(X,y)
nb.get_params()
nb.classes_
print(nb.name)
print(nb.predict_proba(X))
nb.score(X,y)
```

Toy example on Ensemble TAN

```javascript
import numpy as np
Y = np.array([1, 1, 1, 2, 2, 2])
X = np.array([[-1, -1], [-2, -1], [-3, -2], [1, 1], [2, 1], [3, 2]])
import STAN_TAN_bagging
stan_tan_bag = STAN_TAN_bagging(alpha = 1)
stan_tan_bag.fit(X,y,M)
stan_tan_bag.get_params()
stan_tan_bag.classes_
print(stan_tan_bag.name)
print(stan_tan_bag.predict_proba(X))
stan_tan_bag.score(X,y)
```

## Model Selection(Hyper-parameter tuning)
One can choose the best smoothing parameter.

```javascript
import warnings
warnings.filterwarnings("ignore")
from sklearn.model_selection import GridSearchCV
from sklearn.metrics import make_scorer
import pandas as pd
stan = STAN()
stan.get_params()
parameters = {'alpha':[1,2,3]}#,'starting_node':[0,1,2]}
"""scorers = {
    'precision_score': make_scorer(precision_score),
    'recall_score': make_scorer(recall_score),
    'accuracy_score': make_scorer(accuracy_score)#,
    #'Conditional log likelihood': make_scorer(nb.Conditional_log_likelihood_general,C)
}"""
clf = GridSearchCV(stan, parameters,cv =10)

clf.fit(X,y,M = M) 
pd.DataFrame(clf.cv_results_)
```




## Get cross validation


```javascript
import get_cv

Y = np.array([1, 1, 1, 2, 2, 2])
X = np.array([[-1, -1], [-2, -1], [-3, -2], [1, 1], [2, 1], [3, 2]])
Accuracy, CLL, training_time,Precision,Recall= get_cv(NB,X,y,M = None)
print(np.mean(Accuracy))
print(np.mean(CLL))
print(np.mean(Precision))
print(np.mean(Recall))
print(np.mean(np.array(training_time)))

```


## Plot the tree-structure
```javascript
stan0 = STAN(starting_node = 0)
stan0.fit(X,y,M)
stan0.plot_tree_structure()

```
![](/images/tree_plot.png)


## Model explanation using SHAP

```javascript
nb = NB()
nb.fit(lactamase)
explainer1 = shap.KernelExplainer(nb.predict_binary, X2[0:50,], link="logit")
shap_values1 = explainer1.shap_values(X2,nsamples = 20)

shap.summary_plot(shap_values1, X2)
shap.summary_plot(shap_values1, X2, plot_type="bar")

```

![](images/P450_STAN_shap.png)



## Built With

* [Dropwizard](https://scikit-learn.org/stable/modules/classes.html) - scikit-learn API
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds


## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Chengning Zhang** - *Initial work* - [Simpler TAN + Ensemble TAN](https://github.com/chengning-zhang/Simple-TAN-and-Ensemble-TAN)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc
