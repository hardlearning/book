# CHAPTER 40 Advanced Concepts

## 40.1 NEUTRALITY

Neutrality, as it applies to option positions, means that one is noncommittal with respect to at least one of the factors that influence an option's price. Simply put, this means that one can design an option position in which he can profit, no matter which way the underlying security moves.

Often, when one constructs a neutral strategy, he is neutral with respect to price changes in the underlying security. It is also possible to be neutral with respect to the rate of price change of the underlying security, with respect to the volatility of the security, or with respect to time decay.

## 40.2 THE "GREEKS"

### 40.2.1 delta

The term delta is commonly used in at least two different contexts: to express the amount by which an option changes for a 1-point move in the underlying security, or to describe the equivalent stock position of an entire option portfolio.

*Example*: Assume an XYZ January 50 call has a delta of 0.50 with XYZ at a price of 49. This means that the call will move 50% as fast as the stock will move. So, if XYZ jumps to 51, a gain of 2 points, then the January 50 call can be expected to increase in price by 1 point.

In another context, the delta of a call is often thought of as the probability of the call being in-the-money at expiration. That is, if XYZ is 50 and the January 55 call has a delta of 0.40, then there is a 40% probability that XYZ will be over 55 at January expiration.

The low-volatility stock's in-the-money options have the higher delta. The high-volatility stock's out-of-the-money options have the higher delta.

- Delta comparison for different volatilities with XYZ = 50 and time = 3 months.

|Strike|Low-Volatility Stock's Delta|High-Volatility Stock's Delta|
|--|--|--|
|40|100|94|
|45|93|78|
|50|51|53|
|55|11|29|
|60|1|13|
|65|0|5|

The shorter-term in-the-money options have the higher delta. This is because they have the least time value premium. The longer-term out-of-the-money options have the higher deltas, since these options have the most time value premium.

- Delta comparison — varying time remaining with XYZ = 50.

|Strike Price|t = 1 year|t = 6 months|t = 3 months|
|--|--|--|--|
|40|92|97|99|
|45|79|83|90|
|50|61|57|55|
|55|41|30|18|
|60|25|12|3|
|65|14|4|0|

Note that the delta of a longer-term at-the-money option is larger than that of a shorter-term option. In fact, the delta shrinks more rapidly as expiration draws nearer.

#### Position Delta

The position delta is computed according to the following simple equation:

