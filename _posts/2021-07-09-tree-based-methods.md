---
published: false
---

Although typically worse than some other supervised approaches in terms of predictive accuracy, tree-based methods are simple, and useful for interpretation. Combining a large number of trees through methods like _bagging_, _random forest_ and _boosting_ can improve predictive accuracies, but at the expense of some loss in interpretation. 

**Basics of decision trees** \
Decision trees can be applied to both problems involving classification and regression. A decision tree is a data-structure consisting of a hierarchy of nodes. 

* Root Node: has no parent node, gives rise to two children nodes
* Internal Node: has one parent node, gives rise to two children nodes
* Leaf: has one parent node, but no children node --> prediction

Decision trees are linear models that aim to find logical rules that cluster data points into pure subgroups with common output values. With a series of if-else questions about individual features, the model can learn patterns from each feature in a way to produce the purest leaves. The purity, or homogeneity of a cluster can be measured using measures like the Gini index that evaluate impurity. In each iteration, the algorithm tries to find a breakpoint that can split the observation into more homogeneous subgroups. 

*load libraries* \
```{r}
suppressMessages(library(rpart))
suppressMessages(library(tree))
suppressMessages(library(rpart.plot))
suppressMessages(library(mlbench))
suppressMessages(library(DAAG))
suppressMessages(library(lattice))
suppressMessages(library(tidyverse))
suppressMessages(library(ISLR))
suppressMessages(library(rattle))
```
*get the Iris data set*
```{r}
str(iris)
```
*train a decision tree model*
```{r}
iris.tree = rpart(Species ~ Petal.Length + Petal.Width, data = iris)
fancyRpartPlot(iris.tree)
```
