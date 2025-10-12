# 3.2 Regression and Causality

## 3.2.1 The Conditional Independence Assumption

The conditional independence assumption (CIA条件独立假设) is also called selection on observables because the covariates to be held fixed are assumed to be known and observed.

The causal relationship between college attendance and earnings can be described using the potential outcomes:

$$
\text{Potential outcome}=\begin{cases}
Y_{1i} \quad \text{if } C_i=1 \\
Y_{0i} \quad \text{if } C_i=0
\end{cases}
$$

In this case, $Y_{0i}$ is i's earnings without college, while $Y_{1i}$ is i's earnings if he goes. We would like to know the difference between $Y_{1i}$ and $Y_{0i}$, which is the causal effect of college attendance on individual i.

The observed outcome, $Y_i$, can be written in terms of potential outcomes as

$$
Y_i=Y_{0i}+(Y_{1i}-Y_{0i})C_i
$$

We get to see one of Y_{1i} or Y_{0i}, but never both. We therefore hope to measure the average of $Y_{1i}Y_{0i}$, or the average for some group.

$$
\underbrace{E[Y_i|C_i=1]-E[Y_i|C_i=0]}_{\text{Observed difference in earnings}}=\underbrace{E[Y_{1i}-Y_{0i}|C_i=1]}_{\text{Average treatment effect on the treated}}+\underbrace{E[Y_{0i}|C_i=1]-E[Y_{0i}|C_i=0]}_{\text{Selection bias}}
$$

It seems likely that those who go to college would have earned more anyway. If so, selection bias is positive and the naive comparison, $E[Y_i|C_i=1]-E[Y_i|C_i=0]$, exaggerates the benefits of college attendance.

The CIA asserts that conditional on observed characteristics, $X_i$, selection bias disappears. (CIA指的是在观察到特点$X_i$的条件下，选择性偏误消失) Formally, this means

$$
\{Y_{0i},Y_{1i}\}\amalg C_i|X_i,
$$

where the symbol “$\amalg$” denotes the independence relation and random variables to the right of the vertical bar are the conditioning set.

Given the CIA, conditional-on-$X_i$ comparisons of average earnings across schooling levels have a causal interpretation.

$$
E[Y_i|X_i,C_i=1]-E[Y_i|X_i,C_i=0]=E[Y_{1i}-Y_{0i}|X_i]
$$

Now, we'd like to expand the conditional independence assumption to causal relations that involve variables that can take on more than two values, such as years of schooling, $s_i$. The causal relationship between schooling and earnings is likely to be different for each person. We therefore use the individual-specific functional notation,

$$
Y_{si}\equiv f_i(s)
$$

to denote the potential earnings that person i would receive after obtaining s years of education.

The CIA in this more general setup becomes

$$
Y_{si}\amalg s_i|X_i,\text{ for all s}.
$$

Given the CIA, conditional-on-$X_i$ comparisons of average earnings across schooling levels have a causal interpretation.

$$
E[Y_i|X_i,s_i=s]−E[Y_i|X_i,s_i=s−1]=E[f_i(s)−f_i(s−1)|X_i]
$$

Regression provides an easy-to-use empirical strategy that automatically turns the CIA into causal effects. Two routes can be traced from the CIA to regression. One assumes that $f_i(s)$ is both linear in $s$ and the same for everyone except for an additive error term, in which case linear regression is a natural tool to estimate the features of $f_i(s)$. A more general route recognizes that $f_i(s)$ almost certainly differs for different people, and moreover need not be linear in $s$. Even so, allowing for random variation in $f_i(s)$ across people and for nonlinearity for a given person, regression can be thought of as a strategy for the estimation of a weighted average of the individual-specific difference, $f_i(s)−f_i(s−1)$.

Suppose that a linear constant effects causal model:

$$
f_i(s)=\alpha+\rho s+\eta_i. \quad (3.2.7)
$$

In addition to being linear, this equation says that the functional relationship of interest is the same for everyone. Again, $s$ is written without an i subscript, because equation (3.2.7) tells us what person i would earn for any value of $s$, and not just the realized value, $s_i$.

Substituting the observed value $s_i$ for s in equation (3.2.7), we have

$$
Y_i=\alpha+\rho s_i+\eta_i. \quad (3.2.8)
$$

Suppose now that the CIA holds given a vector of observed covariates, $X_i$. We decompose the random part of potential earnings, $\eta_i$, into a linear function of observable characteristics, $X_i$, and an error term, $v_i$:

$$
\eta_i=X_i^\prime\gamma+v_i
$$

where $\gamma$ is a vector of population regression coefficients that is assumed to satisfy $E[\eta_i|X_i]=X_i^\prime\gamma$.

Moreover, by virtue of the CIA, we have

$$
E[f_i(s)|X_i,s_i]=E[f_i(s)|X_i]=\alpha+\rho s+E[\eta_i|X_i]=\alpha+\rho s+X_i^\prime\gamma.
$$

The residual in the linear causal model

$$
Y_i=\alpha+\rho s_i+X_i^\prime\gamma+v_i
$$

is therefore uncorrelated with the regressors, $s_i$ and $X_i$, and the regression coefficient $\rho$ is the causal effect of interest.

## 3.2.2 The Omitted Variables Bias Formula

