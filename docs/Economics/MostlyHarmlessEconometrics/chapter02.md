# Chapter 2 The Experimental Ideal

## 2.1 The Selection Problem

We can think about hospital treatment as a binary random variable, $D_i=\{0,1\}$. (D表示是否接受治疗) The outcome of interest, a measure of health status, is denoted by $Y_i$. The question is whether $Y_i$ is affected by hospital care.

Hence, for any individual there are two potential health variables:

$$
\text{Potential outcome}=
\begin{cases}
Y_{1i} & \mathrm{if}\quad D_i=1 \\
Y_{0i} & \mathrm{if}\quad D_i=0
\end{cases}
$$

$Y_{0i}$ is the health status of an individual had he not gone to the hospital, irrespective of whether he actually went, while $Y_{1i}$ is the individual’s health status if he goes. (Y表示是否去过医院后的健康状态，0是没去过，1是去过)

We would like to know the difference between $Y_{1i}$ and $Y_{0i}$, which can be said to be the causal effect of going to the hospital for individual i.

The observed outcome, $Y_i$, can be written in terms of potential outcomes as

$$
Y_i=
\begin{cases}
Y_{1i} & \mathrm{if}\quad D_i=1 \\
Y_{0i} & \mathrm{if}\quad D_i=0
\end{cases}
=Y_{0i}+(Y_{1i}-Y_{0i})D_i \quad (2.1.1)
$$

This notation is useful because $Y_{1i}-Y_{0i}$ is the causal effect of hospitalization for an individual.

The comparison of average health conditional on hospitalization status is formally linked to the average causal effect by the equation:

$$
\underbrace{E[Y_i|D_i=1]-E[Y_i|D_i=0]}_{\text{Observed difference in average health}}=\underbrace{E[Y_{1i}|D_i=1]-E[Y_{0i}|D_i=1]}_{\text{Average treatment effect on the treated}}+\underbrace{E[Y_{0i}|D_i=1]-E[Y_{0i}|D_i=0]}_{\text{Selection bias}}.
$$

The term $E[Y_{1i}|D_i=1]−E[Y_{0i}|D_i=1]=E[Y_{1i}−Y_{0i}|D_i=1]$ is the average causal effect of hospitalization on those who were hospitalized.

Selection bias is the difference in average $Y_{0i}$ between those who were and those who were not hospitalized.

Because the sick are more likely than the healthy to seek treatment, those who were hospitalized have worse values of $Y_{0i}$, making selection bias negative in this example.

## 2.2 Random Assignment Solves the Selection Problem

Random assignment of $D_i$ solves the selection problem because random assignment makes $D_i$ independent of potential outcomes.

$$
\begin{aligned}
E[Y_i|D_i=1]−E[Y_i|D_i=0]&=E[Y_{1i}|D_i=1]−E[Y_{0i}|D_i=0] \\
&=E[Y_{1i}|D_i=1]−E[Y_{0i}|D_i=1] \\
&=E[Y_{1i}−Y_{0i}|D_i=1] \\
&=E[Y_{1i}−Y_{0i}]
\end{aligned}
$$

The first question to ask about a randomized experiment is whether the randomization successfully balanced subjects’ characteristics across the different treatment groups. To assess this, it’s common to compare pretreatment outcomes or other covariates across groups.

## 2.3 Regression Analysis of Experiments

Suppose that the treatment effect is the same for everyone, say $Y_{1i}−Y_{0i}=\rho$, a constant. With constant treatment effects, we can rewrite (2.1.1) in the form

$$
Y_i=\alpha+\rho D_i+\eta_i
$$

- $\alpha=E(Y_{0i})$
- $\eta_i=Y_{0i}-E(Y_{0i})$ is the random part of $Y_{0i}$