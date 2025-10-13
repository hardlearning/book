# CHAPTER 28 Mathematical Applications

## 28.1 THE BLACK-SCHOLES MODEL

$$
\begin{aligned}
& \text{Theoretical option price}=pN(d_1)-se^{-rt}N(d_2) \\
& d_1=\frac{\ln(\frac{p}{s})+(r+\frac{v^2}{2})t}{v\sqrt{t}} \\
& d_2=d_1-v\sqrt{t}
\end{aligned}
$$

The variables are:
- p = stock price
- s = striking price
- t = time remaining until expiration, expressed as a percent of a year
- r = current risk-free interest rate
- v = volatility measured by annual standard deviation
- ln = natural logarithm
- N(x) = cumulative normal density function

The delta is the amount by which the option price can be expected to change for a small change in the stock price. The delta is also known as the hedge ratio.

$$
\text{Delta} = N(d_1)
$$

The cumulative distribution can be approximated by a formula:

$$
\begin{aligned}
x &=1-z(1.330274y^5-1.821256y^4+1.781478y^3-0.356538y^2+0.3193815y) \\
y &=\frac{1}{1+0.2316419|\sigma|} \\
z &=0.3989423e^{-\sigma^2/2}
\end{aligned}
$$

Then $N(\sigma)=x$ if $\sigma>0$ or $N(\sigma)=1 -x$ if $\sigma<0$.

*Example*: Suppose that XYZ is trading at 45 and we are interested in evaluating the July 50 call, which has 60 days remaining until expiration. Furthermore, assume that the volatility of XYZ is 30% and that the risk-free interest rate is currently 10%.

$$
\begin{aligned}
t &=60/365=0.16438years \\
d_1 &=\frac{\ln(45/50)+(0.1+0.3^2/2)\times 0.16438}{0.3\times\sqrt{0.16438}}=-0.67025 \\
d_2 &=-0.67025-0.3\times\sqrt{0.16438}=-0.79189
\end{aligned}
$$

Now calculate the cumulative normal distribution function for $d_1$ and $d_2$, by referring to the above formulae:

$$
\begin{aligned}
& d_1=-0.67025 \\
& y=\frac{1}{1+0.2316419\times|-0.67025|}=0.86561 \\
& z=0.3989423e^{-(-0.67025)^2/2}=0.31868 \\
& x=0.74865
\end{aligned}
$$

Now, we can complete the calculation of the July 50 calls theoretical value:

$$
\begin{aligned}
& N(d_1)=N(-0.67025)=1-x=0.25134 \\
& N(d_2)=N(-0.79189)=0.21421 \\
& \text{value}=45\times N(d_1)-50\times e^{-0.1\times 0.16438}\times N(d_2)=0.7746
\end{aligned}
$$

#### CHARACTERISTICS OF THE MODEL

The model does not include dividends paid by the common stock. Thus, direct application of the model wall tend to give inflated call prices, especially on stocks that pay relatively large dividends. Fisher Black, one of the coauthors of the model, suggested the following method: Adjust the stock price to be used in the formula by subtracting, from the current stock price, the present worth of the dividends likely to be paid before maturity.

The model is based on a lognormal distribution of stock prices.


In the Black-Scholes model, volatility is defined as the annual standard deviation of the stock price. This is the regular statistical definition of standard deviation:

$$
\begin{aligned}
\sigma^2 &=\frac{\sum_{i=1}^n(P_i-P)^2}{n-1} \\
v &=\sigma/P
\end{aligned}
$$

- $P$ = average stock price of all $P_i$'s
- $P_i$ = daily stock price
- $n$ = number of days observed
- $v$ = volatility

When volatility is computed using past stock prices, it is called a historical volatility.

**Computing Lognormal Historical Volatility**

$$
v=\sqrt{\frac{\sum_{i=1}^n(X_i-\bar{X})^2}{n-1}}
$$

where $X_i=\ln(P_i/P_{i-1})$; $P_i$ = closing price on day i and $\bar{X}$ = the average of the $X_i$'s over the desired number of days.

So to compute a 10-day historical volatility, one would need 11 observations.

