# CHAPTER 2 Covered Call Writing

Covered call writing (卖出备兑看涨期权) is the name given to the strategy by which one sells a call option while simultaneously owning the obligated number of shares of underlying stock.

## 2.1 THE IMPORTANCE OF COVERED CALL WRITING

### 2.1.1 COVERED CALL WRITING FOR DOWNSIDE PROTECTION

Example: An investor owns 100 shares of XYZ common stock, which is currently selling at 48 per share. If this investor sells an XYZ July 50 call option while still holding his stock, he establishes a covered write. Suppose the investor receives 300 from the sale of the July 50 call. If XYZ is below 50 at July expiration, the call option that was sold expires worthless and the investor earns the 300 that he originally received for writing the call. Thus, he receives 300, or 3 points, of downside protection.

### 2.1.2 THE BENEFITS OF AN INCREASE IN STOCK PRICE

*Example*: If XYZ is at or just below 50 at July expiration, the call still expires worthless, and the investor makes the 300 from the option in addition to having a small profit from his stock purchase.

Should XYZ increase in price by expiration to levels above 50, the covered writer has a choice of alternatives. As one alternative, he could do nothing, in which case the option would be assigned and his stock would be called away at the striking price of 50. In that case, his profits would be equal to the 300 received from selling the call plus the profit on the increase of his stock from the purchase price of 48 to the sale price of 50. If as another alternative he desires to retain his stock ownership, he can elect to buy back (or cover) the written call in the open market.

*Example*: XYZ rises to a price of 60 by July expiration. The call option then sells near its intrinsic value of 10. If the investor covers the call at 10, he loses 700 on the option portion of his covered write. (Recall that he originally received 300 from the sale of the option, and now he is buying it back for $1,000.) However, he relieves the obligation to sell his stock at 50 by buying back the call, so he has an unrealized gain of 12 points in the stock, which was purchased at 48. His total profit, including both realized and unrealized gains, is 500.

This profit is exactly the same as he would have made if he had let his stock be called from him. If called, he would keep the 300 from the sale of the call, and he would make 2 points (200) from buying the stock at 48 and selling it at 50. This profit, again, is a total of 500.

The profit potential and break-even point of a covered write can be summarized as follows:

- Maximum profit potential = Strike price - Stock price + Call price
- Downside break-even point = Stock price - Call price

### 2.1.3 QUANTIFICATION OF THE COVERED WRITE

Table 2-1 and Figure 2-1 depict the profit graph for the example involving the XYZ covered write of the July 50 call. The table makes the assumption that the call is bought back at parity. If the stock is called away the same total profit of 500 results; but the price involved on the stock sale is always 50, and the option profit is always 300.

TABLE 2-1. The XYZ July 50 call.

|XYZ Prite ot Expiration|Stock Profit|July 50 Call at Expiration|Call Profit|Total Profit|
|--|--|--|--|--|
|40|-$800|0|+$300|-$500|
|45|-300|0|+300|0|
|48|0|0|+300|+300|
|50|+200|0|+300|+500|
|55|+700|5|-200|+500|
|60|+1,200|10|-700|+500|

![FIGURE 2-1](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-2-1.png?raw=true)

The break-even point is 45 (zero total profit) with risk below 45; the maximum profit attainable is 500 if the position is held until expiration; and the profit if the stock price is unchanged is 300.

## 2.2 COVERED WRITING PHILOSOPHY
