# 3.1 Regression Fundamentals

## 3.1.1 Economic Relationships and the Conditional Expectation Function

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

The law of iterated expectations says that an unconditional expectation (无条件期望) can be written as the unconditional average of the CEF.

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

**Proof**: The CEF decomposition property implies the variance of $Y_i$ is the variance of the CEF plus the variance of the residual, $\epsilon_i\equiv Y_i-E[Y_i|X_i]$. The variance of $\epsilon$ is

$$
E[\epsilon_i^2]=E[E[\epsilon_i^2|X_i]]=E[V[Y_i|X_i]],
$$

where $E[\epsilon_i^2|X_i]=V[Y_i|X_i]$ because $\epsilon_i\equiv Y_i-E[Y_i|X_i]$.

## 3.1.2 Linear Regression and the CEF

The vector of population regression coefficients is defined as the solution to a population least squares problem. We let the $k \times 1$ regression coefficient vector $\beta$ be defined by solving

$$
\beta=\arg\min_b E[(Y_i−X^\prime_i b)^2]
$$

Using the first-order condition,

$$
E[X_i(Y_i−X^\prime_i b)] = 0,
$$

the solution can be written $\beta=E[X_i X^\prime_i]^{-1}E[X_i Y_i]$.

In the simple bivariate case (双变量回归模型) where the regression vector includes only the single regressor, $x_i$, and a constant, the slope coefficient is $\beta_1=\frac{Cov(Y_i,x_i)}{V(x_i)}$, and the intercept is $\alpha=E[Y_i] −\beta_1 E[X_i]$.

In the multivariate case, with more than one nonconstant regressor, the slope coefficient for the kth regressor is given below:

**REGRESSION ANATOMY**
$$
\beta_k=\frac{Cov(Y_i,\tilde{x}_{ki})}{V(\tilde{x}_{ki})}, \quad (3.1.3)
$$

where $\tilde{x}_{ki}$ is the residual from a regression of $x_{ki}$ on all the other covariates.($\tilde{x}_{ki}$是将$x_{ki}$关于其他协变量回归后得到的残差项)

In other words, $E[X_i X^\prime_i]^{-1}E[X_i Y_i]$ is the $k\times 1$ vector with kth element $\frac{Cov(Y_i,\tilde{x}_{ki})}{V(\tilde{x}_{ki})}$.

It shows us that each coefficient in a multivariate regression is the bivariate slope coefficient for the corresponding regressor after partialing out all the other covariates. (公式3.1.3告诉我们多元回归中每个回归元的系数都是该回归元在剔除其他回归元对自己的影响后与$Y_i$进行二元回归得到的斜率)

To verify the regression anatomy formula, substitute

$$
Y_i=\alpha+\beta_1 x_{1i}+\cdots+\beta_k x_{ki}+\cdots+\beta_K x_{Ki}+e_i
$$

in the numerator of (3.1.3). Since $\tilde{x}_{ki}$ is a linear combination of the regressors, it is uncorrelated with $e_i$. Also, since $\tilde{x}_{ki}$ is a residual from a regression on all the other covariates in the model, it must be uncorrelated with these covariates. Finally, for the same reason, the covariance of $\tilde{x}_{ki}$ with $x_{ki}$ is just the variance of $\tilde{x}_{ki}$. We therefore have $Cov(Y_i,\tilde{x}_{ki})=\beta_k V(\tilde{x}_{ki})$

Below we discuss three reasons why the vector of population regression coefficients might be of interest.

**Theorem 3.1.4** The Linear CEF Theorem (Regression Justification I). 

Suppose the CEF is linear. Then the population regression function is it.

The linear CEF theorem raises the question of what makes a CEF linear:

1. The classic scenario is *joint normality* (联合正态分布), that is, the vector $(Y_i,X_i^\prime)^\prime$ has a *multivariate normal distribution* (多元联合正态分布).
2. Another linearity scenario arises when regression models are saturated. (饱和回归模型)

**Theorem 3.1.5** The Best Linear Predictor Theorem (Regression Justification II).

The function $X_i^\prime\beta$ is the best linear predictor of $Y_i$ given $X_i$ in a MMSE sense.

