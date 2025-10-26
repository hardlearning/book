# CHAPTER 20 The Sale of a Straddle

Selling a straddle involves selling both a put and a call with the same terms.

## 20.1 THE COVERED STRADDLE WRITE

In the covered straddle writing strategy (卖出备兑跨式价差), one owns the underlying stock and simultaneously writes a straddle on that stock.

In reality, this position is not totally covered — only the sale of the call is covered by the ownership of the stock. The sale of the put is uncovered.

*Example*: XYZ is at 51 and an XYZ January 50 call is selling for 5 points while an XYZ January 50 put is selling for 4 points. A covered straddle write would be established by buying 100 shares of the underlying stock and simultaneously selling one put and one call.

The covered straddle write is actually a covered write — long 100 shares of XYZ plus short one call — coupled with a naked put write. Since the naked put write is equivalent to a covered call write, this position can be thought of either as the equivalent of a 200-share covered call write, or as the sale of two uncovered puts.

- Maximum profit = Straddle premium + Striking price - Initial stock price
- Break-even price = (Stock price + Strike price - Straddle premium) / 2

The amount of maximum profit in this example is 800=(9+50-51)*100.

The break-even point in this example is 46=(51+50-9)/2.

TABLE 20-1. Results at expiration of covered straddle write.

|Stock Price|(A) 100-Shore Covered Write|(B) Put Write|Covered Straddle Write (A + B)|
|--|--|--|--|
|35|-$1,100|-$1,100|-$2,200|
|40|-600|-600|-1,200|
|46|0|0|0|
|50|+400|+400|+800|
|60|+400|+400|+800|

![FIGURE 20-1](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-20-1.png?raw=true)

## 20.2 THE UNCOVERED STRADDLE WRITE

In an uncovered straddle write (卖出无备兑跨式价差), one sells the straddle without owning the underlying stock.

Example: The following prices exist:

- XYZ common, 45;
- XYZ January 45 call, 4; and
- XYZ January 45 put, 3.

A straddle could be sold for 7 points. If the stock were above 38 and below 52 at expiration, the straddle writer would profit, since the in-the-money option could be bought back for less than 7 points in that case, while the out-of-the-money option expires worthless.

TABLE 20-2. The naked straddle write.

|XYZ Price of Expiration|Call Profit|Put Profit|Total Profit|
|--|--|--|--|
|30|+$400|-$1,200|-$800
|35|+400|-700|-300|
|38|+400|-400|0|
|40|+400|-200|+200|
|45|+400|+300|+700|
|50|-100|+300|+200|
|52|-300|+300|0|
|55|-600|+300|-300|
|60|-1,100|+300|-800|

![FIGURE 20-2](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-20-2.png?raw=true)

The ratio call writing strategy (卖出看涨期权比率) — buying 100 shares of the underlying stock and selling two calls — has the same profit graph.

## 20.7 STRANGLE (COMBINATION) WRITING

strangle write is usually established by selling both an out-of-the-money put and an out-of-the-money call with the stock approximately centered between the two striking prices.

Example: Given the following prices:

- XYZ common, 65;
- XYZ January 70 call, 4; and
- XYZ January 60 put, 3,

a strangle write would be established by selling the January 70 call and the January 60 put.

TABLE 20-3. Results of a combination write.

|Stock Price at Expiration|Call Profit|Put Profit|Total Profit|
|--|--|--|--|
|40|+$400|-$1700|-$1,300|
|50|+400|-700|-300|
|53|+400|-400|0|
|57|+400|0|+400|
|60|+400|+300|+700|
|65|+400|+300|+700|
|70|+400|+300|+700|
|73|+100|+300|+400|
|77|-300|+300|0|
|80|-600|+300|-300|
|90|-1,600|+300|-1,300|

![FIGURE 20-3](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-20-3.png?raw=true)