In addition to the variable of interest, $s_i$, we have now introduced a set of control variables, $X_i$, into our regression. The omitted variables bias (OVB遗漏变量偏误) formula describes the relationship between regression estimates in models with different sets of control variables.

Suppose the relevant set of control variables in the schooling regression can be boiled down to (简化) a combination of family background, intelligence, and motivation. Let these specific factors be denoted by a vector, $A_i$, which we refer to by the shorthand term "ability". The regression of wages on schooling, $s_i$, controlling for ability can be written as

$$
Y_i=\alpha+\rho s_i+A_i^\prime\gamma+e_i \quad(3.2.10)
$$

where $\alpha$, $\rho$, and $\gamma$ are population regression coefficients and $e_i$ is a regression residual that is uncorrelated with all regressors by definition.

In practice, ability is hard to measure. The resulting "short regression" coefficient is related to the "long regression" coefficient in equation (3.2.10) as follows:

**OMITTED VARIABLES BIAS FORMULA**

$$
\frac{Cov(Y_i,s_i)}{V(s_i)}=\rho+\gamma^\prime\delta_{As}
$$

where $\delta_{As}$ is the vector of coefficients from regressions of the elements of $A_i$ on $s_i$.

To paraphrase, the OVB formula says: Short equals long plus the effect of omitted times the regression of omitted on included. (短回归参数等于长回归参数加上遗漏变量效应乘以遗漏变量对被包含变量的回归系数)

## 3.2.3 Bad Control

Bad controls (不合格的控制变量) are variables that are themselves outcome variables in the notional experiment at hand. That is, bad controls might just as well be dependent variables too.

Let $W_i$ be a dummy variable that denotes white collar workers (白领) and let $Y_i$ denote earnings. The realization of these variables is determined by college graduation status and potential outcomes that are indexed against $C_i$. We have

$$
\begin{aligned}
&Y_i=C_i Y_{1i}+(1-C_i)Y_{0i} \\
&W_i=C_i W_{1i}+(1-C_i)W_{0i}
\end{aligned}
$$

where $C_i=1$ for college graduates and is zero otherwise, $\{Y_{1i}, Y_{0i}\}$ denotes potential earnings, and $\{W_{1i},W_{0i}\}$ denotes potential white collar status.

Consider the difference in mean earnings between college graduates and others, conditional on working at a white collar job. We can compute this in a regression model that includes $W_i$ or by regressing $Y_i$ on $C_i$ in the sample where $W_i=1$.

$$
E[Y_i|W_i=1,C_i=1]−E[Y_i|W_i=1,C_i=0]=E[Y_{1i}|W_{1i}=1,C_i=1]−E[Y_{0i}|W_{0i}=1,C_i=0].
$$

By the joint independence of $\{Y_{1i},W_{1i},Y_{0i},W_{0i}\}$ and $C_i$, we have

$$
E[Y_{1i}|W_{1i}=1,C_i=1]−E[Y_{0i}|W_{0i}=1,C_i=0]=E[Y_{1i}|W_{1i}=1]−E[Y_{0i}|W_{0i}=1].
$$

This expression illustrates the apples-to-oranges nature of the bad control problem:

$$
E[Y_{1i}|W_{1i}=1]−E[Y_{0i}|W_{0i}=1]=\underbrace{E[Y_{1i}-Y_{0i}|W_{1i}=1]}_\text{Causal effect}+\underbrace{\{E[Y_{0i}|W_{1i}=1]-E[Y_{0i}|W_{0i}=1]\}}_\text{Selection bias}.
$$

A second version of the bad control scenario involves proxy control (代理变量), that is, the inclusion of variables that might partially control for omitted factors but are themselves affected by the variable of interest.

Suppose you are interested in a long regression, similar to (3.2.10),

$$
Y_i=\alpha+\rho s_i+\gamma a_i+e_i \quad (3.2.13)
$$

where $a_i$ is an IQ score that measures innate ability (天生能力) in eighth grade, before any relevant schooling choices are made. The error term in this equation satisfies $E[s_i e_i]=E[a_i e_i]=0$ by definition. Since $a_i$ is measured before $s_i$ is determined, it is a good control. ($a_i$是在个体做出$s_i$决策之前得到的，所有它是个好的控制变量)

Equation (3.2.13) is the regression of interest, but unfortunately, data on $a_i$ are unavailable. However, you have a second ability measure collected later, after schooling is completed. Call this variable late ability (后天能力), $a_{li}$.

$$
a_{li}=\pi_0+\pi_1 s_i+\pi_2 a_i.
$$

Using (3.2.14) to substitute for $a_i$ in (3.2.13), the regression on $s_i$ and $a_{li}$ is

$$
Y_i=(\alpha-\gamma\frac{\pi_0}{\pi_2})+(\rho-\gamma\frac{\pi_1}{\pi_2})s_i+\frac{\gamma}{\pi_2}a_{li}+e_i
$$

In this scenario, $\gamma$, $\pi_1$, and $\pi_2$ are all positive, so $\rho-\gamma\frac{\pi_1}{\pi_2}$ is too small unless $\pi_1$ turns out to be zero. In other words, use of a proxy control that is increased by the variable of interest generates a coefficient below the desired effect.

One moral of both the bad control and the proxy control stories is that when thinking about controls, timing matters. Variables measured before the variable of interest was determined are generally good controls.