**Theorem 3.1.6** The Regression CEF Theorem (Regression Justification III).

The function $X_i^\prime\beta$ provides the MMSE linear approximation to $E[Y_i|X_i]$, that is,

$$
\beta=\arg\min_b E\{(E[Y_i|X_i]-X_i^\prime b)^2\}
$$

An implication of the regression CEF theorem is that regression coefficients can be obtained by using $E[Y_i|X_i]$ as a dependent variable instead of $Y_i$ itself. An even simpler way to see this is to iterate expectations in the formula for $\beta$:

$$
\beta=E[X_i X^\prime_i]^{-1}E[X_i Y_i]=\beta=E[X_i X^\prime_i]^{-1}E[X_i E(Y_i|X_i)].
$$

## 3.1.3 Asymptotic OLS Inference

Suppose the vector $W_i \equiv [Y_i X_i^\prime]^\prime$ is independently and identically distributed in a sample of size N. A natural estimator of *the first population moment* (总体一阶矩), $E[W_i]$, is the sum, $\frac{1}{N}\sum_{i=1}^N W_i$. By the law of large numbers, this vector of *sample moments* (样本矩) gets arbitrarily close to the corresponding vector of population moments as the sample size grows. We might similarly consider *higher-order moments* (高阶矩) of the elements of $W_i$, for example the matrix of second moments, $E[W_i W_i^\prime]$, with sample analog $\frac{1}{N}\sum_{i=1}^N W_i W_i^\prime$.

The method of moments estimator of $\beta$ replaces each expectation by a sum (对$\beta$进行矩估计的方法是将期望算子换成连加符号). This logic leads to the ordinary least squares (OLS) estimator

$$
\hat\beta=\left[\sum_i X_iX_i^\prime\right]^{-1}\sum_i X_iY_i
$$

**THE LAW OF LARGE NUMBERS**: Sample moments converge in probability to the corresponding population moments. (样本矩依概率收敛于总体矩) In other words, the probability that the sample mean is close to the population mean can be made as high as you like by taking a large enough sample.

**THE CENTRAL LIMIT THEOREM**: Sample moments are asymptotically normally distributed (after subtracting the corresponding population moment and dividing by the square root of the sample size). The asymptotic covariance matrix (渐进协方差矩阵) is given by the variance of the underlying random variable. In other words, in large enough samples, appropriately *normalized sample moments* (标准化后的样本矩) are approximately normally distributed.

**SLUTSKY’S THEOREM**
1. Consider the sum of two random variables, one of which converges in distribution (一个依分布收敛) and the other converges in probability to a constant (另一个依概率收敛于常数): the asymptotic distribution of this sum is unaffected by replacing the one that converges to a constant by this constant. Formally, let $a_N$ be a statistic with an asymptotic distribution and let $b_N$ be a statistic with probability limit b. Then $a_N+b_N$ and $a_N+b$ have the same asymptotic distribution.
2. Consider the product of two random variables, one of which converges in distribution and the other converges in probability to a constant: the asymptotic distribution of this product is unaffected by replacing the one that converges to a constant by this constant. Formally, let $a_N$ be a statistic with an asymptotic distribution and let $b_N$ be a statistic with probability limit b. Then $a_Nb_N$ and $a_Nb$ have the same asymptotic distribution.

**THE CONTINUOUS MAPPING THEOREM**: Probability limits pass through continuous functions. (概率极限算子可以穿过连续函数) For example, the probability limit of any continuous function of a sample moment is the function evaluated at the corresponding population moment. (关于样本矩的任何连续函数的概率极限都等于在相应的总体矩处该连续函数的值) Formally, the probability limit of $h(b_N)$ is $h(b)$, where $\plim b_N = b$ and $h(\cdot)$ is continuous at $b$.

**THE DELTA METHOD**: Consider a vector-valued random variable that is asymptotically normally distributed. Continuously differentiable scalar functions (连续可微标量函数) of this random variable are also asymptotically normally distributed, with covariance matrix given by a quadratic form with the covariance matrix of the random variable on the inside and the gradient of the function evaluated at the probability limit of the random variable on the outside. (这个二次型中，居于中间的是该随机变量的协方差矩阵，居于两边的是这个函数在该随机变量的概率极限处的梯度) Formally, the asymptotic distribution of $h(b_N)$ is normal with covariance matrix $\nabla h(b)^\prime\Omega\nabla h(b)$, where $\plim b_N = b$, $h(\cdot)$ is continuously differentiable at $b$ with gradient $\nabla h(b)$, and $b_N$ has asymptotic covariance matrix $\Omega$.

