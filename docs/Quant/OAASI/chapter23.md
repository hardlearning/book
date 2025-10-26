# CHAPTER 23 Spreads Combining Calls and Puts

## 23.1 THE BUTTERFLY SPREAD

The butterfly spread involves three striking prices, utilizing a bull spread between the lower two strikes and a bear spread between the higher two strikes.

*Example*: The following prices exist:

- XYZ common: 60

|||||
|--|--|--|--|
|Strike:|50|60|70|
|Call:|12|6|2|
|Put:|1|5|11|

Table 23-1 summarizes the four ways in which the butterfly spread might be constructed.

|Bull Spread<br>(Buy Option at 50, Sell at 60)|Bear Spread<br>(Buy Option at 70, Sell at 60)|Total Money|
|--|--|--|
|Calls (6 debit)|Calls (4 credit)|2 debit|
|Calls (6 debit)|Puts (6 debit)|12 debit|
|Puts (4 credit)|Calls (4 credit)|8 credit|
|Puts (4 credit)|Puts (6 debit)|2 debit|

In each of the four spreads, the maximum potential profit at expiration is 8 points if the underlying stock is exactly at 60 at that time. The maximum possible loss in any of the four spreads is 2 points, if the stock is at or above 70 at expiration or is at or below 50 at expiration.

- Maximum profit = striking price differential - maximum risk

Bull spreads are best constructed with calls, and bear spreads are best constructed with puts. Since the butterfly spread is merely the combination of a bull spread and a bear spread, the best way to set up the butterfly spread is to use calls for the bull spread and puts for the bear spread.

## 23.2 CONDOR AND IRON CONDOR SPREADS

Condor spreads (鹰式价差) are very similar to butterfly spreads, except that one uses two different strikes in the center of the spread. Condor spreads are constructed with all call options, or with all put options. Iron condors (铁鹰式价差) are essentially the same thing, except that they are a mix of puts and calls. Both have profit graphs with the same shape, so they are equivalent.

*Example*: Assume XYZ is trading at 120. An iron condor spread might be established as follows:

- Buy 1 XYZ Dec 135 call: 0.50
- Sell 1 XYZ Dec 130 call: 1.00
- Sell 1 XYZ Dec 110 put: 1.00
- Buy 1 XYZ Dec 105 put: 0.50
- Net Credit: 1.00

In it's basic form, the difference in the call strikes and the put strikes should be the same (5 points in this example).

If the underlying stock closes between the two middle strikes at expiration, all the options will expire worthless, and the trader will profit by the amount of the initial credit (less commissions). That is the maximum profit available from the trade: 100 in this example.

If the underlying is outside of either of the long strikes at expiration, the maximum loss is realized, which would be 400 in this example.

Maximum loss = Difference In High Strikes — Initial Credit = 135 - 130 - 1.00 = 4.00

![FIGURE 23-1](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-23-1.png?raw=true)

## 23.3 COMBINING AN OPTION PURCHASE AND A SPREAD

It is possible to combine the purchase of a call and a credit put spread to produce a position that behaves much like a call buy, although it has less risk over much of the profit range.

In a similar manner, if one is bearish on the underlying, he can sometimes combine the purchase of a put with the sale of a call credit spread.

### 23.3.1 THE BULLISH SCENARIO

*Example*: XYZ is selling at 100. One wishes to purchase the December 100 call as an outright bullish speculation. That call is selling for 10. However, one determines that the December 100 call is overpriced at these levels. Hence, he decides to use the following put spread in addition to buying the December 100 call:

- Sell December 90 put, 6
- Buy December 80 put, 3

The sale of the put spread brings in a 3-point credit. Thus, his total expenditure for the entire position is 7 points.

The resulting position is shown in Figure 23-2, along with two other plots. The straight line marked "Spread at expiration" shows how the profitability of the call purchase combined with a bull spread would look at December expiration. In addition, there is a plot with straight lines of the purchase of the December 100 call for 10 points.