|Day|XYZ Stack|$P_i/P_{i-1}$|$X_i=\ln(P_i/P_{i-1})$|$(X_i-\bar{X})^2$|
|--|--|--|--|--|
|1|153.875| | | |
|2|153.625|0.9984|-0.0016|0.000020|
|3|151|0.9829|-0.0172|0.000405|
|4|146|0.9669|-0.0337|0.001336|
|5|144.125|0.9872|-0.0129|0.000250|
|6|147.25|1.0217|0.0215|0.000345|
|7|146.25|0.9932|-0.0068|0.000094|
|8|149.5|1.0222|0.0220|0.000365|
|9|152.5|1.0201|0.0199|0.000289|
|10|158.625|1.0402|0.0394|0.001332|
|11|158.375|0.9984|-0.0016|.000020|
| | | |AVG:0.0028825|$\sum$:0.004455|

$$
v=\sqrt{0.004455/9}=0.22249
$$

This is a 10-day volatility. To convert it into an annual volatility, we need to multiply by the square root of the number of trading days in a year. Since there are approximately 260 trading days in a year, the final volatility would be:

$$
v=0.22249\times\sqrt{260}=0.3587
$$

Thus, one could say that the volatility of XYZ is 36% on an annualized basis.

## 28.2 COMPUTING COMPOSITE IMPLIED VOLATILITY

The weighting factor for volume is merely that option's daily volume divided by the total option volume.

|Option|Volume|Volume Weighting Factor|
|--|--|--|
|January 30|50|0.25 (50/200)|
|January 35|90|0.45 (90/200)|
|April 35|55|0.275 (55/200)|
|April 40|5|0.025 (5/200)|
| |$\sum$ 200| |

The weighting functions for distance from the striking price should probably not be linear.

$$
\text{Weighting factor}\begin{cases}
=\frac{(x-a)^2}{a^2}&\quad\text{if x is less than a} \\
=0 &\quad\text{if x is greater than a}
\end{cases}
$$

where x is the percentage distance between stock price and strike price and a is the maximum percentage distance at which the modeler wants to give any weight at all to the option's implied volatility.

*Example*: An investor decides that he wants to discard options from the weighting criterion that have striking prices more than 25% from the current stock price. The variable, a, would then be equal to 0.25. The weighting factors, with XYZ at 33, could thus be computed as shown:

|Option|Distance from Stock Price|Distance Weighting Factor|
|--|--|--|
|January 30|0.091 (3/33)|0.41|
|January 35|0.061 (2/33)|0.57|
|April 35|0.061 (2/33)|0.57|
|April 40|0.212 (7/33)|0.02|

$$
\text{Composite implied volatility}=\frac{\sum(\text{Volume factor}\times\text{Distance factor}\times\text{Implied volatility})}{\sum(\text{Volume factor}\times\text{Distance factor})}
$$

|Option|Volume Factor|Distance Factor|Option's Implied Volatility|
|--|--|--|--|
|January 30|0.25|0.41|0.34|
|January 35|0.45|0.57|0.28|
|April 35|0.275|0.57|0.30|
|April 40|0.025|0.02|0.38|

$$
\text{Implied volatility}=\frac{{0.25}\times{0.41}\times{0.34}+{0.45}\times{0.57}\times{0.28}+{0.275}\times{0.57}\times{0.30}+{0.25}\times{0.02}\times{0.38}}{{0.25}\times{0.41}+{0.45}\times{0.57}+{0.275}\times{0.57}+{0.025}\times{0.02}}=0.298
$$

As markets become bullish or bearish (generating large rallies or declines), most stocks will react in a volatile manner as well. Option premiums expand rather quickly, and this method of implied volatility is able to pick up the change quickly.

On a day-to-day basis, the implied volatility for a stock—especially one whose options are not too active—may fluctuate more than the strategist would like. A smoothing effect can be obtained by taking a moving average of the last 20 or 30 days'implied volatilities.

An alternative that does not require the saving of many previous days' worth of data is to use a momentum calculation on the implied volatility. For example, today's final volatility might be computed by adding 5% of today's implied volatility to 95% of yesterday's final volatility.

Once this implied volatility has been computed, it can then be used in the Black- Scholes model (or any other model) as the volatility variable.

