# CHAPTER 9 Calendar Spreads

A calendar spread (跨期价差), also frequently called a time spread, involves the sale of one option and the simultaneous purchase of a more distant option, both with the same striking price.

The neutral philosophy for using calendar spreads is that time will erode the value of the near-term option at a faster rate than it will the far-term option. If this happens, the spread will widen and a profit may result at near-term expiration.

Example: The following prices exist sometime in late January:

- XYZ: 50

|April 50 Call <br> (3-month call)|July 50 Call <br> (6-month call)|October 50 Call <br> (9-month call)|
|--|--|--|
|5|8|10|

If one sells the April 50 call and buys the July 50 at the same time, he will pay a debit of 3 points plus commissions.

Furthermore, suppose that in 3 months, at April expiration, XYZ is unchanged at 50. Then the 3-month call should be worth 5 points, and the 6-month call should be worth 8 points, as they were previously, all other factors being equal.

|April 50 Call <br> (Expiring)|July 50 Call <br> (3-month call)|October 50 Call <br> (6-month call)|
|--|--|--|
|0|5|8|

The spread between the April 50 and the July 50 has now widened to 5 points. Since the spread cost 3 points originally, this widening effect has produced a 2-point profit.

## 9.1 THE NEUTRAL CALENDAR SPREAD

The calendar spread that is established when the underlying stock is at or near the striking price of the options used is a neutral spread.

TABLE 9-1. Estimated profit or losses at April expiration.

|XYZ Stock Price|April 50 Price|April 50 Profit|July 50 Price|July 50 Profit|Total Profit|
|--|--|--|--|--|--|
|40|0|+$500|0.50|-$750|-$250|
|45|0|+500|2.50|-550|-50|
|48|0|+500|4|-400|+100|
|50|0|+500|5|-300|+200|
|52|2|+300|6|-200|+100|
|55|5|0|8|0|0|
|60|10|-500|10.50|+250|-250|

![FIGURE 9-1](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-9-1.png?raw=true)

The graph is a curved rather than straight line, since the July 50 call still has time premium.

There is a range within which the spread is profitable at near-term expiration. That range would appear to be about 46 to 55 in the example. Outside that range, losses can occur, but they are limited to the amount of the initial debit.

## 9.3 THE BULLISH CALENDAR SPREAD

In a bullish calendar spread, one sells the near-term call and buys a longer-term call, but he does this when the underlying stock is some distance below the striking price of the calls.

Example: One might set up a bullish calender spread in the following manner:

- XYZ common, 45;
- sell the XYZ April 50 for 1; and
- buy the XYZ July 50 for 1.50.

If the April 50 call expires worthless, the investor will own the fuly 50 call at a net cost of 0.50, plus commissions.

If XYZ were to rally to only 52 between April and July, the July 50 call could be sold for at least 2 points. This represents a substantial percentage gain, because the cost of the call has been reduced to 50 cents.

This strategy is a reasonable way to speculate, provided that the spreader adheres to the following criteria when establishing the spread:

1. Select underlying stocks that are volatile enough to move above the striking price within the alloted time.
2. Do not use options more than one striking price above the current market. (不要使用高于当前市价1档行权价的期权)
3. Do not invest a large percentage of available trading capital in bullish calendar spreads.
