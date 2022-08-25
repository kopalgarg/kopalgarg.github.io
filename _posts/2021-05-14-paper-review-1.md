---
layout: post
title: Summary - Instance-wise Feature Importance for Time-series Models
published: true
---
**Title:**	What went wrong and when? Instance-wise feature importance for time-series black-box models  
**Link:**	https://arxiv.org/abs/2003.02821

Explainability, or an understanding of how a ML model outputs a given prediction, is important for decision making in healthcare applications. Explainability has been overlooked in the time-series domain where due to the dynamic nature of the data, features that drive model predictions change over time. Two approaches for explaining time-series ML model predictions currently exist. 

_Static supervised learning_: The first class of methods is used for static supervised learning cases, and it uses the idea of instance-level feature importance. These methods either compute the gradient of output w.r.t. to input vector or perturb (modify the feature set in some way - e.g. use a subset of the feature set, assign different weights/importance, etc.) to evaluate their impact on the output. These approaches fail to model the dynamic nature and temporal dependencies of time-series data. 

_Instance-level feature importance_: The second class of methods uses attention models designed for time-series data. Attention scores can be interpreted as an importance score for different observations over time.

The paper presents a framework, called Feature Importance in Time (FIT) to measure the importance of observations over time based on how much they contribute to the temporal shift of the model output distribution. The score quantifies how well the observation approx. the predictive shift of ever time step. This framework can be applied to any blackbox model in a time series setting, and is therefore considered to be a model-agnostic method. Model-agnostic interpretation methods can be used with any type of model. Using interpretable models is disadvantageous as predictive performance is lost compared to other ML models, and model-specific interpretation methods bind you to one model and make it difficult to switch to something else. Paper contributions: (1) KL divergence to compare the predictive distributional shift and predictive distributional shift where remaining features are unobserved, (2) generative models to learn time-series dynamics. This is to model the distribution of measurements and then approx. the counterfactual effect of subsets of observations over time, and (3) evaluate the aggregate importance of feature subsets over time.

The goal of FIT is to assign an importance score to a set of observations corresponding to a subset of features `s` at time `t`. This is done by approximating whether the partial conditional distribution for a given set of observations at time `t-1` approximates the full predictive distribution at time `t`. This characterization of distributional shifts from `t-1` to `t` is done using KL-divergence.

When a new observation `x_st` is added, its relative importance to other observations can be evaluated as to whether it adds additional information that may explain the change in the predictive distribution from the previous time step. The assignment score is a measure of the importance of the new set of observations `S` at time `t`. (An important observations is one that approx. outcome distribution even in the absence of other features). 

<img src = "https://latex.codecogs.com/gif.latex?I%28x_s%2C%20t%29%20%3D%20KL%28p%28y%7CX_%7B0%3At%7D%29%7C%7C%20p%28y%7CX_%7B0%3At-1%7D%29%29%20-%20KL%28p%28y%7CX_%7B0%3At%7D%29%7C%7C%20p%28y%7CX_%7B0%3At-1%7D%2C%20x_%7BS%2Ct%7D%29%29" >

where the first KL divergence term is the temporal shift (T1) and the second term is the unexpected distribution shift (T2). T1 estimates the distributional shift between the predicted distribution at `t` and `t-1`. T2 measures the residual effect after adding only <img src= "https://latex.codecogs.com/gif.latex?x_%7BS%2Ct%7D">.

(1) If `I` > 0 (T1>0, T2>0), then the subset of features explains predictive temporal shift completely. If `I`is at its max, then if only <img src= "https://latex.codecogs.com/gif.latex?x_%7BS%2Ct%7D"> was captured, the fully predictive distribution would be fully captured.

(2) If `I` = 0 (T1 = T2), then the subset of features is irrelevant and does not explain the temporal shift. It says that the outcome distribution changed over the time interval but the selected subset of features does not reflect the predictive distribution at time `t`.

(3) If `I` < 0 (T1>0, T2>0) then not only does the subset not explain the temporal shift but it also worsens the estimate of the predictive distribution.

Cross-entropy `H(P,Q)` can be interpreted as measuring the avg. # additional bits of information <img src= "https://latex.codecogs.com/gif.latex?x_%7BS%2Ct%7D"> provides at time `t` in approx. distribution. 

When the cardinality of `S` is 1 and `D` approaches infinity, then T1 = T2, implying that any one feature is unable to approx. predictive distribution `I` = 0).

When the cardinality `S` is D (using all features), T2 =0 , and `I` = max. This ascertains the importance of all features.

In the `I` equation, <img src = "https://latex.codecogs.com/gif.latex?p%28y%7CX_%7B0%3At%7D%29"> is approx. using trained blackbox model, `f_theta` and time series, `X`. 
<img src = "https://latex.codecogs.com/gif.latex?p%28y%7CX_%7B0%3At-1%7D%29"> is approx. using trained blackbox model, `f_theta` and time series, `X`.
<img src = "https://latex.codecogs.com/gif.latex?p%28y%7CX_%7B0%3At-1%7D%2C%20x_%7BS%2Ct%7D%29"> is the partial predictive distribution approx. written as an expectation term. Monte Carlo is used to estimate the expectation by sampling unobserved counterfactuals from the distribution condition on subset, `s`.

FIT uses a generative model, `G` to estimate the distribution of measurements conditioned on past distrbutions to approximate the counterfactual.

In the paper, a recurrent gen. is used as it models non-stationary time series while handeling observations of any length. Specifics of the model can be a design choice, and since the framework is model agnostic, any blackbox model can be used.

Overall, FIT approx. the aggregate importance of subsets of feautures. This is especially important in cases where simultaneous changes in joint measurements drive outcome. FIT can also find a minimal set of observations to acquire in a time series setting to approx. the predictive distribution well.
