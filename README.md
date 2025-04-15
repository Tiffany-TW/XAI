# XAI
This repository contains concepts and implementations of methods in the field of XAI. 

## XAI Taxanomy
The three dimensions of XAI taxanomy are **data explainability**, **model explainability**, and **post-hoc explainability** [(Ali et al., 2023)](#reference). Each dimension includes various explainability approaches, which will be introduced in the following sections.

### Data explainability
### Model explainability
### Post-hoc explainability approaches
Post-hoc explainability approaches elucidates the outcomes of a model. Understanding the contribution of features to the model's predictions is crucial for gaining insights into the model's decision-making process [(Retzlaff et al., 2024)](#reference). The following introduces classic post-hoc explainability approaches using visualization, attribution and game-theoretic methods.  
#### Partial Dependence Plot
**Introduction**
Partial dependence plot (PDP) provides visualization of the dependency of target variables to a machine learning model approximation. The level of dependency is characterized by the behavior of the partial dependency plot. The flatter the plot is, the more independent the target variables are to the approximation.

**Mathematical Arguments**
Suppose $D$ is the training data with n variables. Let $X$ be a set composed of the n variables in the training data, ie. $\{x_1, x_2, ..., x_n\}$. Assume that $z_l\subset X$, and $z_l \cup z_l^c = X$. Note that $z_l^c$ is the complement set of $z_l$. Given the approximation function $\hat{F}(X)$, we have $\bar{F}_{z_l^c}(z_l)=E_{z_l^c}[\hat{F}(X)]=\int\hat{F}(X)p_{z_l^c}(z_l^c)dz_l^c$. $\bar{F}_{z_l^c}(z_l)$ is a function of $z_l$. That is, given the value of $z_l$, $\bar{F}_{z_l^c}(z_l)$ is the expected value of the approximation over all $z_l^c$. Because the values of the variables of $D$ are discrete, $p_{z_l^c}(z_l^c)$  can be estimated by the training data. Moreover, since probability mass function can be interpreted as frequency, $\bar{F}_{z_l^c}(z_l)$ can be defined as $\frac{1}{N}\sum_{i=1}^N\hat{F}(z_l, z^c_{i, l})$, where there are $N$ instances in $D$.

**Limitations**
**Examples**
**Implementation**
#### Accumulated Local Effects
#### Individual Conditional Expectations
#### LIME
#### Shapley Values
## Reference
1. Ali, S., Abuhmed, T., El-Sappagh, S., Muhammad, K., Alonso-Moral, J. M., Confalonieri, R., Guidotti, R., Del Ser, J., Díaz-Rodríguez, N., & Herrera, F. (2023). Explainable Artificial Intelligence (XAI): What we know and what is left to attain Trustworthy Artificial Intelligence. Information Fusion, 99, 101805. https://doi.org/10.1016/j.inffus.2023.101805
2. Retzlaff, C. O., Angerschmid, A., Saranti, A., Schneeberger, D., Röttger, R., Müller, H., & Holzinger, A. (2024). Post-hoc vs ante-hoc explanations: xAI design guidelines for data scientists. Cognitive Systems Research, 86, 101243. https://doi.org/10.1016/j.cogsys.2024.101243