$E[X_ie_i]=0$ is a consequence of $\beta=E[X_i X_i^\prime]^{−1}E[X_i Y_i]$ and $e_i=Y_i−X_i^\prime\beta$, and not an assumption about an underlying economic relation.

Substituting the identity for $Y_i\equiv X_i^\prime\beta+e_i$ in the formula for $\hat\beta$, we have

$$
\hat\beta=\beta+\left[\sum X_iX_i^\prime\right]^{-1}\sum X_ie_i
$$

The asymptotic distribution of $\hat\beta$ is the asymptotic distribution of $\sqrt{N}(\hat\beta-\beta)=N[\sum X_iX_i^\prime]^{-1}\frac{1}{\sqrt{N}}\sum X_ie_i$. By the Slutsky theorem, this has the same asymptotic distribution as $E[X_iX_i^\prime]\frac{1}{\sqrt{N}}\sum X_ie_i$. Since $E[X_ie_i]=0$, $\frac{1}{\sqrt{N}}\sum X_ie_i$ is a root-N normalized and *centered sample moment* (样本中心矩). By the central limit theorem, this is asymptotically normally distributed with mean zero and covariance matrix $E[X_iX_i^\prime e_i^2]$, since this matrix of fourth moments is the covariance matrix of $X_ie_i$. Therefore, $\hat\beta$ has an asymptotic normal distribution with probability limit $\beta$ and covariance matrix

$$
E[X_iX_i^\prime]^{-1}E[X_iX_i^\prime e_i^2]E[X_iX_i^\prime]^{-1}. \quad (3.1.7)
$$

The theoretical standard errors used to construct t-statistics are the square roots of the diagonal elements of (3.1.7). In practice these standard errors are estimated by substituting sums for expectations (用连加算子代替期望算子) and using the estimated residuals, $\hat{e}_i=Y_i-X_i^\prime\hat\beta$ to form the empirical *fourth moment matrix* (四阶矩矩阵), $\sum[X_iX_i^\prime\hat{e}_i^2]/N$.

Asymptotic standard errors computed in this way are known as *heteroskedasticity-consistent standard errors* (异方差修正标准误). They are also known as “robust” standard errors.

Robust standard errors are not the standard errors that you get by default from packaged software. Default standard errors are derived under a *homoskedasticity assumption* (同方差假设), specifically, $E[e_i^2|X_i]=\sigma^2$

Given homoskedasticity assumption, we have

$$
E[X_iX_i^\prime e_i^2]=E(X_iX_i^\prime E[e_i^2|X_i])=\sigma^2E[X_iX_i^\prime],
$$

by iterating expectations. The asymptotic covariance matrix of $\hat\beta$ then simplifies to

$$
\begin{aligned}
E[X_iX_i^\prime]^{-1}E[X_iX_i^\prime e_i^2]E[X_iX_i^\prime]^{-1}&=E[X_iX_i^\prime]^{-1}\sigma^2E[X_iX_i^\prime]E[X_iX_i^\prime]^{-1} \\
&=\sigma^2E[X_iX_i^\prime]^{-1}. \quad (3.1.8)
\end{aligned}
$$

The diagonal elements of (3.1.8) are what SAS or Stata report unless you request otherwise.

Our view of regression as an approximation to the CEF makes heteroskedasticity seem natural. If the CEF is nonlinear and you use a linear model to approximate it, then the quality of fit between the regression line and the CEF will vary with $X_i$.

Even if you are prepared to assume that the conditional variance (条件方差) of $Y_i$ given $X_i$ is constant, the fact that the CEF is nonlinear means that $E[(Y_i−X_i^\prime\beta)^2|X_i]$ will vary with $X_i$. To see this, note that

