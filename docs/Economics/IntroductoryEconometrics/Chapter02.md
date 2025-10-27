# Chapter 2. The Simple Regression Model

## 2.1 Definition of the Simple Regression Model

A simple equation is

$$
y=\beta_0+\beta_1x+u. \quad [2.1]
$$

which is assumed to hold in the population of interest, defines the **simple linear regression model**.

The average value of $u$ in the population is zero.

$$
E(u)=0. \quad [2.5]
$$

The average value of $u$ does not depend on the value of x.

$$
E(u|x)=E(u). \quad [2.6]
$$

When assumption (2.6) holds, we say that $u$ is **mean independent** of $x$. When we combine mean independence with assumption (2.5), we obtain the **zero conditional mean assumption**, $E(u|x)=0$. 

Taking the expected value of (2.1) conditional on x and using $E(u|x)=0$ gives

$$
E(y|x)=\beta_0+\beta_1 x. \quad [2.8]
$$

Equation (2.8) shows that the **population regression function** (PRF), $E(y|x)$, is a linear function of $x$.

## 2.2 Deriving the Ordinary Least Squares Estimates

In the population, $u$ is uncorrelated with $x$. Therefore, $u$ has zero expected value and the covariance between $x$ and $u$ is zero:

$$
E(u)=0 \quad [2.10]
$$

and

$$
Cov(x,u)=E(xu)=0 \quad [2.11]
$$

Given $\bar{y}=n^{-1}\sum_{i=1}^ny_i$ and likewise for $\bar{x}$, the estimated intercept is

$$
\hat\beta_0=\bar{y}-\hat\beta_1\bar{x}. \quad [2.17]

$$

The estimated slope is

$$
\hat\beta_1=\frac{\sum_{i=1}^n\left(x_i-\bar{x}\right)\left(y_i-\bar{y}\right)}{\sum_{i=1}^n\left(x_i-\bar{x}\right)^2} \quad [2.19]
$$

The estimates given in (2.17) and (2.19) are called the **ordinary least squares (OLS)** estimates of $\beta_0$ and $\beta_1$.

The **residual** for observation $i$ is the difference between the actual $y_i$ and its fitted value $\hat{y}_i$:

$$
\hat{u}_i=y_i-\hat{y}_i=y_i-\hat\beta_0-\hat\beta_1x_i. \quad [2.21]
$$

Equation (2.22) is the **sum of squared residuals** for $\hat\beta_0$ and $\hat\beta_1$.

$$
\sum_{i=1}^n\hat{u}_i^2=\sum_{i=1}^n(y_i-\hat{\beta}_0-\hat{\beta}_1x_i)^2 \quad [2.22]
$$

Equations (2.14) and (2.15) are often called the **first order conditions** for the OLS estimates.

$$
\begin{aligned}
& \sum_{i=1}^n(y_i-\hat{\beta}_0-\hat{\beta}_1x_i)=0 \quad [2.14] \\
& \sum_{i=1}^nx_i(y_i-\hat{\beta}_0-\hat{\beta}_1x_i)=0 \quad [2.15]
\end{aligned}
$$

The conditions necessary for $(\hat\beta_0,\hat\beta_1)$ to minimize the sum of squared residuals are given exactly by the first order conditions.

Once we have determined the OLS intercept and slope estimates, we form the **OLS regression line**:

$$
\hat y=\hat\beta_0+\hat\beta_1x \quad [2.23]
$$

Equation (2.23) is also called the **sample regression function (SRF)** because it is the estimated version of the population regression function $E(y|x)=\beta_0+\beta_1 x$.

## 2.3 Properties of OLS on Any Sample of Data

### Algebraic Properties of OLS Statistics

1. The sum, and therefore the sample average of the OLS residuals, is zero. Mathematically,

$$
\sum_{i=1}^n\hat{u}_i=0. \quad [2.30]
$$

2. The sample covariance between the regressors and the OLS residuals is zero.

$$
\sum_{i=1}^nx_i\hat{u}_i=0. \quad [2.31]

$$

3. The point $(\bar x,\bar y)$ is always on the OLS regression line.

Define the **total sum of squares (SST)**, the **explained sum of squares (SSE)**, and the **residual sum of squares (SSR)** (also known as the sum of squared residuals), as follows:

$$
\text{SST}\equiv\sum_{i=1}^n(y_i-\bar{y})^2 \quad [2.33] \\
\text{SSE}\equiv\sum_{i=1}^n(\hat{y}_i-\bar{y})^2 \quad [2.33] \\
\text{SSR}\equiv\sum_{i=1}^n\hat{u}_i^2 \quad [2.35]

$$

