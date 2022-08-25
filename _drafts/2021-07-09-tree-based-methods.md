---
published: true
---
<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
  });
</script>

Although typically worse than some other supervised approaches in terms of predictive accuracy, tree-based methods are simple, and useful for interpretation. Combining a large number of trees through methods like _bagging_, _random forest_ and _boosting_ can improve predictive accuracies, but at the expense of some loss in interpretation. 

**Basics of decision trees**
Decision trees can be applied to both problems involving classification and regression. A decision tree is a data-structure consisting of a hierarchy of nodes. 

* Root Node: has no parent node, gives rise to two children nodes
* Internal Node: has one parent node, gives rise to two children nodes
* Leaf: has one parent node, but no children node --> prediction

Decision trees are linear models that aim to find logical rules that cluster data points into pure subgroups with common output values. With a series of if-else questions about indivudal features, the model can learn patterns from each feature in a way to produce the purest leaves. The purity, or homogenity of a cluster can be measured using the Gini index that evaluated impurity. In each iteration, the algorithm tries to find a breakpoint that can split the observation into more homogenous subgroups. 

Let's consider a 2-D feature set and see how we can construct a decision tree from the data. Our goal is to create a decision boundary that can help infer class labels.