There will be a discrepancy between the option's actual closing price and the theoretical price as computed by the model. This differential represents the amount by which the option is theoretically overpriced or underpriced, compared to other options on that same stock.

#### Computing a Volatility Skew

1. Calculate the individual implied volatility of each option.
2. Calculate the standard deviation of the series in step 1. Note that one may want to eliminate options that are essentially trading with little or no time value premium from this standard deviation calculation, since they are not representative of the "normal" options on this stock.
3. Divide the result of step 2 by the composite implied volatility.

*Example*: XYZ is trading at 6.50. It has several listed options, with various individual implied volatilities.

|Option|Implied Volatility|
|--|--|
|Mar 5 call|85%|
|June 5 call|77.5%|
|Mar 7.5 call|75%|
|June 7.5 call|70.0%|

The standard deviation of these four numbers is 6.25%. Assuming that the composite implied volatility of the above four options is 75.0%, the "skew factor" for this stock on this day would be:

$$
\text{Skew factor}=6.25/75.0=8.3%
$$

If an "event" (FDA hearing, lawsuit rerdict, earnings report, etc.) is due, that might cause a horizontal skew—where the implied volatilities of the options expiring just after the anticipated event are more expensive than all other options. Conversely, in a bearish market, there might be a vertical skew, where options at lower strikes have higher implied volatilities than options at higher strikes.

## 28.3 EXPECTED RETURN

The expected return is nothing more than the return that the position should yield over a large number of cases.

*Example*: XYZ is selling at 33, and an investor is interested in determining where XYZ will be in 6 months. Assume that there is a 20% chance of XYZ being below 30 in 6 months, and that there is a 40% chance that XYZ will be above 35 in 6 months. Finally, assume that XYZ has an equal 10% chance of being at 31, 32, 33, or 34 in 6 months.

Now suppose a February 30 call is trading at 4 and a February 35 call is trading at 2 points. A bull spread could be established by buying the February 30 and selling the February 35. This position would cost 2 points. The spreader could make 3 points if XYZ were above 35 at expiration for a return of 150%, or he could lose 100% if XYZ were below 30 at expiration.

The expected return for this spread can be computed by multiplying the outcome at expiration for each price by the probability of being at that price, and then summing the results.

|XYZ Price at Expiration|Chance of XYZ Being at That Price (A)|Profit at That Price (B)|Expected Profit: (A)x(B)|
|--|--|--|--|
|Below 30|20%|-200|-40|
|31|10%|-100|-10|
|32|10%|0|0|
|33|10%|+100|+10|
|34|10%|+200|+20|
|Above 35|40%|+300|+120|
| | |Total expected profit|$100|

The expected return (profit divided by investment) is 50% ($100/$200).


Since the option modeler is generally interested in time periods other than one year, the annual volatility must be converted into a volatility for the time period in question.

$$
v_i=v\sqrt{t}
$$

- $v$ = annual volatility
- $t$ = time, in years
- $v_t$ = volatility for time, t.

As an example, a 3-month volatility would be equal to one-half of the annual volatility. In this case, t would equal 0.25 (one fourth of a year), so $v_{0.25} = v\sqrt{0.25} = 0.5v$.

Probability of stock being below price q at end of time period t:

$$
P(\text{below})=N\left(\frac{\ln(\frac{q}{p})}{v_t}\right)
$$

- N = cumulative normal distribution
- p = current price of the stock
- q = price in question
- ln = natural logarithm for the time period in question.

The probability of the stock being above the given price is

$$
P(\text{above})=1-P(\text{below})
$$

The following iterative equation would be used.

$$
P(\text{of being at price x})=P(\text{below x})-P(\text{below y})
$$

where y is close to but less than x in price.

*Example*: XYZ is currently at 33 and has an annual volatility of 25%. The bull spread is being established (buy the February 30 call and sell the February 35 call for a 2-point debit) and these are 6-month options.

|Price at Expiration (q)|(A) P(below q)|(B) P(of being at q)|(C) Profit on Spread|
|--|--|--|--|
|30|0.295|0.295|-200|
|30.1|0.301|0.006|-190|
|30.2|0.308|0.007|-180|
|30.3|0.316|0.008|-170|
|$\vdots$|$\vdots$|$\vdots$|$\vdots$|