$\text{SST}$ is a measure of the total sample variation in the $y_i$. If we divide $\text{SST}$ by $n-1$, we obtain the sample variance of $y$. Similarly, $\text{SSE}$ measures the sample variation in the $\hat{y}_i$, and $\text{SSR}$ measures the sample variation in the $\hat{u}_i$.

The total variation in $y$ can always be expressed as the sum of the explained variation and the unexplained variation $\text{SSR}$. Thus,

$$
\text{SST}\equiv\text{SSE}+\text{SSR}. \quad [2.36]
$$

### Goodness-of-Fit

The **R-squared** of the regression, sometimes called the **coefficient of determination**, is defined as

$$
R^2\equiv\text{SSE}/\text{SST}=1-\text{SSR}/\text{SST}. \quad [2.38]
$$

$R^2$ is the ratio of the explained variation compared to the total variation; thus, it is interpreted as the fraction of the sample variation in y that is explained by x.

## 2.5 Expected Values and Variances of the OLS Estimators

### Unbiasedness of OLS

**Assumption SLR.1: Linear in Parameters** 
In the population model, the dependent variable, $y$, is related to the independent variable, $x$, and the error (or disturbance), $u$, as

$$
y=\beta_0+\beta_1x+u, \quad [2.47]
$$

where $\beta_0$ and $\beta_1$ are the population intercept and slope parameters, respectively.

**Assumption SLR.2: Random Sampling**

We have a random sample of size n, $\{(x_i,y_i):i=1,2,\dots,n\}$, following the population model in equation (2.47).

**Assumption SLR.3: Sample Variation in the Explanatory Variable**

The sample outcomes on $x$, namely, $\{x_i,i=1,\dots,n\}$, are not all the same value.

**Assumption SLR.4: Zero Conditional Mean**

The error $u$ has an expected value of zero given any value of the explanatory variable. In other words,

$$
E(u|x)=0.
$$

**Theorem 2.1: Unbiasedness of OLS**

Using assumptions SLR.1 through SLR.4,

$$
E(\hat\beta_0)=\beta_0,E(\hat\beta_1)=\beta_1, \quad [2.53]
$$

for any values of $\beta_0$ and $\beta_1$. In other words, $\hat\beta_0$ is unbiased for $\beta_0$, and $\hat\beta_1$ is unbiased for $\beta_1$.

### Variances of the OLS Estimators

**Assumption SLR.5: Homoskedasticity**

The error $u$ has the same variance given any value of the explanatory variable. In other words,

$$
Var(u|x)=\sigma^2.
$$

When $Var(u|x)$ depends on x, the error term is said to exhibit **heteroskedasticity** (or nonconstant variance). Because $Var(u|x) =Var(y|x)$, heteroskedasticity is present whenever $Var(y|x)$ is a function of x.

**Theorem 2.2 Sampling Variances of The OLS Estimators**

Under Assumptions SLR.1 through SLR.5,

$$
\begin{aligned}
& Var(\hat\beta_1)=\frac{\sigma^2}{\sum_{i=1}^n(x_i-\bar{x})^2}=\sigma^2/\text{SST}_x \quad [2.57] \\
& Var(\hat\beta_0)=\frac{\sigma^2n^{-1}\sum_{i=1}^nx_i^2}{\sum_{i=1}^n(x_i-\bar{x})^2} \quad [2.58]
\end{aligned}
$$

where these are conditional on the sample values $\{x_1,…,x_n\}$.

Two restrictions that must be satisfied by the OLS residuals are given by the two OLS first order conditions:

$$
\sum_{i=1}^n\hat{u}_i=0,\sum_{i=1}^nx_i\hat{u}_i=0. \quad [2.60]
$$

One way to view these restrictions is this: if we know n-2 of the residuals, we can always get the other two residuals by using the restrictions implied by the first order conditions in (2.60). Thus, there are only n-2 **degrees of freedom** in the OLS residuals.

**Theorem 2.3: Unbiased Estimation of** $\sigma^2$

Under Assumptions SLR.1 through SLR.5,

$$
E(\hat\sigma^2)=\sigma^2.
$$

The natural estimator of $\sigma$ is

$$
\hat\sigma=\sqrt{\hat\sigma^2} \quad [2.62]
$$

and is called the **standard error of the regression (SER)**. Although $\hat\sigma$ is not an unbiased estimator of $\sigma$, it is a consistent estimator of $\sigma$.

Since $sd(\hat\beta_1)=\sigma/\sqrt{\text{SST}_x}$, the natural estimator of $sd(\hat\beta_1)$ is

$$
se(\hat\beta_1)=\hat\sigma/\sqrt{\text{SST}_x}=\hat\sigma/(\sum_{i=1}^n(x_i-\bar{x})^2)^{1/2}
$$

this is called the **standard error** of $\hat\beta_1$.