$$
\begin{aligned}
E[(Y_i−X_i^\prime\beta)^2|X_i]&=E\{[(Y_i-E[Y_i|X_i])+(E[Y_i|X_i]−X_i^\prime\beta)]^2\} \\
&=V[Y_i|X_i]+(E[Y_i+X_i]-X_i^\prime\beta)^2.
\end{aligned}
$$

Therefore, even if $V[Y_i|X_i]$ is constant, the residual variance (残差的方差) increases with the square of the gap between the regression line and the CEF.

While a linear CEF makes homoskedasticity (同方差) possible, this is not a sufficient condition (充分条件) for homoskedasticity.

A linear probability model (LPM线性概率模型) is any regression where the dependent variable is zero-one (只取0-1两个值).

Suppose the regression model is saturated, so the CEF given regressors is linear. Because the CEF is linear, the residual variance is also the conditional variance, $V[Y_i|X_i]$. But the dependent variable is a Bernoulli trial with conditional variance $P[Y_i=1|X_i](1−P[Y_i=1|X_i])$. We conclude that LPM residuals are necessarily heteroskedastic unless the only regressor is a constant.

The classical normal regression model postulates: fixed (non-stochastic) regressors, a linear CEF, normally distributed errors, and homoskedasticity. These stronger assumptions give us two things: (1) unbiasedness of the OLS estimator, (2) a formula for the sampling variance of the OLS estimator that is valid in small as well as large samples.

## 3.1.4 Saturated Models, Main Effects, and Other Regression Talk

Saturated regression models (饱和回归模型) are regression models with discrete explanatory variables, where the model includes a separate parameter for all possible values taken on by the explanatory variables. 

When working with a single explanatory variable (单一解释变量) indicating whether a worker is a college graduate, the model is saturated by including a single dummy for college graduates and a constant.

Suppose that $s_i=0,1,2,\dots,\tau$. A saturated regression model for $s_i$ is

$$
Y_i=\alpha+\beta_1d_{1i}+\beta_2d_{2i}+\cdots+\beta_{\tau}d_{\tau i}+\epsilon_i
$$

where $d_{ji}=1[s_i=j]$ is a dummy variable indicating schooling level j, and $\beta_j$ is said to be the jth-level schooling effect. ($s_i=j$时$d_{ji}=1$, 否则$d_{ji}=0$; $\beta_j$是教育水平为j年级所带来的效应)

If there are two explanatory variables (两个解释变量) (one dummy indicating college graduates and one dummy indicating sex), the model is saturated by including these two dummies, their product, and a constant. The coefficients on the dummies are known as main effects (主效应), while the product is called an interaction term (交互项).

Any set of indicators (dummies) that can be used to identify each value taken on by all covariates produces a saturated model. (任何能识别出所有协变量取值的虚拟变量集合都能构成一个饱和模型) For example, an alternative saturated model includes dummies for male college graduates, male nongraduates, female college graduates, and female nongraduates, but no intercept.

Let $x_{1i}$ indicate college graduates and $x_{2i}$ indicate women. The CEF given $x_{1i}$ and $x_{2i}$ takes on four values:

$$
\begin{aligned}
&E[Y_i|x_{1i}=0,x_{2i}=0]=\alpha \\
&E[Y_i|x_{1i}=1,x_{2i}=0]=\alpha+\beta_1 \\
&E[Y_i|x_{1i}=0,x_{2i}=1]=\alpha+\gamma \\
&E[Y_i|x_{1i}=1,x_{2i}=0]=\alpha+\beta_1+\gamma+\delta_1
\end{aligned}
$$

The saturated regression equation becomes

$$
Y_i=\alpha+\beta_1 x_{1i}+\gamma x_{2i}+\delta(x_{1i}x_{2i})+\epsilon_i
$$

We can combine the multivalued schooling variable with sex to produce a saturated model that has $\tau$ main effects for schooling, one main effect for sex, and $\tau$ sex-schooling interactions:

$$
Y_i=\alpha+\sum_{j=1}^\tau\beta_j d_{ji}+\gamma x_{2i}+\sum_{j=1}^\tau\delta_j(d_{ji}x_{2i})+\epsilon_i
$$

The coefficients on the interaction terms, $\delta_j$, tell us how each of the schooling effects differ by sex.
