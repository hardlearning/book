# Chapter 3 Making Regression Make Sense

## 3.1 Regression Fundamentals

### 3.1.1 Economic Relationships and the Conditional Expectation Function

The conditional expectation function (CEF) for a dependent variable $Y_i$, given a $k\times 1$ vector of covariates $X_i$ (with elements $x_{ki}$), is the expectation or population average, of $Y_i$ with $X_i$ held fixed.

The CEF is written $E[Y_i|X_i]$ and is a function of $X_i$.

For continuous $Y_i$ with conditional density $f_y(t|X_i = x)$ at $Y_i = t$, the CEF is

$$
E[Y_i|X_i = x]=\int tf_y(t|X_i=x)dt
$$

If $Y_i$ is discrete,

$$
E[Y_i|X_i = x]=\sum_t tP(Y_i = t|X_i =x),
$$

where $P(Y_i = t|X_i = x)$ is the conditional probability mass function for $Y_i$ given $X_i = x$.

The law of iterated expectations says that an unconditional expectation can be written as the unconditional average of the CEF.

$$
E[Y_i] = E\{E[Y_i|X_i]\}
$$

where the outer expectation uses the distribution of $X_i$.(处在外面一层的期望算子针对$X_i$的分布求期望)

The power of the law of iterated expectations comes from the way it breaks a random variable into two pieces, the CEF and a residual with special properties.

**Theorem 3.1.1** The CEF Decomposition Property.

$$
Y_i = E[Y_i|X_i]+\epsilon_i
$$

where (i) $\epsilon_i$ is mean independent of $X_i$, that is, $E[\epsilon_i|X_i] = 0$, and therefore (ii) $\epsilon_i$ is uncorrelated with any function of $X_i$.

The CEF is the best predictor of $Y_i$ given $X_i$ in the sense that it solves a minimum mean squared error (MMSE) prediction problem.

**Theorem 3.1.2** The CEF Prediction Property. 

Let $m(X_i)$ be any function of $X_i$. The CEF solves

$$
E[Y_i|X_i]=\arg\min_{m(X_i)}E[(Y_i-m(X_i))^2],
$$

so it is the MMSE predictor of $Y_i$ given $X_i$.

**Theorem 3.1.3** The analysis of variance (ANOVA) theorem.

$$
V(Y_i) = V(E[Y_i|X_i])+E[V(Y_i|X_i)],
$$

where $V(\cdot)$ denotes variance and $V(Y_i|X_i)$ is the conditional variance of $Y_i$ given $X_i$.

The CEF decomposition property implies the variance of $Y_i$ is the variance of the CEF plus the variance of the residual.

### 3.1.2 Linear Regression and the CEF

We let the $k \times 1$ regression coefficient vector $\beta$ be defined by solving

$$
\beta=\arg\min_b E[(Y_i−X^\prime_i b)^2]
$$

Using the first-order condition,

$$
E[X_i(Y_i−X^\prime_i b)] = 0,
$$

the solution can be written $\beta=E[X_i X^\prime_i]^{-1}E[X_i Y_i]$.

In the simple bivariate case where the regression vector includes only the single regressor, $x_i$, and a constant, the slope coefficient is $\beta_1=\frac{Cov(Y_i,x_i)}{V(x_i)}$, and the intercept is $\alpha=E[Y_i] −\beta_1 E[X_i]$.

In the multivariate case, with more than one nonconstant regressor, the slope coefficient for the kth regressor is given below:

**REGRESSION ANATOMY**
$$
\beta_k=\frac{Cov(Y_i,\tilde{x}_{ki})}{V(\tilde{x}_{ki})}, \quad (3.1.3)
$$

where $\tilde{x}_{ki}$ is the residual from a regression of $x_{ki}$ on all the other covariates.($\tilde{x}_{ki}$是将$x_{ki}$关于其他协变量回归后得到的残差项)

In other words, $E[X_i X^\prime_i]^{-1}E[X_i Y_i]$ is the $k\times 1$ vector with kth element $\frac{Cov(Y_i,\tilde{x}_{ki})}{V(\tilde{x}_{ki})}$.

This formula (3.1.3) shows us that each coefficient in a multivariate regression is the bivariate slope coefficient for the corresponding regressor after partialing out all the other covariates. (这个公式告诉我们多元回归中每个回归元的系数都是该回归元在剔除其他回归元对自己的影响后与$Y_i$进行二元回归得到的斜率)

**Theorem 3.1.4** The Linear CEF Theorem (Regression Justification I). 

Suppose the CEF is linear. Then the population regression function is it.

The linear CEF theorem raises the question of what makes a CEF linear:

1. The classic scenario is joint normality, that is, the vector $(Y_i,X_i^\prime)^\prime$ has a multivariate normal distribution.
2. Another linearity scenario arises when regression models are saturated.

**Theorem 3.1.5** The Best Linear Predictor Theorem (Regression Justification II).

The function $X_i^\prime\beta$ is the best linear predictor of $Y_i$ given $X_i$ in a MMSE sense.

**Theorem 3.1.6** The Regression CEF Theorem (Regression Justification III).

The function $X_i^\prime\beta$ provides the MMSE linear approximation to $E[Y_i|X_i]$, that is,

$$
\beta=\arg\min_b E\{(E[Y_i|X_i]-X_i^\prime b)^2\}
$$

### 3.1.3 Asymptotic OLS Inference

Suppose the vector $W_i \equiv [Y_i X_i^\prime]^\prime$ is independently and identically distributed in a sample of size N. A natural estimator of the first population moment, $E[W_i]$, is the sum, $\frac{1}{N}\sum_{i=1}^N W_i$. By the law of large numbers, this vector of sample moments gets arbitrarily close to the corresponding vector of population moments as the sample size grows. We might similarly consider higher-order moments of the elements of $W_i$, for example the matrix of second moments, $E[W_i W_i^\prime]$, with sample analog $\frac{1}{N}\sum_{i=1}^N W_i W_i^\prime$.