1. Column (A) is computed according to the previously given formula:
    $$
    \begin{aligned}
    & p=33, v_t=0.25\sqrt{1/2}=0.177 \\
    & P(\text{below 30})=N(\ln(30/33)/0.177)=0.295 \\
    & P(\text{below 30.1})=N(\ln(30.1/33)/0.177)=0.301 \\
    & P(\text{below 30.2})=N(\ln(30.2/33)/0.177)=0.308 \\
    & P(\text{below 30.3})=N(\ln(30.3/33)/0.177)=0.316
    \end{aligned}
    $$
    The calculations would be performed for each tenth of a point (十分之一) up through a price of 35.
2. Column (B) is determined by subtracting successive numbers in column (A).
    $$
    \begin{aligned}
    & P(\text{of being at price 30.1})=P(\text{below 30.1})-P(\text{below 30})=0.006 \\
    & P(\text{of being at price 30.2})=P(\text{below 30.2})-P(\text{below 30.1})=0.007 \\
    & P(\text{of being at price 30.3})=P(\text{below 30.3})-P(\text{below 30.2})=0.008
    \end{aligned}
    $$
3. The first stock price is 30, since all results for the bull spread are equal below that price — a 100% loss on the spread.
4. The expected return is computed by multiplying the two right-hand columns, (B) and (C), and summing the results.

## 28.4 APPLYING THE CALCULATIONS TO STRATEGY DECISIONS

### 28.4.1 CALL WRITING

He knows the downside break-even point at expiration in each write. Therefore, the probability of the stock being below that break-even point at expiration can be computed quickly. His final list would rank those writes with the least chance of being below the break-even point at expiration as the best writes.

*Example*: XYZ is selling for 43 and a 6-month July 40 call is selling for 8 points. After including dividends and commission costs for a 500-share position, the downside break-even point at expiration is 36. If the annualized volatility of XYZ is 25%, the probability of making money at expiration can be computed.

$$
\begin{aligned}
&v_{6-month}=0.25*\sqrt{1/2}=0.177 \\
&P(below 36 in 6 months)=N(\frac{\ln(36/43)}{0.177})=0.158
\end{aligned}
$$

The expected probability of XYZ being below 36 in 6 months is 15.8%. Therefore, this would be an attractive write on a conservative basis, because it has a nearly 85% probability of making money.

### 28.4.2 CALL BUYING

The exact steps to be followed in the analysis of profitability and risk can be listed as follows:

1. Specify the distance that underlying stock can move, up or down, in terms of its volatility.
2. Select the holding period over which the analysis is to take place.
> PROFITABILITY
3. Calculate the stock price that the stock would move up to, when the foregoing assumptions are implemented.
4. Using a pricing model, such as the Black-Scholes model, estimate what the option price would become after the upward stock movement.
5. Calculate the percent profit, after deducting commissions.
6. Repeat steps 4 and 5 for each option on the stock.
> RISK
7. Calculate the stock price that the stock could fall to, when the assumptions in steps 1 and 2 are applied.
8. With a model, price the option after the stock's decline.
9. Calculate the percentage loss after commissions.
10. Compute a reward/risk ratio: Divide the percentage profit from step 5 by the percentage risk from step 9.
11. Repeat steps 8 through 10 for each option on the stock.

*Example*: Steps 1 and 2: Suppose an investor wants to look at option purchases for a 90-day holding period, under the assumption that each stock could move up by one standard deviation in that time. (There is only about a 16% chance that a stock will move more than one standard deviation in one direction in a given time period.) Furthermore, assume that the following data are known:

- XYZ common, 41;
- XYZ volatility, 30% annually;
- XYZ January 40 call, 4; and
- time to January expiration, 6 months

Step 3: Calculate upward stock potential. This is accomplished by the following formula:

$$
q=p\cdot e^{a\cdot v_t}
$$

- p = current stock price
- q = potential stock price
- $v_t$ = volatility for the time period, t
- a = a constant (see below).

The first constant, a, is the number of standard deviations of movement to be allowed. In our example, a = 1. The second constant, t, is 0.25, since the analysis is for a 90-day holding period, which is 25% of a year. In this example:

