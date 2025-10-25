# CHAPTER 13 Reverse Spreads

## 13.1 REVERSE CALENDAR SPREAD

The reverse calendar spread (反向跨期价差) is a position that is just the opposite of a "normal" calendar spread. In the reverse calendar spread, one sells a long-term call option and simultaneously buys a shorter-term call option.

This strategy will make money if one of two things happens: Either (1) the stock price moves away from the striking price by a great deal, or (2) the implied volatility of the options involved in the spread shrinks.

*Example*: Suppose the current month is April and that XYZ is trading at 80.

- XYZ December 80 call: 12
- XYZ July 80 call: 7

A reverse calendar spread is established by selling the December 80 call for 12 points, and buying the July 80 call for 7, a net credit of 5 points for the spread.

If XYZ were to fall to 50 in a month or so, the July 80 call would be nearly worthless and the December 80 call could be bought back for about a point. Thus, the spread would have shrunk from its initial price of 5 to a price of about 1, a profit of 4 points.

The other way to make money would be for implied volatility to decrease. Suppose implied volatility dropped after a month had passed. Then the spread might be worth something like 4 points — an unrealized profit of about 1 point, since it was sold for a price of 5 initially.

The profit graph in Figure 13-1 shows the profitability of the reverse calendar.

![FIGURE 13-1](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-13-1.png?raw=true)

## 13.2 REVERSE RATIO SPREAD (BACKSPREAD)

A more popular reverse strategy is the reverse ratio call spread (反向看涨期权比率价差), which is commonly known as a backspread (后式价差). In this type of spread, one would sell a call at one striking price and then would buy several calls at a higher striking price. This is exactly the opposite of the ratio spread (比率价差).

*Example*: XYZ is selling for 43 and the July 40 call is at 4, with the July 45 call at 1. A reverse ratio spread would be established as follows:

- Buy 2 July 45 calls at 1 each: 2 debit
- Sell 1 July 40 call at 4: 4 credit
- Net: 2 credit

Table 13-1 and Figure 13-2 depict the potential profits and losses from this example of a reverse ratio spread. Note that the profit graph is exactly like the profit graph of a ratio spread that has been rotated around the stock price axis.

TABLE 13-1. Profits and losses for reverse ratio spread.

|XYZ Price at July Expiration|Profit on 1 July 40|Profit on 2 July 45's|Total Profit|
|--|--|--|--|
|35|+$400|-$200|+$200|
|40|+400|-200|+200|
|42|+200|-200|0|
|45|-100|-200|-300|
|48|-400|+400|0|
|55|-1,100|+1,800|+700|
|70|-2,600|+4,800|+2,200|

![FIGURE 13-2](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-13-2.png?raw=true)

The strategy is actually a long call added to a bear spread.

Notice that the concept of a delta-neutral spread can be utilized in this strategy.

*Example*: The neutral ratio is determined by dividing the delta of the July 45 into the delta of the July 40.

||Prices|Delta|
|--|--|--|
|XYZ common:|43||
|XYZ July 40 call:|4|0.80|
|XYZ July 45 call:|1|0.35|

In this case, that would be a ratio of 2.29:1 (0.80/0.35). That is, if one sold 5 July 40's, he would buy 11 July 45's (or if he sold 10, he would then buy 23).