This logic leads to the ordinary least squares (OLS) estimator

$$
\hat\beta=\left[\sum_i X_iX_i^\prime\right]^{-1}\sum_i X_iY_i
$$

**THE LAW OF LARGE NUMBERS**: Sample moments converge in probability to the corresponding population moments.

**THE CENTRAL LIMIT THEOREM**: Sample moments are asymptotically normally distributed (after subtracting the corresponding population moment and dividing by the square root of the sample size).

**SLUTSKY’S THEOREM**
1. Consider the sum of two random variables, one of which converges in distribution and the other converges in probability to a constant: the asymptotic distribution of this sum is unaffected by replacing the one that converges to a constant by this constant. Formally, let $a_N$ be a statistic with an asymptotic distribution and let $b_N$ be a statistic with probability limit b. Then $a_N+b_N$ and $a_N+b$ have the same asymptotic distribution.
2. Consider the product of two random variables, one of which converges in distribution and the other converges in probability to a constant: the asymptotic distribution of this product is unaffected by replacing the one that converges to a constant by this constant. Formally, let $a_N$ be a statistic with an asymptotic distribution and let $b_N$ be a statistic with probability limit b. Then $a_Nb_N$ and $a_Nb$ have the same asymptotic distribution.

**THE CONTINUOUS MAPPING THEOREM**: Probability limits pass through continuous functions. For example, the probability limit of any continuous function of a sample moment is the function evaluated at the corresponding population moment. Formally, the probability limit of $h(b_N)$ is $h(b)$, where $\plim b_N = b$ and $h(\cdot)$ is continuous at $b$.

**THE DELTA METHOD**: Consider a vector-valued random variable that is asymptotically normally distributed. Continuously differentiable scalar functions of this random variable are also asymptotically normally distributed, with covariance matrix given by a quadratic form with the covariance matrix of the random variable on the inside and the gradient of the function evaluated at the probability limit of the random variable on the outside. Formally, the asymptotic distribution of $h(b_N)$ is normal with covariance matrix $\nabla h(b)^\prime\Omega\nabla h(b)$, where $\plim b_N = b$, $h(\cdot)$ is continuously differentiable at $b$ with gradient $\nabla h(b)$, and $b_N$ has asymptotic covariance matrix $\Omega$.

Substituting the identity for $Y_i\equiv X_i^\prime\beta+e_i$ in the formula for $\hat\beta$, we have

$$
\hat\beta=\beta+\left[\sum X_iX_i^\prime\right]\sum X_ie_i
$$

Therefore, $\hat\beta$ has an asymptotic normal distribution with probability limit $\beta$ and covariance matrix

$$
E[X_iX_i^\prime]^{-1}E[X_iX_i^\prime e_i^2]E[X_iX_i^\prime]^{-1}
$$

The theoretical standard errors used to construct t-statistics are the square roots of the diagonal elements. They are also known as “robust” standard errors.

Default standard errors are derived under a homoskedasticity assumption, specifically, $E[e_i^2|X_i]=\sigma^2$

A linear probability model (LPM) is any regression where the dependent variable is zero-one.

The classical normal regression model postulates: fixed (non-stochastic) regressors, a linear CEF, normally distributed errors, and homoskedasticity. These stronger assumptions give us two things: (1) unbiasedness of the OLS estimator, (2) a formula for the sampling variance of the OLS estimator that is valid in small as well as large samples.

### 3.1.4 Saturated Models, Main Effects, and Other Regression Talk

Saturated regression models are regression models with discrete explanatory variables, where the model includes a separate parameter for all possible values taken on by the explanatory variables.

If there are two explanatory variables—say, one dummy indicating college graduates and one dummy indicating sex— the model is saturated by including these two dummies, their product, and a constant. The coefficients on the dummies are known as main effects, while the product is called an interaction term.

## 3.2 Regression and Causality

### 3.2.1 The Conditional Independence Assumption

The conditional independence assumption (CIA) is also called selection on observables because the covariates to be held fixed are assumed to be known and observed.

The CIA asserts that conditional on observed characteristics, $X_i$, selection bias disappears. Formally, this means

$$
\{Y_{0i},Y_{1i}\}\amalg C_i|X_i,
$$

where the symbol “$\amalg$” denotes the independence relation and random variables to the right of the vertical bar are the conditioning set.

### 3.2.2 The Omitted Variables Bias Formula

The omitted variables bias (OVB) formula describes the relationship between regression estimates in models with different sets of control variables.

**OMITTED VARIABLES BIAS FORMULA**

$$
\frac{Cov(Y_i,s_i)}{V(s_i)}=\rho+\gamma^\prime\delta_{As}
$$

where $\delta_{As}$ is the vector of coefficients from regressions of the elements of $A_i$ on $s_i$.

To paraphrase, the OVB formula says: Short equals long plus the effect of omitted times the regression of omitted on included.

### 3.2.3 Bad Control

Bad controls are variables that are themselves outcome variables in the notional experiment at hand. That is, bad controls might just as well be dependent variables too.

## 3.3 Heterogeneity and Nonlinearity

### 3.3.1 Regression Meets Matching

Matching estimators are appealingly simple: at bottom, matching amounts to covariate-specific treatment-control comparisons, weighted together to produce a single overall average treatment effect. (事实上，匹配法对由每个协变量的特定值所决定的个体计算处理组和控制组之间的平均差异，然后用加权平均的方式将这些因果效应汇总到一个总的因果效应中。)