$$
\begin{aligned}
&v_t=0.3\times\sqrt{0.25}=0.15 \\
&q=41\times e^{0.15}=47.64
\end{aligned}
$$

Thus, this stock would move up to approximately 47.64 if it moved one standard deviation in exactly 90 days.

Step 4: Using the Black-Scholes model, the XYZ January 40 call can be priced. It would be worth approximately 8.10 if XYZ were at 47.60 and there were 90 days’ less life in the call.

Step 5: Calculate the profit potential. For this example, commissions will be ignored, but they should be included in a real-life situation.

$$
\text{Percents profit}=\frac{8.10-4}{4}=103\%
$$

Thus, if XYZ stock moves up by one standard deviation over the next 90 days, this call would yield a projected profit of 103%.

Step 6 is omitted from this example. It would consist of performing a similar profit analysis (steps 4 and 5) on all other XYZ options, with the assumption that XYZ is at 47.60 after 90 days.

Step 7: Calculate the downside potential of XYZ. The formula for the downside potential of the stock is nearly the same as that used in step 3 for the upside potential:

$$
\begin{aligned}
q&=p\cdot e^{-a\cdot v_t} \\
&=41\times e^{-0.15}=35.39
\end{aligned}
$$

XYZ would fall to approximately 35.39 in 90 days if it fell by one standard deviation.

Step 8: Using the Black-Scholes model, one could estimate that the XYZ January 40 call would be worth about 1.10 if XYZ were at 35.39 in 90 days.

Step 9: The risk potential in the January 40 call would be:

$$
\text{Percent risk}=\frac{4-1.10}{4}=73\%
$$

Step 10: The reward/risk ratio is merely the percentage reward divided by the percentage risk:

$$
\text{Reward/risk ratio}=\frac{103\%}{73\%}=1.41
$$

Step 11: This analysis would be repeated for all XYZ options, and then for all other optionable stocks. The less aggressive call purchases would be ranked by their reward/risk ratios, with higher ratios representing more attractive purchases. More aggressive purchases would be ranked by the potential rewards only (step 5).

It should be noted that the assumption of ranking the purchases after one full standard deviation movement by the underlying stock is probably excessive. A more moderate assumption would be that the stock might be able to move 0.7 standard deviation. There is about a 25% expected chance that a stock could move up at least 0.7 standard deviation at the end of a fixed time period.

### 28.4.5 PRICING A PUT OPTION

One could use the basic call pricing model for the purpose of predicting put prices if he assumes that arbitrageurs will efficiently influence the market via conversions.

The listed put's price can be estimated by using the call pricing model and the arbitrage formula. Recall that the arbitrageur must include the cost of carrying the position (持有成本) as well as the dividends (股息) to be received.

$$
\text{Theoretical put}=\text{Theoretical call price}+\text{Strike price}-\text{Stock price}-\text{Carrying cost}+\text{Dividends}
$$

The "theoretical call price" is obtained from the Black-Scholes model. The carrying cost is the cost of money (interest rate利率) times the striking price, multiplied by the time to expiration.

If XYZ were at 41 and a 6-month January 40 call option were valued at 4 points by the Black-Scholes model, the theoretical put price could be estimated. Assume that the cost of money interest rate is 10% annually, and that the stock will pay $0.50 in dividends in 6 months (t = 1/2 year).

$$
\text{Theoretical put price}=4+40-41-(0.1\times 40\times\frac{1}{2})+0.5=1.50
$$

This means that if the call could be sold for 4 points, the arbitrageur would be willing to pay up to 1.50 points for the put to establish a conversion. The arbitrageur's price is used as the theoretical listed put price estimate.

### 28.4.6 PUT BUYING

The pricing of the put necessary for steps 4 and 8 is done in accordance with the arbitrage model just presented.

The synthetic put (合成看跌期权) pricing formula that would be used in steps 4 and 8 of the option buying analysis is exactly the same as the arbitrage model for listed puts, except that the carrying costs are omitted:

$$
\text{Theoretical synthetic put price}=\text{Theoretical call price}+\text{Strike price}-\text{Stock price}+\text{Dividends}
$$

