# CHAPTER 17 Put Buying in Conjunction with Common Stock Ownership

When one sinmltaneously owns both the common stock and a put on that same stock, he has a position with limited downside risk during the life of the put. This position is also called a synthetic long call (合成看涨期权多头), because the profit graph is the same shape as a long call's.

*Example*: An investor owns XYZ stock, which is at 52. and purchases an XYZ October 50 put for 2. The put gives him the right to sell XYZ at 50, so the most that the stockholder can lose on his stock is 2 points.

TABLE 17-1. Results at expiration on a protected stock holding.

|XYZ Price at Expiration|Stock Profit|Put Profit|Total Profit|
|--|--|--|--|
|30|$2,200|+$1,800|-$400|
|40|-1,200|+800|-400|
|50|-200|-200|-400|
|54|+200|-200|0|
|60|+800|-200|+600|
|70|+1,800|-200|+1,600|
|80|+2,800|-200|+2,600|

![FIGURE 17-1](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-17-1.png?raw=true)

## 17.3 PUT BUYING AS PROTECTION FOR THE COVERED CALL WRITER

The covered call writing strategy involves the purchase of stock and the sale of a call option against that stock. This strategy is known as a protective collar or, more simply, a "collar."

The purchase of an out-of-the-money put option can eliminate the risk of large potential losses for the covered write, although the money spent for the put purchase will reduce the overall return from the covered write.

*Example*: XYZ is at 39 and there is an XYZ October 40 call selling for 3 points and an XYZ October 35 put selling for 0.50. A covered write could be established by buying the common at 39 and selling the October 40 call for 3. By also purchasing the October 35 put at the time the covered write is initiated, the maximum profit potential is 3.50 points at October expiration. The break-even point moves up to 36.50, and the most that the writer could lose would be 1.50 points if XYZ were below 35 at expiration.

TABLE 17-2. Comparison of regular and protected covered writes.

|XYZ Price at Expiration|Stock Profit|October 40 Call Profit|October 35 Put Profit|Total Profit|
|--|--|--|--|--|
|25|-$1,400|+$300|+$950|-$150
|30|-900|+300|+450|-150|
|35|-400|+300|-50|-150|
|36.50|-250|+300|-50|0|
|38|-100|+300|-50|+150|
|40|+100|+300|-50|+350|
|45|+600|-200|-50|+350|
|50|+1,100|-700|-50|+350|

![FIGURE 17-2](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-17-2.png?raw=true)

This strategy is equivalent to the bull spread.

## 17.4 NO-COST COLLARS

The "collar" strategy is often arrived at in another manner: a stockholder begins to worry about the downside potential of the stock market. If he buys an out-of-the-money put, he might be able to sell an out-of-the-money call whose proceeds completely cover the cost of the put. Thus, he has established a protective collar at no cost — at least no debit.
