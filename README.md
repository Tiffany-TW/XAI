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

<a id="math"></a>
**Mathematical Arguments [(Friedman, 2001)](#reference)**
Suppose $D$ is the training data with n variables. Let $X$ be a set composed of the n variables in the training data, ie. $\{x_1, x_2, ..., x_n\}$. Assume that $z_l\subset X$, and $z_l \cup z_l^c = X$. Note that $z_l^c$ is the complement set of $z_l$. Given the approximation function $\hat{F}(X)$, we have $$\bar{F}_{z_l^c}(z_l)=E_{z_l^c}[\hat{F}(X)]=\int\hat{F}(X)p_{z_l^c}(z_l^c)dz_l^c,$$ and $\bar{F}_{z_l^c}(z_l)$ is a function of $z_l$. That is, given the value of $z_l$, $\bar{F}_{z_l^c}(z_l)$ is the expected value of the approximation over entire domain of $z_l^c$.
For the training set $D$, the values of the variables of $D$ are discrete. Thus, $p_{z_l^c}(z_l^c)$  can be estimated by the training data. Since the notion of probability mass function is the same as frequency, $\bar{F}_{z_l^c}(z_l)$ is thus defined as $$\frac{1}{N}\sum_{i=1}^N\hat{F}(z_l, z^c_{i, l}),$$ with $N$ instances in $D$. Finally, PDP is plotted as a graph of the value of $\bar{F}_{z_l^c}(z_l)$ against each corresponding value of $z_l$.

**Features**
* PDP is most suitable when $\hat{F}(X)$ is dominated by low-order interactions.
    * This statement is derived from the equation $$\bar{F}_{z_l^c}(z_l)=E_{z_l^c}[\hat{F}(X)]=\int\hat{F}(X)p_{z_l^c}(z_l^c)dz_l^c.$$ If interactions among varaibles of $z_l$ and $z_l^c$ exist, then $\bar{F}_{z_l^c}(z_l)$ may not reflect the underlying association.
* PDP is time-consuming for large data sets. PDP presents the dependency of variables to the approximation by a series of graphs that plot the approximation function against each corresponding value of a small subset of varaibles (a target variable subset contains at most two variables). 

**Examples**
Let us assume that the training set $D$ contains four instances, which is shown as the following table:
|index|$v_1$|$v_2$|
|----|----|----|
|1|0|1|
|2|1|1|
|3|0|1|
|4|1|0|

Suppose that $z_l$ = {$v_1$}.
According to [Mathematical Arguments](#math), $\bar{F_{z_l^c}}(z_l)$ is computed by substituting the value of $v_2$ into the approximation function $\hat{F}(v_1, v_{i, 2}).$ As a result, when $v_1=0$, $$\bar{F_{z_l^c}}(0) = \frac{1}{4}(\hat{F}(0,1)+\hat{F}(0,1)+\hat{F}(0,1)+\hat{F}(0,0))$$ $$=\frac{3}{4}\hat{F}(0,1)+\frac{1}{4}\hat{F}(0,0)$$$$=p_{v_2}(1)\hat{F}(0,1)+p_{v_2}(0)\hat{F}(0,0).$$ The result is similar when $v_1=1.$

**Implementation**
#### Individual Conditional Expectations
#### Accumulated Local Effects
#### LIME
#### Shapley Values
## Reference
1. Ali, S., Abuhmed, T., El-Sappagh, S., Muhammad, K., Alonso-Moral, J. M., Confalonieri, R., Guidotti, R., Del Ser, J., Díaz-Rodríguez, N., & Herrera, F. (2023). Explainable Artificial Intelligence (XAI): What we know and what is left to attain Trustworthy Artificial Intelligence. Information Fusion, 99, 101805. https://doi.org/10.1016/j.inffus.2023.101805
2. Retzlaff, C. O., Angerschmid, A., Saranti, A., Schneeberger, D., Röttger, R., Müller, H., & Holzinger, A. (2024). Post-hoc vs ante-hoc explanations: xAI design guidelines for data scientists. Cognitive Systems Research, 86, 101243. https://doi.org/10.1016/j.cogsys.2024.101243
3. Friedman, J. H. (2001). Greedy function approximation: A gradient boosting machine. The Annals of Statistics, 29(5). https://doi.org/10.1214/aos/1013203451