When the customer buys a synthetic put, he must advance the full cost of the dividend, but receives no offsetting cost reduction for the credit being earned by the short stock position. (他必须事先付出股息的全部成本，但在卖空股票头寸得到的收入里，得不到降低成本的对冲) Consequently, synthetic puts are always more expensive, on a relative basis, than are listed puts.

### 28.4.7 CALENDAR SPREADS

A neutral calendar spread is selling a near-term call and buying a longer-term call, when the stock is relatively close to the striking price of the calls. The neutral calendar spread is normally closed when the near-term option expires.

1. The maximum profit potential of the spread

    To determine the maximum profit potential of the spread, assume that the near-term call expires worthless and use the pricing model to estimate the value of the longer-term call with the stock exactly at the striking price. Since commission costs are relatively large in spread transactions, it would be best to have the computations include commissions.

2. The profit if unchanged

    To determine how much profit would be made if the stock were unchanged at near-term expiration, assume that the spread is closed with the near-term call equal to its intrinsic value (zero if the stock is currently below the strike, or the difference between the stock price and the strike if the stock is initially above the strike). Then use the pricing model to estimate the value of the longer-term call, which will then have three or six months of life remaining, with the stock unchanged. The resulting differential between the near-term call's intrinsic value and the estimated value of the longer-term call is an estimate of the price at which the spread could be liquidated. The profit, of course, is that differential minus the current (initial) differential, less commissions.

3. Break-even points of the position at near-term expiration

    There is both an upside break-even point and a downside break-even point at near-term expiration. These break-even points can be estimated with the use of the pricing model. One method of determination involves estimating the liquidating value (平仓价值) of the spread at successive stock prices. When the liquidating value is found to be equal to the initial value, plus commissions, a break-even point has been located.

    *Example*: If the spread in question is using options with a striking price of 30, one would begin his break-even point calculations at a price of 30. Estimate the liquidating value of the spread at 30, 29.90, 29.80, 29.70, and so forth until the break-even point is found. Once the downside break-even point has been determined in this manner, the iterations to locate the upside break-even point should begin again at the striking price. Thus, one would evaluate the liquidating value at 30, 30.10, 30.20, and so on.

4. The theoretical value of the spread

    Recompute the estimated value of both the near-term and longer-term calls at the current time and stock price, using the implied volatility for the underlying stock. The resultant differential between the two estimated call prices may differ substantially from the actual differential. One would want to establish spreads in which the theoretical differential is greater than the actual differential.

The logical method of ranking the spreads is by their return if unchanged. The spreads with the highest return if unchanged at near-term expiration are those in which the stock price and striking price were close together initially, a basic requirement of the neutral calendar spread. More complicated ranking systems should try to include the theoretical value of the spread and possibly even the maximum potential of the spread.

### 28.4.8 RATIO STRATEGIES

Ratio strategies involve selling naked options. Therefore, the strategist has potentially large risk, either to the upside or to the downside or both. The formulae for determining the probability of a stock being above or below a certain price at some time in the future can give him the probabilities of this risk.

If the volatility increases, the expected return of a ratio position will drop, because the probabilities of the stock moving outside the profit range will increase, thereby increasing the probability of loss.

The effect of a changing volatility can be counteracted by continuing to monitor the position daily after it has been established.

## 28.5 FACILITATION OR INSTITUTIONAL BLOCK POSITIONING

The hedge ratio is the delta of the option —  the amount by which the option will change in price for small changes in the stock price.

By selling the correct number of calls against his stock purchase, the block trader will have a neutral position. This position would, in theory, neither gain nor lose for small changes in the stock price. He is therefore buying himself time until he can unwind the position in the open market. (在头寸平仓前，他赢得了时间)

*Example*: A trader buys 10,000 shares of XYZ, and a January 30 call is trading with a hedge ratio of 0.50. To have a neutral position, the trader should sell options against 20,000 shares of stock (10,000 divided by 0.50 equals 20,000). Thus, he should sell 200 of the January 30’s. In this sample position, if the stock moves up by 1 point, the option should move up by 50 cents. The trader would make $10,000 on his stock position and would lose $10,000 on his 200 short options.

