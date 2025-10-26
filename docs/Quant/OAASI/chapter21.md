# CHAPTER 21 Synthetic Stock Positions Created by Puts and Calls

It is possible for a strategist to establish a position that is essentially the same as a stock position, and he can do this using only options. The strategies are summarized by:

1. Buy call and sell put instead of buying stock.
2. Buy put and sell call instead of selling stock short.

## 21.1 SYNTHETIC LONG STOCK

When one buys a call and sells a put at the same strike, he sets up a position that is equivalent to owning the stock. His position is sometimes called "synthetic" long stock (合成股票多头).

Example: Suppose that the following prices exist:

- XYZ common, 50;
- XYZ January 50 call, 5; and
- XYZ January 50 put, 4.

If one were bullish on XYZ and wanted to buy stock at 50, he might consider the alternative strategy of buying the January 50 call and selling (uncovered) the January 50 put.

TABLE 21-1. Synthetic long stock position.

|XYZ Price of Expiration|January 50 Call Result|January 50 Put Result|Total Option Result|Long Stock Result|
|--|--|--|--|--|
|40|-$500|-$600|-$1,100|-$1,000|
|45|-500|-100|-600|-500|
|50|-500|+400|-100|0|
|55|0|+400|+400|+500|
|60|+500|+400|+900|+1,000|

The table shows that the result of the option strategy is exactly $100 less than the stock results for any price at expiration. The reason there is a difference in the results of the two equivalent positions lies in the fact that the option strategist had to pay 1 point of time premium in order to set up his position. That $100 represents the carrying cost of the stock and the dividends to be paid.

## 21.2 SYNTHETIC SHORT SALE

A position that is equivalent to the short sale of the underlying stock can he established by selling a call and siniidtaiwously buying a put.

Using the prices above — XYZ at 50, January 50 call at 5, and January 50 put at 4 — Table 21-2 depicts the potential profits and losses at January expiration.

TABLE 21-2. Synthetic short sale position.

|XYZ Price at Expiration|January 50 Call Result|January 50 Put Result|Total Option Result|Short Stock Result|
|--|--|--|--|--|
|40|+$500|+$600|+$1,100|+$1,000|
|45|+500|+100|+600|+500|
|50|+500|-400|+100|0|
|55|0|-400|-400|-500|
|60|-500|-400|-900|-1,000|

The option strategy does better than the stock position, because the option strategist is getting the benefit of the time value premium.

## 21.3 SPLITTING THE STRIKES

The strategist may be able to use a slight variation of the synthetic strategy to set up an aggressive, but attractive, position. Rather than using the same striking price for the put and call he can use a lower striking price for the put and a higher striking price for the call.

### 21.3.1 BULUSHLY ORIENTED

If an out-of-the-money put is sold naked, and an out-of-the-money call is simultaneously purchased, an aggressive bullish position is established.

*Example*: The following prices exist: XYZ is at 53, a January 50 put is selling for 2, and a January 60 call is selling for 1. An investor who is bullish on XYZ sells the January 50 put naked and simultaneously buys the January 60 call.

TABLE 21-3. Bullishly split strikes.

|XYZ Price at Expiration|January 50 Put Profit|January 60 Call Profit|Total Profit|
|--|--|--|--|
|40|-$800|-$100|-$900|
|45|-300|-100|-400|
|50|+200|-100|+100|
|55|+200|-100|+100|
|60|+200|-100|+100|
|65|+200|+400|+600|
|70|+200|+900|+1,100|

![FIGURE 21-1](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-21-1.png?raw=true)

### 2.3.2 BEARISHLY ORIENTED

There is a companion strategy for the investor who is bearish on a stock. He could attempt to buy an out-of-the-money put and write an out-of-the-money call naked.

*Example*: With XYZ at 65, the bearish investor buys a February 60 put for 2 points, and simultaneously sells a February 70 call for 3 points. These trades bring in a credit of 1 point, less commissions.

TABLE 21-4. Bearishly split strikes.

|XYZ Price at Expiration|February 60 Put Profit|February 70 Call Profit|Total Profit|
|--|--|--|--|
|50|+$800|+$300|+$1,100|
|55|+300|+300|+600|
|60|-200|+300|+100|
|65|-200|+300|+100|
|70|-200|+300|+100|
|75|-200|-200|-400|
|80|-200|-700|-900|

![FIGURE 21-2](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-21-2.png?raw=true)

This strategy of splitting the strikes in a bearish manner is used very frequently in conjunction with the ownership of common stock. That is, a stock owner who is looking to protect his stock will buy an out-of-the-money put and sell an out-of-the-money call to finance the put purchase. This strategy is called a "protective collar".
