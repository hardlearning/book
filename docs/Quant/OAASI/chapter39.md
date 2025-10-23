# CHAPTER 39 Volatility Trading Techniques

## 39.2 TRADING THE VOLATILITY PREDICTION

### 39.2.1 DETERMINING WHEN VOLATILITY IS OUT OF LINE

1. Compare implied volatility to its own past levels (percentile approach).
2. Compare implied volatility to historical volatility.
3. Interpret the chart of volatility.

In addition, we will examine two lesser-used methods: comparing current levels of historical volatility to past measures of historical volatility, and finally, using only a probability calculator and trading the situation that has the best probabilities of success.

### 39.2.2 THE PERCENTILE APPROACH

The percentile of implied volatility is generally used to describe just where the current implied volatility reading lies with respect to its past values.

Those with readings in the 10th percentile or less would be considered "cheap"; those in the 90th percentile or higher would be considered expensive.

### 39.2.3 COMPARING IMPLIED AND HISTORICAL VOLATILITY

One should ensure that implied volatility is significantly different from all of the pertinent historical volatilities. For example, one might require that implied volatility is less than 80% of each of the 10-, 20-, 50-, and 100-day historical volatility calculations. (需要确定隐含波动率比10天、20天、50天和100天的历史波动率都低80%)

### 39.2.7 SELECTING THE STRATEGY TO USE

If volatility is too low, then either a straddle or a strangle should be purchased. One would normally choose a straddle if the underlying instrument is currently trading near an available striking price. However, if the underlying is currently trading between two striking prices, then a strangle might be the better choice.

Example: XYZ is trading at 39.60 and a volatility trader has determined that he wants to buy volatility with this information, he should attempt to buy a straddle with a striking of 40 for both the put and the call.

If XYZ had been trading at a price of 37.50, then the trader would probably want to consider buying a strangle: buying a call with a striking price of 40 and a put with a striking price of 35.

Speaking of neutrality, one can also use the deltas of the options in question to alter the ratio of puts to calls, making the position initially as neutral as possible.

Example: XYZ is again trading at 39.60, and the trader wants a neutral position. Consider the October 40 straddle, for example. Assume the volatility used for the probability calculations is 40%. The October 40 call has a delta of 0.60 and the October 40 put has a delta of -0.40. Thus a ratio of buying 2 calls and 3 puts is a neutral ratio. If the call is selling for 6 and the put is selling for 5, then the break-even points for a 2-by-3 position would be 53.5 on the upside and 31 on the downside. This information is summarized as follows:

- Delta of October 40 call: +0.60
- Delta of October 40 put: -0.40
- Delta-neutral ratio: buy 2 calls and 3 puts
- Price of October 40 call: 6.00
- Price of October 40 put: 5.00
- Net cost of 2-by-3 position: 27 points
- Break-even points:
  - Upside = 40 + 27/2 = 53.50
  - Downside = 40 - 27/3 = 31.00

So, the probability calculations would endeavor to determine what the chances are of the stock ever trading at either 53.50 or 31.00 at any time prior to expiration.

Another simple strategy that can be used when volatility is low is the calendar spread, because it has a positive vega. That is, it can be expected to expand if implied volatility increases.

### 39.2.8 SELLING VOLATILITY

The simplest strategy is just to sell both an out-of-the-money put and an out-of-the-money call. The striking prices chosen should be far enough away from the current underlying price so that the probabilities of the position getting in trouble are quite small.

The next best choice is a credit spread. The problem with a credit spread is that one is both selling expensive options and also buying expensive options as protection.

If volatility decreases, the profits to be realized by a credit spreader are quite small, whereas a naked option seller would benefit to a greater and more obvious extent.

Index options are by far the best choices for naked option selling. Futures are next, and stocks are last.

### 39.2.9 USING A PROBABILITY CALCULATOR

An attractive volatility buying situation should have probabilities in excess of 80% of the underlying ever exceeding the break-even point, while an attractive volatility selling situation should have probabilities of less than 25% of ever trading at prices that would cause losses.