$$
\text{Position delta}=\text{Option's delta}\times\text{Shares per option}\times\text{Option quantity}
$$

For futures options, the term "shares per option" would be replaced by "shares per contract." which is always 1.

*Example*: The following position exists when XYZ is at 31.75.

|Position|Delta|Position Delta|
|--|--|--|
|Short 4,500 XYZ|1.00|-4,500|
|Short 100 XYZ April 25 calls|0.89|-8,900|
|Long 50 XYZ April 30 calls|0.76|+3,800|
|Long 139 XYZ July 30 calls|0.74|+10,286|
||Total ESP:|+686|

This position has some exposure to the market since it is delta long. If the position delta were zero, it would be referred to as being delta neutral and would have no exposure to the market at that time.

### 40.2.2 GAMMA

The gamma is how fast the delta changes with respect to changes in the underlying stock price.

*Example*: With XYZ at 49, assume the January 50 call has a delta of 0.50 and a gamma of 0.05. If XYZ moves up one point to 50, the delta of the call will increase by the amount of the gamma: It will increase from 0.50 to 0.55.

Conceptually, a deeply in-the-money or deeply out-of-the-money option has a gamma of nearly zero. This implies that the delta of a deep in- or deep out-of-the-money option does not change very much at all, even if the stock moves by one point.

At-the-money options on less volatile securities will have higher gammas than similar options on more volatile securities. The following example demonstrates this fact.

*Example*: Assume XYZ is at 49, as is ABC. Moreover, XYZ is a more volatile stock (30% implied) as compared to ABC (20%). Then, similar options on the two stocks would have significantly different gammas.

|Option|XYZ Gammas<br>(Volatility=30%)|ABC Gammas<br>(Volatility = 20%)|
|--|--|--|
|January 50|0.066|0.097|
|January 55|0.045|0.039|
|January 60|0.019|0.0053|
|February 50|0.055|0.081|
|February 60|0.024|0.011|

Note that the at-the-money options (January 50's and February 50's) on ABC, the less volatile stock, have larger gammas than do their XYZ counterparts. However, look one strike higher (January 55's), and notice that the more volatile options have a slightly higher gamma. Look two strikes higher and the more volatile options have a vastly higher gamma, both for the January 60's and the February 60's.

Since the stock is not volatile, buyers are not willing to pay much time premium for the option. As a result, the gamma is high as well, because as the stock moves into-the-money, the increase in delta will be more dramatic than it would be for a volatile stock.

Since the nonvolatile stock will have difficulty moving fast enough to reach an out-of-the-money striking price, the delta of the out-of-the-money option is small and it will not change quickly (that is, the gamma is small also).

The gamma of the underlying security itself is zero. This is true because the delta of the underlying security (which is always 1.0) never changes — hence the gamma is zero.

*Example*: The following position exists when XYZ is at 31.75.

|Position|Option Delta|Position Delta|Option Gamma|Position Gamma|
|--|--|--|--|--|
|Short 4,500 XYZ|1.00|-4,500|0.0000|0|
|Short 100 XYZ April 25 calls|0.89|-8,900|0.0100|-100|
|Long 50 XYZ April 30 calls|0.76|+3,800|0.0300|+150|
|Long 139 XYZ July 30 calls|0.74|+10,286|0.0200|+278|
||Total|+686||+328|

The position has a positive gamma of over 300 shares. This means that the delta can be expected to change by 328 shares for each point that XYZ moves: If it moves up 1 point, the delta will increase to +1,014 (the current delta, 686, plus the gamma of 328). However, if XYZ moves down by 1 point, then the delta will decrease to +358 (the current delta, 686, less the gamma of 328).

### 40.2.3 VEGA OR TAU

Vega is the amount by which the option price changes when the volatility changes. Vega is always expressed as a positive number, whether it refers to a put or a call.

Example: Assume XYZ is at 49, and the January 50 call is selling for 3.50. The vega of the option is 0.25, and the current volatility of XYZ is 30%. If the volatility increases by one percentage point or 1% to 31%, then the vega indicates that the option will increase in value by 0.25, to 3.75. If the volatility had instead decreased by 1 percent to 29%, then the January 50 call would have decreased to 3.25 (a loss of 0.25, the amount of the vega).

Vega can refer to the option itself ("option vega") or to the position as a whole ("position vega"). Since vega is expressed as a positive number, if one is long options, then his position vega will be positive. This means he has exposure if volatilities decrease, or can make money if volatilities increase.

*Example*: Again, assume that we have the same backspread position as before, with XYZ at 31.75.

|Position|Option Vega|Position Vega|
|--|--|--|
|Short 4,500 XYZ|0.00|0|
|Short 100 XYZ April 25 calls|0.02|-200|
|Long 50 XYZ April 30 calls|0.05|+250|
|Long 139 XYZ July 30 calls|0.07|+973|
|Total Vega:||+1,023|

The vega is a positive 10.23 points ($1,023 since each point for these equity options is worth $100). The fact that the position has a positive vega means that it is exposed to variations in volatility. If volatility decreases, the position will lose money: $1,023 for each one percentage point decrease in volatility. However, if volatility increases, the position will benefit.

Vega is greatest for at-the-money options and approaches zero as the option is deeply in- or out-of-the-money. Again, this is common sense, since a deep in- or out-of-the-money option will not be affected much by a change in volatility. In addition, for at-the-money options, longer-term options have a higher vega than short-term options.

### 40.2.4 THETA

Theta measures the time decay of a position.

Theta is generally expressed as a negative number, and it is expressed as the amount by which the option value will change. Thus, if an option has a theta of -0.12, that means the option will lose 12 cents, or about an eighth of a point, per day.

At-the-money Short-term options have the largest absolute theta.

The theta of options on a highly volatile stock will be higher than the theta of options on a low-volatility stock.

*Example*: With XYZ at 49, the strategist has the following position in February, so that the April calls are nearer to expiration than the July calls. This position is similar to a large calendar spread position.

|Position|Option Theta|Position Theta|
|--|--|--|
|Short 4,000 XYZ|0.00|0|
|Short 150 XYZ April 50 calls|-0.04|+600|
|Long 150 XYZ April 30 calls|-0.02|-300|
|Short 78 XYZ July 30 puts|-0.02|+156|
|Total Theta:||+456|

This position is expected to make $456 per day due to time decay. Note that short options, whether puts or calls, have a positive position theta, while long options have a negative position theta.

### 40.2.5 RHO

Rho is the name given to the price change of an option's value due to a change in interest rates.

As interest rates rise, call prices will rise, but put prices will fall. The opposite is true as well: As interest rates fall, call prices decline and put prices rise.

Rho is expressed as a positive number for calls and a negative one for puts. Rho is smallest for deeply out-of-the-money options and is large for deeply in-the-money options. It is larger for longer-term options and is nearly zero for very short-term options.

Example: With XYZ at 49, the following options have the rho indicated (January is the near-term expiration):

|Month/Strike|Call Rho|Put Rho|
|--|--|--|
|January 35|0.05|-0.01|
|January 50|0.03|-0.03|
|January 60|0.00|-0.05|
|July 35|0.18|-0.02|
|July 50|0.14|-0.15|
|July 60|0.07|-0.18|

Note that the in-the-money calls (35 strike) have larger rho than the out-of-the-money 60's, in both January and July. Similarly, the in-the-money puts (the 60's) have larger rho on an absolute basis than the out-of-the-money 35's. Again, this is true for both January and July.

### 40.2.7 SUMMARY

Delta: Positive delta indicates that a position is currently bullish; if the underlying security goes up in price, the position should make money. A negative delta indicates a bearish slant.

Gamma: Positive gamma means that the delta will increase if the underlying security rises in price. Positive gamma generally implies that there is a preponderance of long options in the position, either puts or calls; negative gamma indicates written or naked options in the position.

Theta: Negative theta means that the position will lose money as time passes (typical of positions with long options); positive theta implies that time is working for the position (positions with written options).

Vega: Positive vega means that an increase of (perceived) volatility will benefit the position — usually true of positions with long options in them; negative vega means that a decrease of volatility would be beneficial.

## 40.3 STRATEGY CONSIDERATIONS: USING THE "GREEKS"

General risk exposure of common strategies.

|Strategy|Delta|Gamma|Theta|Vega|Rho|
|--|--|--|--|--|--|
|Buy stock|+|0|0|0|0|
|Sell stock short|-|0|0|0|0|
|Call buy|+|+|-|+|+|
|Put buy|-|+|-|+|-|
|Straddle buy|0|+|-|+|+|
|Covered write|+|-|+|-|-|
|Naked call sale|-|-|+|-|-|
|Naked put sale|+|-|+|-|+|
|Ratio write (straddle sale)|0|-|+|-|-|
|Calendar spread|0|-|+|+|-|
|Bull spread|+|-|-|-|+|
|Bear spread|-|-|-|-|+|
|Ratio call spread|0|-|+|-|-|
|Ratio put spread|0|-|+|-|+|

The calendar spread strategy does not want a lot of stock movement — he would prefer the underlying security to remain near the striking price, for that is the area of maximum profit potential. This is reflected by the fact that gamma is negative. Also, for calendar spreads, the passage of time is good, a fact that is reflected by the fact that theta is positive. Finally, since an increase in implied volatilities or interest rates would boost prices and widen the spread (creating a profit), vega is positive and rho is negative.

A bull spread has positive delta, reflecting the bullish nature of the spread, but it has negative gamma. The reason gamma is negative is that the position becomes less bullish as the underlying security rises, since the profit potential, and hence the bullishness of the position, is limited.

A bear spread has negative delta (reflecting bearishness) and negative gamma (reflecting limited bearishness).

Both the bull spread and the bear spread are the same with respect to the other risk measurements: Theta is negative, reflecting the fact that time decay can hurt the spread. Less obvious is the fact that these spreads are hurt by an increase in perceived volatility; a negative vega tells us this is true.

### 40.3.1 DELTA NEUTRAL

A delta neutral position is to have the equivalent stock position (ESP) or equivalent futures position (EFP) be zero. A delta neutral position is one in which the sum of the projected price changes of the long options in the spread is essentially offset by the projected price changes of the short options in the same spread.

*Example*: XYZ is trading at 50.

|Option|Price|Delta|"Theoretical Value"|
|--|--|--|--|
|January 50 call|3.00|0.55|3.50|
|January 55 call|1.50|0.35|1.48|
|February 50 put|3.50|-0.40|3.44|

Assuming that one can rely upon these "theoretical values", it is obvious that the January 50 call is cheap with respect to the other options: They are close to their values, while the January 50 is 50 cents under.

The neutral strategist would want to establish a spread wherein the January 50 calls are bought and a number of January 55's are sold. To determine how many are to be bought and sold, one merely has to divide the deltas of the two options:

$$
\text{Delta neutual spread ratio}=0.55/0.35=11/7
$$

Thus, a delta neutral ratio spread would consist of buying 7 January 50's and selling 11 January 55's. Notice that if XYZ moves up in price 1 point, the January 50 will increase in price by 0.55; so seven of them will increase by $7 \times 0.55$, or 3.85 points total. Similarly, the January 55 will increase in price by 0.35, so eleven of them would increase in price by $11 \times 0.35$, or 3.85 points total. Hence, the long side of the spread would profit by 3.85 points, while the short side loses 3.85 points — a neutral situation.

The resulting position is a ratio spread. The profitability of the spread occurs between about 51 and 62 at expiration.

The real attractiveness of the spread to the neutral trader is that if the underpriced nature of the January 50 call should disappear, the spread should produce a profit, regardless of the short-term market movement of XYZ. The spread could then be closed if this should occur.

To illustrate this fact, suppose that XYZ actually falls to 49, but the January 50 call returns to "fair value":

|Option|Price|Delta|"Theoretical Value"|
|--|--|--|--|
|January 50 call|3.00|0.52|3.00|
|January 55 call|1.10|0.34|1.13|
|February 50 put|3.90|-0.42|3.84|

Notice that the theoretical values in this table are equal to the theoretical values from the previous table, less the amount of the delta. Since the XYZ January 50 call is no longer underpriced, the position would be removed, and the strategist would make nothing on his January 50's, but would make 0.40 on each of the eleven short January 55's, for a profit of $440 less commissions.

Another type of delta neutral position could be established from the previous data: Buy the January 50 call and buy the February 50 put. This position is a long straddle of sorts. Recall that the delta of a put is negative; so again, the delta neutral ratio can be calculated by dividing the absolute value of two deltas:

$$
\text{Delta neutual straddle ratio}=0.55/|-0.40|=11/8
$$

Thus, a delta neutral straddle position would consist of buying 8 January 50 calls and buying 11 February 50 puts. The straddle has no market exposure, at least over the short term.

#### Delta Neutral Is Not Entirely Neutral.

In fact, delta neutral means that one is neutral only with respect to small price changes in the underlying security.

Positions with naked options in them have negative position gamma. This means that as the underlying security moves, the position will acquire traits opposite to that movement: If the security rises, the position becomes short; if it falls, the position becomes long.

*Example*: XYZ is at 88. There are three months remaining until July expiration, and the volatility of XYZ is 30%. Suppose 100 July 90 straddles are sold for 10 points — the put and the call each selling for 5. Initially, this position is nearly delta neutral, as shown in Table:

|Position|Option Delta|Position Delta|Option Gamma|Position Gamma|
|--|--|--|--|--|
|Sell 100 July 90 calls|0.505|-5,050|0.03|-300|
|Sell 100 July 90 puts|0.495|+4,950|0.03|-300|
|Total shares||-100||-600|

The initial position is NET short only 100 shares of XYZ, a very small delta. If the stock moves only 2 points lower, this trader's straddle position can be expected to behave as if it were now long 1,100 shares (the original 100 shares short plus 1,200 that the gamma tells us we can expect to get long). The position might look like this after the stock drops 2 points:

|Position|Option Delta|Position Delta|
|--|--|--|
|Sold 100 July 90 calls|0.44|-4400|
|Sold 100 July 90 puts|0.55|+5500|
|||+1100 shares|

In a similar manner, if the stock had risen 2 points to 90, the position would quickly have become delta short. In fact, one could expect it to be short 1,300 shares in that case: the original short 100 shares plus the 1,200 indicated by the negative gamma. A rise to 90 would make the position look like this:

|Position|Option Delta|Position Delta|
|--|--|--|
|Sold 100 July 90 calls|0.56|-5600|
|Sold 100 July 90 puts|0.43|+4300|
|||-1300 shares|

Figure 40-10 depicts what the delta of this large short straddle position will be, two weeks after it was first sold. The points on the horizontal axis are stock prices.

![FIGURE 40-10](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-40-10.png?raw=true)

With the first point that XYZ moves, from 88 to 89, the position acts as if it is short 100 shares (the position delta), so it would lose $100. With the next point that XYZ rises, from 89 to 90, the position will act as if it is short the original 100 shares (the position delta), plus another 600 shares (the position gamma). Hence, during that second point of movement by XYZ, the entire position will act as if it is short 700 shares, and therefore lose another $700. Therefore, an immediate 2-point jump in XYZ will cause an unrealized loss of $800 in the position. Summarizing:

- Loss, first point of stock movement = position delta
- Loss, second point of stock movement = position delta + gamma
- Total loss for 2 points of stock movement = 2 $\times$ position delta + position gamma

Using the example data:

- Loss, XYZ moves from 88 to 89: -100 (the position delta)
- Loss, XYZ moves from 89 to 90: -100 (delta) -600 (gamma) = -700
- Total loss, XYZ moves from 88 to 90: -100 $\times$ 2 -600 = -800

If the stock goes up by 1 point, the call will then have a price of:

$$
\begin{aligned}
&p_1=p_0+\text{delta} \\
&5.505=5.00+0.505 \quad (\text{if XYZ goes to 89 in the example})
\end{aligned}
$$

If the stock goes up 2 points, the call will have an increase of the above amount plus a similar increase for the next point of stock movement. The delta for that second point of stock movement is the original delta plus the gamma, since gamma tells one how much his delta is going to change.

$$
\begin{aligned}
&p_2=p_1+\text{gamma}=p_0+2 \times\text{delta}+\text{gamma} \\
&6.04=5.00+2\times 0.505+0.03 \quad (\text{in the example if XYZ = 90})
\end{aligned}
$$

By the same calculation, the put in the example will be priced at 4.04 if XYZ immediately jumps to 90: 

$$
4.04 = 5.00-2\times 0.495+0.03
$$

So, overall, the call will have increased by 1.04, but the put will only have decreased by 0.96. The unrealized loss would then be computed as -$10,400 for the 100 calls, offset by a gain of $9,600 on the sale of 100 puts, for a net unrealized loss of $800.

Let us look at time affecting the sale of this straddle. The exact amount of time decay to expect can be calculated from the theta of the position:

- XYZ: 88

|Position|Option Theta|Position Theta|
|--|--|--|
|Sold 100 July 90 calls|-0.03|+$300|
|Sold 100 July 90 puts|-0.03|+$300|
|||+$600|

Note that the theta is expressed as a negative number, and since these options are sold, the position theta is a positive number. A positive position theta means time decay is working in your favor. One could expect to make $300 per day from the sale of the 100 calls. He could expect to make another $300 per day from the sale of the 100 puts. Thus, his overall position is generating a theoretical profit from time decay of $600 per day.

Finally, let us examine the position with respect to changes in volatility. This is done by calculating the position vega.

- XYZ: 88

|Position|Option Vega|Position Vega|
|--|--|--|
|Sold 100 July 90 calls|0.18|-$1,800|
|Sold 100 July 90 puts|0.18|-$1,800|
|||-$3,600|

The fact that the call's vega is 0.18 means that the call price is expected to increase by 18 cents if the implied volatility of the option increases by one percentage point, from 30% to 31%. Since the position is short 100 calls, an increase of 18 cents in the price of the call would translate into a loss of $1,800. The put has a similar vega, so the overall position would lose $3,600 if the options trade with an increase in volatility of just one percentage point.

Position summary

|Risk Factor|Comment|
|--|--|
|Position delta = -100|Neutral; <br> no immediate exposure to small market movements; <br> lose $100 for 1 point move in underlying.|
|Position gamma = -600|Fairly negative; <br> position will react inversely to market movements, causing <br> losses of $700 for second point of movement by underlying.|
|Position theta = +$600|Favorable; <br> the passage of time works in the position's favor.|
|Position vega = -$3,600|Very negative; <br> position is extremely subject to changes in implied volatility.|

*Example*: Heavy volatility skewing exists in the prices of January soybean options: The out-of-the-money calls are much more expensive than the at-the-money calls. The following data is known:

- January soybeans: 583

|Option|Price|Implied Volatility|Delta|Gamma|
|--|--|--|--|--|
|575 call|19.50|15%|0.55|0.0100|
|675 call|2.25|23%|0.09|0.0026|

Using deltas, the following spread appears to be neutral:

- Buy 1 January bean 575 call at 19.50: 19.50 Debit
- Sell 6 January bean 675 calls at 2.25: 13.50 Credit
- Net position: 6 Debit

The position gamma of this spread is quite negative:

$$
\text{Position gamma}=0.01-6\times 0.0026=-0.0056
$$

That is, for every 10 points that January soybeans rally, the position will become short about 1/2 of one futures contract. The maximum profit point, 675, is 92 points above the current price of 583. While beans would not normally rally 92 points in only a few days, it does demonstrate that this position could become very short if beans quickly rallied to the point of maximum profit potential.

### 40.3.2 CREATING MULTIFACETED NEUTRALITY

The secret to determining a spread that is neutral with respect to both gamma and delta is to neutralize gamma first, for delta can always be neutralized by taking an offsetting position in the underlying security, whether it be stock or futures.

*Example*: XYZ is 60. A spreader wants to establish a spread that is neutral with respect to both gamma and delta, using the following prices:

|Option|Delta|Gamma|
|--|--|--|
|October 60 call|0.60|0.050|
|October 70 call|0.25|0.025|

First, determine a gamma neutral spread by dividing the two gammas:

$$
\text{Gamma neutral ratio}=0.050/0.025=2/l
$$

So, buying one October 60 and selling two October 70 calls would be a gamma neutral spread. Now, the position delta of that spread is computed:

|Position|Delta|Position Delta|
|--|--|--|
|Long 1 October 60 call|0.60|+60 shares|
|Short 2 October 70 calls|0.25|-50 shares|
|Net position delta:||+10 shares|

Hence, this gamma neutral ratio is making the position delta long by 10 shares of stock for each l-by-2 spread that is established. For example, if one bought 100 October 60 calls and sold 200 October 70 calls, his position delta would be long 1,000 shares. This position delta is easily neutralized by selling short 1,000 shares of the stock.

|Position|Option Delta|Position Delta|Option Gamma|Position Gamma|
|--|--|--|--|--|
|short 1,000 XYZ|1.00|-1,000|0|0|
|Long 100 October 60 calls|0.60|+6,000|0.050|+500|
|Short 200 October 70 calls|0.25|-5,000|0.025|-500|
|Net Position:||0||0|

Suppose that one thought the implied volatility of a certain set of options was too high. He would construct a position with negative vega to reflect his expectation on volatility, but then also have the position be delta neutral and gamma neutral.

*Example*: XYZ is 48. There are three months to expiration, and the volatility of XYZ and its options is 35%. The following information is also known:

- XYZ: 48

|Option|Price|Delta|Gamma|Vega|
|--|--|--|--|--|
|April 50 call|2.50|0.47|0.045|0.08|
|April 60 call|1.00|0.17|0.026|0.06|

He wants to have a negative position vega so that when the volatility decreases, he will make money.

First, he should determine a gamma neutral spread.

$$
\text{Gamma neutral ratio} = 0.045/0.026 = 1.73/l
$$

Thus, a gamma neutral position would be created by buying 100 April 50's and selling 173 April 60's.

|Position|Option Delta|Position Delta|Option Gamma|Position Gamma|Option Vega|Position Vega|
|--|--|--|--|--|--|--|
|long 100 April 50|0.47|+4,700|0.045|+450|0.08|+$800|
|Short 173 April 60|0.17|-2,941|0.026|-450|0.06|-1,038|
|Total:||+1,759||0||-$238|

The position delta is long 1,759 shares of XYZ. Consequently, the complete position, including the short 1,700 shares, would be neutral with respect to both delta and gamma, and would have the desired negative vega.

### 40.3.3 THE MATHEMATICAL APPROACH

*Example*: XYZ is 48. There are three months to expiration, and the volatility of XYZ and its options is 35%. The following information is also the same:

|Option|Price|Delta|Gamma|Vega|
|--|--|--|--|--|
|April 50 call|2.50|0.47|0.045|0.08|
|April 60 call|1.00|0.17|0.026|0.06|

A spreader expects volatility to decline and is willing to set up a position whereby he will profit by $250 for each one percentage decrease in volatility Moreover, he wants to be gamma and delta neutral.

The unknowns x and y represent the quantities of options to be bought and sold, respectively.

Equations:

$$
\begin{aligned}
&0.045x + 0.026y = 0 \\
&0.08x + 0.06y = -2.5
\end{aligned}
$$

Solutions:

$$
\begin{aligned}
&x = 104.80 \\
&y = -181.45
\end{aligned}
$$

The first equation represents gamma neutral. The second equation represents the desired vega risk of making 2.5 points, or $250. x is the number of April 50's in the spread and y is the number of April 60's.

The solutions means that one would buy 105 April 50 calls, since x being positive means that the options would be bought. He would also sell 181 April 60 calls (y is negative, which implies that the calls would be sold).

Finally, one would again determine the amount of stock to buy or sell to neutralize the delta by computing the position delta:

$$
\text{Position delta}=105 \times 0.47 - 181 \times 0.17 = 18.58
$$

Thus 1,858 shares of XYZ would be shorted to neutralize the position.

Note: All the equations cannot be set equal to zero, or the solution will be all zeros. This is easily handled by setting at least one equation equal to a small, nonzero quantity, such as 0.1.

### 40.3.4 EVALUATING A POSITION USING THE RISK MEASURES

First, one would choose an appropriate time period — say, 7 days hence — for the first analysis. Then he should use the statistical projection of stock prices to determine probable prices for the underlying security at that time.

*Example*: XYZ is at 60 and has a volatility of 35%. A distribution of stock prices 7 days into the future would be determined using the equation:

$$
\text{Future Price}=\text{Current Price}\times e^{av\sqrt{t}}
$$

where $a$ corresponds to the constants in the following table: (-2.0, ..., 2.0):

|Standard Deviations|Projected Stock Price|
|--|--|
|-2.0|54.46|
|-1.5|55.79|
|-1.0|57.16|
|-0.5|58.56|
|0|60.00|
|0.5|61.47|
|1.0|62.98|
|1.5|64.52|
|2.0|66.11|

Once the appropriate stock prices have been determined, the following quantities would be calculated for each stock price: profit or loss, position delta, position gamma, position theta, and position vega.

#### Initial Position. 

XYZ is at 60. The January 70 calls, which have three months until expiration, are expensive with respect to the January 60 calls. A strategist expects this discrepancy to disappear when the implied volatility of XYZ options decreases. He therefore established the following position, which is both gamma and delta neutral.

|Position|Delta|Gamma|Theta|Vega|
|--|--|--|--|--|
|Long 100 January 60 calls|0.565|0.0723|-0.020|0.109|
|Short 240 January 70 calls|0.204|0.0298|-0.019|0.080|
|Short 800 XYZ|||||

The risk measures for the entire position are:
- Position delta: -46 shares (virtually delta neutral)
- Position gamma: +8 shares (gamma neutral)
- Position theta: +$256
- Position vega: -$830

The following analyses will assume that the relative expensiveness of the April 70 calls persists.

How would the position look in 7 days at the stock prices determined above?

|Stock Price|P&L|Delta|Gamma|Theta|Vega|
|--|--|--|--|--|--|
|54.46|1905|-7.40|1.62|0.94|-1.57|
|55.79|1077|-4.90|2.07|1.18|-1.96|
|57.16|606|-1.97|2.13|1.53|-2.90|
|58.56|528|0.74|1.65|2.00|-4.62|
|60.00|771|2.38|0.56|2.63|-7.22|
|61.47|1127|2.07|-1.01|3.38|-10.63|
|62.98|1252|-0.87|-2.85|4.22|-14.56|
|64.52|702|-6.73|-4.67|5.07|-18.61|
|66.11|-1019|-15.42|-6.21|5.85|-22.31|

In a similar manner, the position would have the following characteristics after 14 days had passed: 

|Stock Price|P&L|Delta|Gamma|Theta|Vega|
|--|--|--|--|--|--|
|52.31|4221|-9.10|0.69|0.55|-0.98|
|54.14|2731|-6.93|1.69|0.75|-0.89|
|56.02|1782|-2.87|2.51|1.06|-1.21|
|57.98|1717|2.17|2.44|1.61|-2.69|
|60.00|2577|5.85|1.00|2.51|-6.00|
|62.09|3839|5.29|-1.63|3.73|-11.05|
|64.26|4361|-1.55|-4.61|5.09|-16.90|
|66.50|2631|-14.80|-7.02|6.31|-22.17|
|68.82|-2799|-32.83|-8.32|7.18|-25.72|

![FIGURE 40-12](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-40-12.png?raw=true)

![FIGURE 40-13](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-40-13.png?raw=true)

![FIGURE 40-14](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-40-14.png?raw=true)

Note that in 7 days, there is a small profit if the stock remains unchanged. This is to be expected, since theta was positive, and therefore time is working in favor of this spread.

The downside is favorable to the spread since the short stock in the position would contribute to ever larger profits in the case that XYZ tumbles dramatically. The upside is where problems could develop.

#### Follow-Up Action.

A simplistic approach is to adjust the delta as it becomes non-neutral.

If one were to adjust only the delta, he would do it in the following manner: The position will be approximately delta short 800 shares if XYZ rises to 64.50 in a week. One simple plan would be to cover the 800 shares of XYZ that are short if the stock rises to 64.50.

The only way to counter negative gamma is to buy options, not stock. To return a position to neutrality with respect to more than one risk variable requires one to approach the problem as he did when the position was established: Neutralize the gamma first, and then use stock to adjust the delta.

### 40.3.5 TRADING GAMMA FROM THE LONG SIDE

The simplest position with long gamma is a long straddle, or a backspread (reverse ratio spread). Another way to construct a position with long gamma is to invert a calendar spread — to buy the near-term option and to sell a longer-term one. Since a near-term option has a higher gamma than a longer-term one with the same strike, such a position has long gamma.

*Example*: Suppose that a strategist wants to create a position that is gamma long, but is neutral with respect to both delta and vega. Let us assume that he wants to be gamma long 1,000 shares or 10 contracts.

- XYZ: 60

|Option|Price|Delta|Gamma|Theta|Vega|
|--|--|--|--|--|--|
|March 60 call|3.25|0.54|0.0510|0.033|0.089|
|June 60 call|5.50|0.57|0.0306|0.021|0.147|

The two equations below are used to determine the quantities to buy in order to make gamma long and vega neutral:

$$
\begin{aligned}
&0.0510x + 0.0306y = 10 \quad (\text{gamma}) \\
&0.089x + 0.147y = 0 \quad (\text{vega})
\end{aligned}
$$

The solution to these equations is: $x = 308, y = —186$

Thus, one would buy 308 March 60 calls and would sell 186 June 60 calls. This is the reverse calendar spread that was discussed: Near-term calls are bought and longer-term calls are sold.

Finally, the delta must be neutralized. To do this, calculate the position delta using the quantities just determined:

$$
\text{Position delta}= 0.54 \times 308 - 0.57 \times 186 = 60.30
$$

The overall position would look like this:

|Position Delta Gamma Vega|
|--|--|--|--|
|Short 6,000 XYZ|1.00|0|0|
|Long 308 March 60 calls|0.54|0.0510|0.089|
|Short 186 June 60 calls|0.57|0.0306|0.147|

It's risk measurements are:

- Position delta: long 30 shares (neutral)
- Position vega: $7 (neutral)
- Position gamma: long 1,001 shares

Fiually, note that theta = -$625. The position will lose $625 per day from time decay.

Figure 40-15 (see Tables 40-10, 40-11, and 40-12) shows the profit potential in 7 days, in 14 days, and at March expiration.

![FIGURE 40-15](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-40-15.png?raw=true)

TABLE 40-10. Risk measures of long gamma position in 7 days.

|Stock Price|P&L|Delta|Gamma|Theta|Vega|
|--|--|--|--|--|--|
|54.46|12259|-58.72|8.28|4.15|-5.74|
|55.79|5202|-46.60|9.78|5.20|-4.18|
|57.16|-224|-32.45|10.80|6.09|-2.85|
|58.56|-3670|-16.91|11.25|6.73|-1.94|
|60.00|-4975|-0.80|11.08|7.04|-1.63|
|61.47|-3901|15.01|10.32|6.98|-1.96|
|62.98|-507|29.69|9.09|6.57|-2.89|
|64.52|5105|42.56|7.54|5.87|-4.29|
|66.11|12717|53.17|5.86|4.97|-5.96|

TABLE 40-11. Risk measures of long gamma position in 14 days.

|Stock Price|P&L|Delta|Gamma|Theta|Vega|
|--|--|--|--|--|--|
|52.31|24945|-79.34|4.75|2.10|-9.91|
|54.14|11445|-67.68|8.00|3.91|-787|
|56.02|277|-49.79|10.79|5.76|-5.56|
|57.98|-7263|-26.87|12.42|7.21|-3.73|
|60.00|-10141|-1.44|12.47|788|-3.04|
|62.09|-7784|23.32|10.99|7.60|-3.78|
|64.26|-347|44.47|8.45|6.47|-5.71|
|66.50|11491|60.12|5.55|4.82|-8.20|
|68.82|26672|69.81|2.92|3.09|-10.48|

TABLE 40-12. Risk measures of long gamma position at March expiration.

|Stock Price|P&L|Delta|Gamma|Theta|Vega|
|--|--|--|--|--|--|
|46.19|81327|-75.69|-3.65|-1.32|-6.88|
|9.31|55628|-89.84|-5.39|-2.25|-11.43|
|52.64|22378|-110.50|-6.89|-3.33|-16.50|
|56.20|-21523|-136.65|-7.62|-4.28|-20.67|
|60.00|-78907|144.68|-7.29|-4.79|-22.49|
|64.06|-25946|11744|-6.03|-4.70|-21.26|
|68.39|19787|95.03|-4.31|-4.10|-17.44|
|73.01|59732|79.05|-2.67|-3.24|-12.43|
|77.95|96062|69.19|-1.43|-2.41|-7.69|

Figure 40-16 shows the position vega at the 7- and 14-day time intervals.

![FIGURE 40-16](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-40-16.png?raw=true)

#### Other Variations.

In the preceding position, the strategist wanted to be gamma long, but neutral with respect to delta and volatility. Suppose he not only expects price movement (meaning he wants positive gamma), but also expects an increase in volatility. If that were the case, he would want positive vega as well. Suppose he quantifies that desire by deciding that he wants to make $1,000 for every one percentage increase in volatility. The simultaneous equations would then be:

$$
\begin{aligned}
&0.0510x + 0.0306y = 10 \quad (\text{gamma}) \\
&0.089x + 0.147y = 10 \quad (\text{vega})
\end{aligned}
$$

The solution to these equations is: $x = 243, y = -80$

Furthermore, 8,500 shares would have to be sold short in order to make the position delta neutral. The resulting position would then be:

|||
|--|--|
|Short 8,500 XYZ|Delta: neutral|
|Long 243 March 60 calls|Gamma: long 1,000 shares|
|Short 80 June 60 calls|Vega: long $1,000|
||Theta: long $630|

Recall that the position discussed in the last section was vega neutral and was:

|||
|--|--|
|Short 6,000 XYZ|Delta: neutral|
|Long 308 March 60 calls|Gamma: long 1,000 shares|
|Short 186 June 60 calls|Vega: neutral|
||Theta: long $625|

Notice that in the new position, there are over three times as many long March 60 calls as there are short June 60 calls. This even greater preponderance of near-term calls that are purchased means the newer position has an even larger exposure to time decay than did the previous one. That is, in order to acquire the positive vega, one is forced to take on even more risk with respect to time decay. For that reason, this is a less desirable position than the first one.

In fact, if one expected volatility to increase, he might want to establish a position that was delta neutral and gamma neutral, but had positive vega. Again, using the same prices as in the previous examples, the following position would satisfy these criteria:

|||
|--|--|
|Short 2,600 XYZ|Delta: neutral|
|Short 64 March 60 calls|Gamma: neutral|
|Long 106 June 60 calls|Vega: long $1,000|
||Theta: long $11|

This position is a calendar spread, except that more long calls are purchased. Moreover, the theta of this position is only $11 — it will only lose $11 per day to time decay. At first glance it might seem like the best of the three choices. Unfortunately, when one draws the profit graph (Figure 40-19), he finds that this position has significant downside risk: The short stock cannot compensate for the large quantity of June 60 calls. Still, the position does make money on the upside, and will also make money if volatility increases.

![FIGURE 40-19](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-40-19.png?raw=true)

Thus, in the example presented, the strategist felt that he initially wanted to be long gamma, but it involved too much risk of time decay. A second attempt was made, introducing positive volatility into the situation, but that didn't seem to help much. Finally, a third analysis was generated involving only long volatility and not long gamma. The resulting position has little time risk, but has risk if the stock drops in price.

## 40.4 ADVANCED MATHEMATICAL CONCEPTS

### 40.4.1 CALCULATING THE "GREEKS"

The equation for delta is a direct by-product (副产品) of the Black-Scholes model calculation:

$$
\Delta=N(d_1)
$$

The formula for gamma is as follows:

$$
\begin{aligned}
&x=\ln\left[\frac{P}{s\times(1+r)^t}\right]\bigg/v\sqrt{t}+\frac{v\sqrt{t}}{2} \\
&\Gamma=\frac{e^{(-x^2/2)}}{pv\sqrt{2\pi t}}
\end{aligned}
$$

Thus, one can approximate the gamma by the following steps:
1. Calculate the delta with p = Current stock price.
2. Set p = p + 1 and recalculate the delta.
3. Gamma = delta from step 1 - delta from step 2.

Vega:
1. Calculate the option price with a particular volatility.
2. Calculate another option price with volatility increased by 1%.
3. Vega = difference of the prices in steps 1 and 2.

Theta:
1. Calculate the option price with the current time to expiration.
2. Calculate the option price with 1 day less time remaining to expiration.
3. Theta = difference of the prices in steps 1 and 2.

Rho:
1. Calculate the option price with the current risk-free interest rate.
2. Calculate the option price with the rate increased by 1%.
3. Rho = difference of the prices in steps 1 and 2.

### 40.4.2 THE GAMMA OF THE GAMMA

The gamma of the gamma is the amount by which the gamma will change when the stock price changes.

*Example*: With XYZ at 49, assume the January 50 call has a delta of 0.50 and a gamma of 0.05. If XYZ moves up 1 point to 50, the delta of the call will increase by the amount of the gamma: It will increase from 0.50 to 0.55. Simplistically, if XYZ moves up another point to 51, the delta will increase by another 0.05, to 0.60.

In reality, the gamma decreases as the stock moves away from the strike. Thus, with XYZ at 51. the gamma might only be 0.04. Therefore, if XYZ moved up to 52, the call's delta would only increase by 0.04, to 0.64. Hence, the gamma of the gamma is -0.01, since the gamma decreased from 0.05 to 0.04 when the stock rose by one point.

Example: With XYZ at 31.75 as in some of the previous examples, the following risk measures exist:

|Position|Option Delta|Option Gamma|Option Gamma/Gamma|Position Gamma/Gamma|
|--|--|--|--|--|
|Short 4,500 XYZ|1.00|0.00|0.0000|0|
|Short 100 XYZ April 25 calls|0.89|0.01|-0.0015|-15|
|Long 50 XYZ April 30 calls|0.76|0.03|-0.0006|-3|
|Long 139 XYZ July 30 calls|0.74|0.02|-0.0003|-4|
|||Total Gamma of Gamma:|-22|

Recall that, in the same example used to describe gamma, the position was delta long 686 shares and had a positive gamma of 328 shares.

In fact, it is expected to increase or decrease by 22 shares for each point XYZ moves.

### 40.4.3 MEASURING THE DIFFERENCE OF IMPLIED VOLATILITIES

A logical way to approach this is to look at each individual implied volatility and compute the standard deviation of these numbers. This standard deviation can be converted to a percentage by dividing it by the overall implied volatility of the stock. This percentage, if it is large enough, alerts the strategist that there may be opportunities to spread the options of this underlying security against each other.

*Example*: XYZ is trading at 50, and the following options exist with the indicated implied volatilities. We can calculate a standard deviation of these implieds, called implied deviation, via the formula:

$$
\text{Implied deviation}=\sqrt{\frac{\sum(\text{differences from mean})^2}{\text{number of options}-1}}
$$

- XYZ: 50

|Option|Implied Volatility|Difference from Average|
|--|--|--|
|October 45 call|21%|-9.44|
|November 45 call|21%|-9.44|
|January 45 call|23%|-7.44|
|October 50 call|32%|+1.56|
|November 50 call|30%|-0.44|
|January 50 call|28%|-2.44|
|October 55 call|40%|+9.56|
|November 55 call|37%|+6.56|
|January 55 call|34%|+3.56|

- Average: 30.44%

$$
\begin{aligned}
\sum(\text{difference from avg})^2=389.26 \\
\text{Implied deviation}=\sqrt{(389.26/8)}=6.98
\end{aligned}
$$

This figure represents the raw standard deviation of the implied volatilities. To convert it into a useful number for comparisons, one must divide it by the average implied volatility.

$$
\text{Percent deviation}=\frac{\text{Implied deviation}}{\text{Average implied}}=\frac{6.98}{30.44}=23\%
$$

This "percent deviation" number is usually significant if it is larger than 15%.

