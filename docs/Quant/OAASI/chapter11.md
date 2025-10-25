# CHAPTER 11 Ratio Call Spreads

A ratio call spread (看涨期权比率价差) is a neutral strategy in which one buys a number of calls at a lower strike and sells more calls at a higher strike. It is somewhat similar to a ratio write (卖出比率) in concept, although the spread has less downside risk and normally requires a smaller investment than does a ratio write.

*Example*: The following prices exist:

- XYZ common, 44;
- XYZ April 40 call, 5; and
- XYZ April 45 call, 3.

A 2:1 ratio call spread could be established by buying one April 40 call and simultaneously selling two April 45's. This spread would be done for a credit of 1 point (3*2-5).

TABLE 11-1. Ratio call spread.

|XYZ Price at Expiration|April 40 Call Profits|April 45 Call Profits|Total Profits|
|--|--|--|--|
|35|-$500|+$600|+$100|
|40|-500|+600|+100|
|42|-300|+600|+300|
|45|0|+600|+600|
|48|+300|0|+300|
|51|+600|-600|0|
|55|+1,000|-1,400|-400|
|60|+1,500|-2,400|-900|

![FIGURE 11-1](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-11-1.png?raw=true)

In a 2:1 ratio spread, two calls are sold for each one purchased. The maximum profit amount and the upside break-even point can easily be computed by using the following formulae:

- Points of maximum profit = Initial credit + Difference between strikes or = Difference between strikes - Initial debit
- Upside break-even point = Higher strike price + Points of maximum profit

In the preceding example, the initial credit was 1 point, so the points of maximum profit = 1 + 5 = 6, or $600. The upside break-even point is then 45 + 6 = 51.
