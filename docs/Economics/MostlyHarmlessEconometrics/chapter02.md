# Chapter 2 The Experimental Ideal

## 2.1 The Selection Problem

We can think about hospital treatment as a binary random variable, $D_i=\{0,1\}$. ($D_i$表示实际是否接受医院院治疗) The outcome of interest, a measure of health status, is denoted by $Y_i$. ($Y_i$表示健康水平) The question is whether $Y_i$ is affected by hospital care.

Hence, for any individual there are two potential health variables:

$$
\text{Potential outcome}=
\begin{cases}
Y_{1i} & \mathrm{if}\quad D_i=1 \\
Y_{0i} & \mathrm{if}\quad D_i=0
\end{cases}
$$

$Y_{0i}$ is the health status of an individual had he not gone to the hospital, irrespective of whether he actually went, while $Y_{1i}$ is the individual’s health status if he goes. ($Y_{0i}$是假设一个人不接受医院治疗的健康状况，$Y_{1i}$是假设一个人接受医院治疗的健康状况。)

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

This notation is useful because $Y_{1i}-Y_{0i}$ is the *causal effect* (因果效应) of hospitalization for an individual.

The comparison of average health conditional on hospitalization status is formally linked to the average causal effect by the equation:

$$
\underbrace{E[Y_i|D_i=1]-E[Y_i|D_i=0]}_{\text{Observed difference in average health}}=\underbrace{E[Y_{1i}|D_i=1]-E[Y_{0i}|D_i=1]}_{\text{Average treatment effect on the treated}}+\underbrace{E[Y_{0i}|D_i=1]-E[Y_{0i}|D_i=0]}_{\text{Selection bias}}.
$$

The term $E[Y_{1i}|D_i=1]−E[Y_{0i}|D_i=1]=E[Y_{1i}−Y_{0i}|D_i=1]$ is the *average causal effect* (平均因果效应) of hospitalization on those who were hospitalized. This term captures the averages difference between the health of the hospitalized, $E[Y_{1i}|D_i=1]$ (接受医院治疗的人的健康水平), and what would have happened to them had they not been hospitalized, $E[Y_{0i}|D_i=1]$ (接受了医院治疗的人假设没有得到治疗，他们的平均健康水平).

Selection bias is the difference in average $Y_{0i}$ between those who were and those who were not hospitalized. (选择性偏误是接受医院治疗与不接受医院治疗的人假设没有被治疗时的健康状况的平均差异)

Because the sick are more likely than the healthy to seek treatment, those who were hospitalized have worse values of $Y_{0i}$, making selection bias negative in this example.

## 2.2 Random Assignment Solves the Selection Problem

*Random assignment* (随机分配) of $D_i$ solves the selection problem because random assignment makes $D_i$ independent of potential outcomes.

$$
\begin{aligned}
E[Y_i|D_i=1]−E[Y_i|D_i=0]&=E[Y_{1i}|D_i=1]−E[Y_{0i}|D_i=0] \\
&=E[Y_{1i}|D_i=1]−E[Y_{0i}|D_i=1]
\end{aligned}
$$

where the independence of $Y_{0i}$ and $D_i$ allows us to swap $E[Y_{0i}|D_i=1]$ for $E[Y_{0i}|D_i=0]$ in the second line.

$$
\begin{aligned}
E[Y_{1i}|D_i=1]−E[Y_{0i}|D_i=1]&=E[Y_{1i}−Y_{0i}|D_i=1] \\
&=E[Y_{1i}−Y_{0i}]
\end{aligned}
$$

The effect of randomly assigned hospitalization on the hospitalized is the same as the effect of hospitalization on a randomly chosen patient. (接受医院治疗的人的因果效应等于随机分配患者进行治疗的因果效应) The main thing is that random assignment of di eliminates selection bias.

The STAR experiment demonstrates the relationship between class size (课堂规模) and student learning (学生成绩). The study ran for four years and involved about 11,600 children. The experiment assigned students to one of three treatments: small classes (小班) with 13–17 children, regular classes (普通班级) with 22–25 children and a part-time teacher’s aide (the usual arrangement), or regular classes with a full-time teacher’s aide.

The first question to ask about a randomized experiment is whether the randomization successfully balanced subjects' characteristics across the different treatment groups. (随机化是否成功地平衡了不同处理组间的各种特征) To assess this, it's common to compare pretreatment outcomes or other covariates across groups. (比较处理之前的结果或者在组间比较不被处理过程影响但是影响被试者的变量)

## 2.3 Regression Analysis of Experiments

Suppose that the *treatment effect* (因果效应) is the same for everyone, say $Y_{1i}−Y_{0i}=\rho$, a constant. With constant treatment effects, we can rewrite (2.1.1) in the form

$$
Y_i=\underbrace{\alpha}_{E(Y_{0i})}+\underbrace{\rho}_{(Y_{1i}−Y_{0i})}D_i+\underbrace{\eta_i}_{Y_{0i}-E(Y_{0i})} \quad (2.3.1)
$$

$\eta_i$ is the random part of $Y_{0i}$. Evaluating the conditional expectation of this equation with treatment status switched off and on gives

$$
\begin{aligned}
&E[Y_i|D_i=1]=\alpha+\rho+E[\eta_i|D_i=1] \\
&E[Y_i|D_i=0]=\alpha+E[\eta_i|D_i=0] \\
&E[Y_i|D_i=1]-E[Y_i|D_i=0]=\underbrace{\rho}_{\text{Treatment effect}}+\underbrace{E[\eta_i|D_i=1]-E[\eta_i|D_i=0]}_{\text{Selection bias}}
\end{aligned}
$$

Thus, selection bias amounts to correlation between the regression error term, $\eta_i$, and the regressor, $D_i$. Since

$$
E[\eta_i|D_i=1]-E[\eta_i|D_i=0]=E[Y_{0i}|D_i=1]-E[Y_{0i}|D_i=0]
$$

this correlation reflects the difference in (no-treatment) potential outcomes between those who get treated and those who don't. (上面等式反映了得到处理和没得到处理的人的潜在结果的差别)

The other controls in Krueger's table describe student characteristics such as race, age, and free lunch status. If these controls, call them $X_i$, are uncorrelated with the treatment $D_i$, then they will not affect the estimate of $\rho$. In other words, estimates of $\rho$ in the long regression,

$$
Y_i=\alpha+\rho D_i+X_i^\prime\gamma+\eta \quad (2.3.2)
$$

will be close to estimates of $\rho$ in the short regression, (2.3.1).

Although the control variables, $X_i$, are uncorrelated with $D_i$, they have substantial explanatory power for $Y_i$. Including these control variables therefore reduces the *residual variance* (残差的方差), which in turn lowers the standard error of the regression estimates.