The final plot in Figure 23-2 is that of the three-way spread's (三重价差) profit and losses halfway to the expiration date. You can see that it looks much like the profitability of merely owning a call.

![FIGURE 23-2](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-23-2.png?raw=true)

### 23.3.2 THE BEARISH SCENARIO

*Example*: XYZ is trading at 80, and one has a definite bearish opinion on the stock. However, the December 80 put, which is selling for 8, is expensive according to an option analysis. Therefore, one might consider selling a call credit spread (out-of-the-money) to help reduce the cost of the put. The entire position would thus be:

- Buy 1 December 80 put: 8 debit
- Sell 1 December 90 call: 4 credit
- Buy 1 December 100 call: 2 debit
- Total cost: 6 debit (600)

The profitability of this position is shown in Figure 23-3. The straight line on that graph shows how the position would behave at expiration. The margin required would be this maximum risk, or 1,600.

The curved line on Figure 23-3 shows how the three-way spread would behave if one looked at it halfway to its expiration date. In that case, it has a curved appearance much like the outright purchase of a put option.

![FIGURE 23-3](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-23-3.png?raw=true)

## 23.5 THREE USEFUL BUT COMPLEX STRATEGIES

### 23.5.1 A TWO-PRONGED ATTACK (THE DUAL CALENDAR SPREAD)

With a stock midway between two striking prices, one might set up a bullish out-of-the-money call calendar spread and simultaneously establish a bearish out-of-the-money put calendar spread.

*Example*: Suppose that the following prices exist three months before the January options expire:

- XYZ common: 65
- January 70 call: 3
- April 70 call: 5
- January 60 put: 2
- April 60 put: 3

The bullish portion of this combination of calendar spreads would be set up by selling the shorter-term January 70 call for 3 points and simultaneously buying the longer-term April 70 call for 5 points. The bearish portion of the spread would be constructed using the puts. The near-term January 60 put would be sold for 2 points, while the longer-term April 60 put would be bought for 3.

The bullish portion of the spread requires a 2-point debit. The bearish portion of the spread is a 1-point debit. Overall, then, the combination of the calendar spreads requires a 3-point debit, plus commissions.

One has sold a near-term put and call combination and purchased a longer-term combination. For nomenclature purposes, this strategy is called a "dual calendar spread." (双重跨期价差)

![FIGURE 23-4](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-23-4.png?raw=true)

In Figure 23-4, there are two profit peaks, one at each strike. Due to the way that puts and calls are priced in equity options, the peak for the call calendar (at the striking price of 70, in the example) produces a greater profit than the peak for the put calendar, at 60.

### 23.5.2 THE CALENDAR STRADDLE

Another strategy that combines calendar spreads on both put and call options can be constructed by selling a near-term straddle and simultaneously purchasing a longer-term straddle.

*Example*: Suppose that three months before January expiration, the following prices exist:

- XYZ common: 40
- January 40 straddle: 5
- April 40 straddle: 7

A calendar spread of the straddles could be established by selling the January 40 straddle and sinmltaneously buying the April 40 straddle. This would involve a cost ot 2 points, or the debit of the transaction, plus commissions.

### 23.5.3 OWNING A "FREE" COMBINATION (THE "DIAGONAL BUTTERFLY SPREAD")

This strategy consists of selling a near-term straddle and simultaneously purchasing both a longer-term, out-of-the-money call and a longer-term, out-of-the-money put.

Example: 
- XYZ common: 40
- April 35 put: 1.50
- January 40 straddle: 7
- April 45 call: 2.50

If one were to sell the short-term January 40 straddle for 7 points and simultaneously purchase the out-of-the-money put and call combination — April 35 put and April 45 call — he would eslablish a credit spread.

The credit for the position is 3 points less commissions, since 7 points are brought in from the straddle sale and 4 points are paid for the out-of-the-money combination.

Note that the position technically consists of a bearish spread in the calls (buy the higher strike and sell the lower strike) coupled with a bullish spread in the puts (buy the lower strike and sell the higher strike).
