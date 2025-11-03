# 4.1 IV and Causality

To motivate the constant effects setup as a framework for the causal link between schooling and wages, suppose that potential outcomes can be written

$$
Y_{si}\equiv\alpha+\rho s+\eta_i
$$

We imagine that there is a vector of control variables, $A_i$, called "ability," that gives a selection-on-observables (将选择性偏误由可观察变量引入) story:

$$
\eta_i=A_i^\prime\gamma+v_i
$$

where $\gamma$ is again a vector of population regression coefficients, so that $v_i$ and $A_i$ are uncorrelated by construction. For now, the variables $A_i$, are assumed to be the only reason why $\eta_i$ and $s_i$ are correlated, so that $E[s_i v_i]=0$.

Thereby producing a long regression that can be written

$$
Y_i=\alpha+\rho s_i+A_i^\prime\gamma+v_i \quad (4.1.2)
$$

Instrumental variables, $Z_i$, is correlated with the causal variable of interest, $s_i$, but uncorrelated with any other determinants of the dependent variable, or $Z_i$ is uncorrelated with both $A_i$ and $v_i$, or $Cov(\eta_i,Z_i)=0$.

This statement "uncorrelated with any other determinants of the dependent variables" is called an *exclusion restriction* (排他性约束), since $Z_i$ can be said to be excluded from the causal model of interest.

Given the exclusion restriction, it follows from (4.1.2) that

$$
\rho=\frac{Cov(Y_i,Z_i)}{Cov(s_i,Z_i)}=\frac{Cov(Y_i,Z_i)/V(Z_i)}{Cov(s_i,Z_i)/V(Z_i)} \quad (4.1.3)
$$

The population regression of $Y_i$ on $Z_i$ called the reduced form (简约式).

The population regression of $s_i$ on $Z_i$ called the first stage (第一阶段).

It's worth recapping the assumptions needed for the ratio of covariances in (4.1.3) to equal the casual effect, $\rho$:

1. First, the instrument must have a clear effect on $s_i$. This is the first stage.
2. Second, the only reason for the relationship between $Y_i$ and $Z_i$ is the first stage. We're calling this second assumption the exclusion restriction, this assumption has two parts: 
   - The first is that the instrument is as good as randomly assigned (随机抽样), 
   - and the second is that the instrument has no effect on outcomes other than through the first-stage channel.

Where can you find an instrumental variable? For example, the economic model of education suggests that schooling decisions are based on the costs and benefits of alternative choices. Thus, one possible source of instruments for schooling is differences in costs due to loan policies or other subsidies that vary independently of ability or earnings potential. A second source in schooling is institutional constraints (制度约束).

Angrist and Krueger (1991) uses quarter of birth to construct IV estimates of the wages to schooling.

Panel A of figure 4.1.1 displays the education quarter-of-birth pattern for men who were born in the 1930s. The figure clearly shows that men born earlier in the calendar year tended to have lower average schooling levels. Panel A of figure 4.1.1 is a graphical depiction of the first stage. The first stage in a general IV framework is the regression of the causal variable of interest on covariates (协变量) and instruments (工具变量). The plot summarizes this regression because average schooling by year and quarter of birth is what you get for fitted values from a regression of schooling on a full set of year-of-birth dummies (covariates) and quarter-of-birth dummies (instruments).

Panel B of figure 4.1.1 displays average earnings by quarter of birth. This panel illustrates the reduced-form relationship between the instruments and the dependent variable. The reduced form is the regression of the dependent variable on any covariates in the model and the instruments. The figure shows that men born in early quarters almost always earned less than those born later in the year, even after adjusting for year of birth. Because an individual's date of birth is probably unrelated to his or her innate ability, motivation, or family connections, it seems credible to assert that the only reason for the up-and-down quarter-of-birth pattern in earnings is the up-and-down quarter-of-birth pattern in schooling. This is the critical assumption that drives the quarter-of-birth IV story.

A mathematical representation of the story told by figure 4.1.1 comes from the first-stage and reduced-form regression equations, spelled out below:

$$
\begin{aligned}
&s_i=X_i^\prime\pi_{10}+\pi_{11}Z_i+\xi_{1i} \quad (4.1.4a) \\
&Y_i=X_i^\prime\pi_{20}+\pi_{21}Z_i+\xi_{2i} \quad (4.1.4b)
\end{aligned}
$$

The parameter $\pi_{11}$ captures the first-stage effect of $Z_i$ on $s_i$, adjusting for covariates, $X_i$. The parameter $\pi_{21}$ captures the reduced-form effect of $Z_i$ on $yY_i$, adjusting for these same covariates. The instrument $Z_i$ is a dummy indicating quarter of birth and the covariates are dummies for year of birth and state of birth.

In the language of the SEM, the dependent variables in these two equations are said to be the endogenous variables (内生变量 determined jointly within the system), while the variables on the right-hand side are said to be the exogenous variables (外生变量 determined outside the system). The instruments $Z_i$ are a subset of the exogenous variables. The exogenous variables that are not instruments are said to be exogenous covariates.

The covariate-adjusted IV estimator is the sample analog of the ratio:

$$
\rho=\frac{\pi_{21}}{\pi_{11}}=\frac{Cov(Y_i,\tilde{z}_i)}{Cov(s_i,\tilde{z}_i)} \quad (4.1.5)
$$

where $\tilde{z}_i$ is the residual from a regression of $Z_i$ on the exogenous covariates, $X_i$. The right-hand side of (4.1.5) therefore swaps $\tilde{z}_i$ for $Z_i$ in the IV formula, (4.1.3).

The sample analog of equation (4.1.5) is an indirect least squares (ILS, 间接最小二乘估计值) estimator of $\rho$ in the causal model with covariates,

$$
Y_i=\alpha^\prime X_i+\rho s_i+\eta_i \quad (4.1.6)
$$

where $\eta_i$ is the compound error term, $A_i^\prime\gamma+v_i$.

## 4.1.1 Two-Stage Least Squares

In practice, of course, we almost always work with data from samples. Given a random sample, the first-stage fitted values are consistently estimated by

$$
\hat{s}_i=X_i^\prime\hat\pi_{10}+\hat\pi_{11}Z_i
$$

where $\hat\pi_{10}$ and $\hat\pi_{11}$ are OLS estimates from equation (4.1.4a).

The coefficient on $\hat{s}_i$ in the regression of $Y_i$ on $X_i$ and $\hat{s}_i$ is called the two-stage least squares (2SLS, 两阶段最小二乘估计值) estimator of $\rho$. In other words, 2SLS estimates can be constructed by OLS estimation of the "second-stage equation,"

$$
Y_i=\alpha^\prime X_i+\rho\hat{s}_i+[\eta_i+\rho(s_i-\hat{s}_i)] \quad (4.1.9)
$$

This is called 2SLS because it can be done in two steps, the first estimating $\hat{s}_i$ using equation (4.1.4a) and the second estimating equation (4.1.9).

2SLS is an IV estimator: the 2SLS estimate of $\rho$ in (4.1.9) is the sample analog of $\frac{Cov(Y_i,\hat{s}_i^*)}{Cov(s_i,\hat{s}_i^*)}$, where $\hat{s}_i^*$ is the residual from a regression of $\hat{s}_i$ on $X_i$.

## 4.1.2 The Wald Estimator