*Example*: The OEX Index is trading at 650. Suppose that one has determined that volatilities are too high and wants to analyze the sale of some naked options. Furthermore, suppose that the choices have been narrowed down to selling the September options, which expire in about five weeks.

|Naked sale:|September 800 call<br>September 500 put|September 750 call<br>September 550 put|September 730 call<br>September 570 put|September 700 call<br>September 600 put|
|--|--|--|--|--|
|Call price|0.20|1.50|3.50|8.80|
|Put price|0.40|2.00|3.70|8.50|
|Probability of call strike|4%|17%|30%|44%|
|Probability of put strike|1%|11%|20%|40%|

The two right-hand columns should be rejected because the probabilities of the stock hitting one or the other of the striking prices prior to expiration are too high — well in excess of the 25% guideline mentioned earlier.

Remember that one is required to establish the position with margin of at least 10% of the index price for naked index options, which would be $6,500 in this case. In fact, it has been recommended that one margin the position at the striking price itself (15% of 800, or $12,000 in this case). So, taking in only $60, less commissions, for the sale of the September 500-800 strangle doesn't seem to provide enough of a reward.

Thus, the best choice seems to be the September 550-750 strangle. One would be making about $320 after commissions if the options expired worthless, and the recommended margin would be 15% of 750 (the higher strike), or $11,250 — a return of about 2.8% for one month.

### 39.2.12 MORE THOUGHTS ON SELLING VOLATILITY

The simplest strategy that has the desired traits is selling a calendar spread — that is, sell a longer-term option and hedge it by buying a short-term option at the same strike. True, both are expensive. But the longer-term one trades with a far greater absolute price, so if both become cheaper, the longer-term one can decline quite a bit farther in points than the near-term one. That is, the vega of the longer-term option is greater than the vega of the shorter-term one. When one sells a calendar spread, it is called a reverse calendar spread (反向跨期价差).

A volatility backspread (波动率后式价差) involves selling a long-term at-the-money option (just as in the reverse calendar spread) and then buying a greater number of nearer term out-of-the-money options. The position is generally constructed to be delta-neutral and it has a negative vega, meaning that it will profit if implied volatility decreases.

*Example*: XYZ is trading at 115 in early June. Its options are very expensive. A trader would like to construct a volatility backspread using the following two options:

|Call Option|Price|Delta|Vega|
|--|--|--|--|
|July 130 call|2.50|0.26|0.10|
|October 120 call|13|0.53|0.27|

A delta-neutral position would be to buy 2 of the July 130 calls and sell one of the October 120 calls. This would bring in a credit of 8 points. Also, it would have a small negative position vega, since two times the vega of the July calls minus one times the vega of the October call is -0.07. That is, for each one percentage point drop in implied volatility of XYZ options in general, this position would make $7.

### 39.2.13 SUMMARY: TRADING THE VOLATILITY PREDICTION

Step 1: Use a selection criterion to limit the myriad of volatility trading choices. Any of these could be used as the first criterion, but not all of them at once:

- a. Require implied volatility to be at an extreme percentile.
- b. Require historical and implied volatility to have a large discrepancy between them.
- c. Interpret the chart of implied volatility to see if it has reversed trend.

Step 2: Use a probability calculator to project whether the strategy can be expected to be a success.

Step 3: Using past price histories, determine whether the underlying has been able to create profitable trades in the past. Use histograms to ensure that the past distribution of stock prices is smooth, so that an aberrant, nonrepeatable move is not overly influencing the results.

## 39.3 TRADING THE VOLATILITY SKEW

Individual options on the same underlying instrument have significantly different implied volatilities. This is called a volatility skew.

### 39.3.1 DIFFERING IMPLIED VOLATILITIES ON THE SAME UNDERLYING SECURITY

*Example*: XYZ is trading at 45. The following option prices exist, along with their implied volatilities:

|Option|Actual Price|Implied Volatility|
|--|--|--|
|January 45 call|2.75|41%|
|January 50 call|1.25|47%|
|January 55 call|0.63|53%|
|February 45 call|3.50|38%|
|February 50 call|4.00|45%|

A neutral strategy could be established by buying options with lower implied volatilities and simultaneously selling ones with higher volatilities, such as buy 10 February 45 calls and sell 20 January 50 calls.