In actual practice, this hedge ratio may not work exactly, because it tends to change constantly as the stock price changes. If the trader finds the stock moving more than fractionally (股票运动超过一个点), he may have to add more calls or buy some in, to maintain a neutral hedge ratio.

A similar hedge can be established by the block trader who sells stock to accommodate a customer buy order. He could buy calls in accordance with the hedge ratio, to set up a neutral position.

### THE NEUTRAL SPREAD

If the hedge ratios of two options are known, the neutral ratio is determined by dividing the two hedge ratios.

*Example*: An XYZ January 35 has a hedge ratio of 0.25, and an XYZ January 30 has a hedge ratio of 0.50, so a neutral ratio would be 2:1 (0.50 divided by 0.25). That is, one would sell 2 January 35's against one long January 30, or, conversely, would buy 2 January 35's against one short January 30. (卖出2手一月35每买入1手一月30，或者买入2手一月35每卖出1手一月30)

A ratio spread consists of buying options at a certain strike, and selling more options further out-of-the-money. The hedge ratios can be used by the trader to initially establish a neutral position. Perhaps more important, the hedge ratio can also be used as a follow up action to keep the position neutral after the stock changes in price.

*Example*: The purchase of 15 January 30 calls and the sale of 30 January 35 calls — a ratio call spread — may be a position taken for profit potential. It would be a neutral position if the deltas were 0.60 and 0.30. This spread would do best if the stock were at exactly 35 at expiration. However, if the stock rose quickly before expiration, the spread ratio would decrease from 2:1 to perhaps 3:2. If the trader wants to balance his position, he could buy 5 more January 30’s, giving him a total of 20 long versus the 30 short January 35's that he originally sold. If this stock declines, the neutral ratio might be 3:1. In that case. 15 more January 35's could be sold, making the position short 45 calls versus 15 long calls, which would produce the neutral 3:1 ratio.

By monitoring the spread using the hedge ratio, the trader may also be able to discern whether he has established too bullish or too bearish a position. (过于看多或过于看空)

*Example*: The trader starts with the example described above — long 15 January 30 calls and short 30 January 35 calls — when the hedge ratios were 0.60 and 0.30, respectively. Some later time, the stock falls to 27. The hedge ratios may have become 0.42 for the January 30 and 0.14 for the January 35, indicating that a 3:1 ratio would be neutral (0.42/0.14 = 3). He now has a bullish position, because his 2:1 ratio is less than the neutral 3:1 ratio. If the trader's ratio is greater than the neutral ratio (2:1 vs. 3:2, for example), he is bearishly positioned.

## 28.6 AIDING IN FOLLOW-UP ACTION

The computation for determining whether a position is net short or net long (净空头或净多头) generally involves calculating the "equivalent stock position" (ESP等股头寸). If one owns 10 calls that have a delta of 0.45, his equivalent stock position from those calls is 10 x 100 shares per call x 0.45 = 450. That is, owning those 10 calls is equivalent to owning 450 shares of the underlying stock.

*Example*: The following position exists when XYZ is at 31.75. It is essentially a backspread combined with a reverse ratio write.

|Position| |Delta|ESP| |
|--|--|--|--|--|
|Short|4,500 XYZ|1.00|ESP|4,500 shares|
|Short|100 XYZ April 25 calls|0.89|Short|8,900 shares|
|Long|50 XYZ April 30 calls|0.76|Long|3,800 shares|
|Long|139 XYZ July 30 calls|0.74|Long|10,286 shares|
| |Total ESP| |Long|686 shares|
|Total money in position|$163,500 credit| | | |

The computer uses the stock’s volatility to project stock prices 30 days in the future. Seven stock prices are shown in the next table.

|Stock Price in 30 Days|Standard Deviations|Expected Results|
|--|--|--|
|35.90|+1.5|+15,847|
|34.10|+1.0|+12,355|
|32.90|+0.5|+10,097|
|31.75|0.0|+9,443|
|30.60|-0.5|+10,743|
|29.50|-1.0|+14,172|
|28.50|-1.5|+19,605|
|Expected profit| |+$11,426|

If the current mark to market of this position were in excess of $11,426, then he should consider removing the position, since it would be more profitable than the expected profit.
