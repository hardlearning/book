# CHAPTER 4 Other Call Buying Strategies

## 4.1 THE PROTECTED SHORT SALE (OR SYNTHETIC PUT)

Purchasing a call at the same time that one is short the underlying stock is a means of limiting the risk of the short sale to a fixed amount.

Example: An investor sells XYZ short at 40 and simultaneously purchases an XYZ July 40 call for 3 points.

Table 4-1 and Figure 4-1 depict the results at expiration from utilizing this strategy. Commissions are not included.

TABLE 4-1. Results at expiration — protected short sale.

|XYZ Price at Expiration|Profit on XYZ|Call Price at Expiration|Profit on Call|Total Profit|
|--|--|--|--|--|
|20|+$2,000|0|-$300|+$1,700|
|30|+1,000|0|-300|+700|
|37|+300|0|-300|0|
|40|0|0|-300|-300|
|50|-1,000|10|+700|-300|
|60|-2,000|20|+1,700|-300|

![FIGURE 4-1](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-4-1.png?raw=true)

Note that the break-even point is 37 in this example. That is, if the stock drops 3 points, the protected short sale position will break even because of the 3-point loss on the call.

At 43, both types of short sales have $300 losses. But above that level, the loss would continue to grow for a regular short sale, while it is fixed for the short seller who also bought a call.

A simple formula is available for determining the maximum amount of risk when one protects a short sale by buying a call option:

- Risk = Striking price of purchased call + Call price - Stock price

Depending on how much risk the short seller is willing to absorb, he might want to buy an out-of-the-money call as protection rather than an at-the-money call, as was shown in the example above.

*Example*: With XYZ at 40, the short seller of XYZ buys the July 45 call at 0.50 for protection. His maximum possible loss, if XYZ is above 45 at July expiration, would be 5.50 points (45-40+0.5). On the other hand, if XYZ declines, the protected short seller will make nearly as much as the short seller who did not protect, since he only spent 0.50 for the long call.

If one buys an in-the-money call as protection for the short sale, his risk will be quite minimal. However, his profit potential will be severely limited. As an example, with XYZ at 40, if one had purchased a July 35 call at 5.50, his risk would be limited to 0.50 anywhere above 35 at July expiration (35-40+5.5). Unfortunately, he would not realize any profit on the position until the stock went below 34.50, a drop of 5.50 points.

Generally, it is best to buy a call that is at-the-money or only slightly out-of-the-money as the protection for the short sale.

## 4.4 SYNTHETIC STRADDLE (REVERSE HEDGE)

In a reverse hedge (反向对冲) or synthetic straddle (合成跨式价差), one purchases calls on more shares than he has sold short. On stocks for which listed puts are traded, this strategy is outmoded; the same results can be better achieved by buying a straddle (a call and a put).

Example: XYZ is at 40 and an investor could short XYZ at 40 and buy 2 XYZ July 40 calls at 3 each to set up a synthetic straddle.

TABLE 4-2. Synthetic straddle at July expiration.

|XYZ Price at Expiration|Stock Profit|Profit on 2 Calls|Total Profit|
|--|--|--|--|
|20|+$2,000|-$600|+$1,400|
|25|+1,500|-600|+900|
|30|+1,000|-600|+400|
|34|+600|-600|0|
|40|0|-600|-600|
|46|-600|+600|0|
|50|-1,000|+1,400|+400|
|55|-1,500|+2,400|+900|
|60|-2,000|+3,400|+1,400|

![FIGURE 4-2](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-4-2.png?raw=true)