### 39.3.2 VOLATILITY SKEWING

Volatility skewing: the long-lasting effect whereby options at different striking prices trade with differing implied volatilities. (波动率倾斜是不同行权价的期权按不同的隐含波动率交易的持久效果)

*Example*: Volatility skewing exists in OEX index options. Assume the average volatility of OEX and its options is 16%. With volatility skewing present, the implied volatilities at the various striking prices might look like this:

- OEX: 580

|Strike|Implied Volatility of Both Puts and Calls|
|--|--|
|550|22%|
|560|19%|
|570|17%|
|580|16%|
|590|15%|
|600|14%|
|610|13%|

In this form of volatility skewing, the out-of-the-money puts are the most expensive options; the out-of-the-money calls are the cheapest. This pattern of implied volatilities is called a reverse volatility skew (反向波动率倾斜) or, alternatively, a negative volatility skew.

The causes of this effect stem from the stock markets penchant to crash occasionally.

It was shown in previous examples that one would attempt to sell the options with higher implied volatilities and buy ones with lower implieds as a hedge. Hence, for OEX traders, three strategies seem relevant:

1. Buy a bear put spread in OEX. Example: Buy 10 OEX June 560 puts, Sell 10 OEX June 540 puts.
2. Buy OEX puts and sell a larger number of out-of-the-money puts — a ratio write of put options. Example: Buy 10 OEX June 560 puts, Sell 20 OEX June 550 puts.
3. Sell OEX calls and buy a larger number of out-of-the-money calls — a backspread of call options. Example: Buy 20 OEX June 590 calls, Sell 10 OEX June 580 calls.

As a general rule of thumb, one would use the ratio spread strategy if the current level of implied volatility were in a high percentile. The backspread strategy would be used if implied volatility were in a low percentile currently.

Assuming that the skewing is present wherever OEX is trading means that the at-the-money strike will have 16% as its implied volatility regardless of the absolute price level; the skewing will then extend out from that strike.

*Example*: Initially, a trader establishes a call backspread in OEX options in order to take advantage of the volatility skewing:

- Initial situation: OEX: 580

|Option|Implied Volatility|Delta|
|--|--|--|
|June 590 call|15%|0.40|
|June 600 call|14%|0.20|

A neutral spread would be:
- Buy 2 June 600 calls
- Sell 1 June 590 call

since the deltas are in the ratio of 2-to-1.

Now, suppose that OEX rises to 600 at a later date, but well before expiration. The present situation would probably look like this:

|Option|Implied Volatility|
|--|--|
|June 590 call|17%|
|June 600 call|16%|

The June 600 call is now the at-the-money call, since OEX has risen to 600. As such, its implied volatility will be 16%. The June 590 call has a slightly higher volatility (17%) because volatility skewing is still present.

The overall spread should benefit for two reasons:
1. Twice as many options are owned as were sold. (买入期权数量是卖出期权数量的两倍)
2. The effect of increased volatility is greatest on the at-the-money option; the in-the-money will be affected to a lesser degree.

Volatility skewing exists in futures option markets as well.  In particular, futures options will from time to time display a form of volatility skewing that is the opposite of that displayed by index options. In these futures markets, the cheapest options are out-of-the-money puts, while the most expensive options are out-of-the-money calls.

*Example*: January soybeans are trading at 580 (85.80 per bushel). The following table of implied volatilities shows how volatility skewing that is present in the soybean market is the opposite of that shown by the OEX market in the previous examples:

- January beans: 580

|Strike|Implied Volatility|
|--|--|
|525|12%|
|550|13%|
|575|15%|
|600|17%|
|625|19%|
|650|21%|
|675|23%|

Notice that the out-of-the-money calls are now the more expensive items, while out-of-the-money puts are the cheapest. This pattern of implied volatilities is called forward volatility skew (前向波动率倾斜) or, alternatively, positive volatility skew.

A strategist attempting to benefit from the forward  volatility skew in this market has essentially three strategies available. First would be a call bull spread, second would be a put backspread, and third would be a call ratio spread. In all three cases, one would be buying options at the lower striking price and selling options at the higher striking price.
