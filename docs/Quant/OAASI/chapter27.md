# CHAPTER 27 Arbitrage

## 27.1 BASIC PUT AND CALL ARBITRAGE ("DISCOUNTING")

In these situations, the arbitrageur attempts to buy the option at a discount (贴水) while simultaneously taking an opposite position in the underlying stock. He can then exercise his option immediately and make a profit equal to the amount of the discount.

Discount options generally either are quite deeply in-the-money or have only a short time remaining until expiration.

*Example*: XYZ is trading at 58 and the XYZ July 50 call is trading at 7.90. The call is actually at a discount from parity of 10 cents.

1. buying the call at 7.90;
2. selling the stock at 58;
3. exercising the call to buy the stock at 50.

The arbitrageur would make 8 points of profit from the stock, having sold it at 58 and bought it back at 50 via the option exercise. He loses the 7.90 points that he paid for the call option, but this still leaves him with an overall profit of 10 cents.

*Example*: XYZ is at 58 and the XYZ July 70 put is at 11.90. With the put at a 10-cent discount from parity, the arbitrageur might take the following action:

1. Buy put at 11.90.
2. Buy stock at 58.
3. Exercise put to sell stock at 70.

The stock transaction is a 12-point profit, since the stock was bought at 58 and is sold at 70 via the put exercise. The cost of the put — 11.90 points — is lost, but the arbitrageur still makes a 10-cent profit.

There may be occasions when the option markets are larger than the corresponding stock quotes. When this happens, the arbitrageur has an alternative available to him: He might sell an in-the-money option at parity rather than take a stock position.

*Example*: XYZ is at 58 and the XYZ July 50 call is at 7.90. For example, if the XYZ July 40 call could be sold at 18 (parity), the arbitrage could still be established. If he is assigned on the July 40 that he is short, he will then be short stock at a net price of 58 — the striking price of 40, plus the 18 points that were brought in from the sale of the July 40 call. (卖空股票58的净价格，相当于行权价40，再加上卖出7月看涨期权时得到18) Thus, the sale of the in-the-money call at parity is equivalent to shorting the stock for the arbitrage purpose.

In a similar manner, an in-the-money put can be used in the basic put arbitrage.

*Example*: With XYZ at 58 and the July 70 put at 11.90, the arbitrage could be established. Suppose the XYZ July 80 put could be sold at 22. This would be the same as buying the stock at 58, because if the put were assigned, the arbitrageur would be forced to buy stock at 80 — the striking price — but his net cost would be 80 minus the 22 points he received from the sale of the put, for a net cost of 58.

In actual practice, if an in-the-money option is at a discount, an even deeper in-the-money option will generally be at a discount as well. The arbitrageur would normally try to sell, at parity, an option that was less deeply in-the-money than the one he is discounting.

## 27.2 DIVIDEND ARBITRAGE

In theory, on the day before a stock goes ex-dividend (除息), all puts should have a time value premium at least as large as the dividend amount.

*Example*: Suppose the XYZ July 50 put is selling for 5.90, with the stock at 45 and about to go ex-dividend by $1. The arbitrageur can take the following steps:

1. Buy the put at 5.90.
2. Buy the stock at 45.
3. Hold the put and stock until the stock goes ex-dividend (1 point in this case).
4. Exercise the put to sell the stock at 50.

The trader makes 5 points from the stock trade, buying it at 45 and selling it at 50 via the put exercise, and also collects the 1-point dividend, for a total inflow of 6 points. Since he loses the 5.90 points he paid for the put, his net profit is 10 cents.

The arbitrageur has a carrying cost (持有成本) for the money that he must tie up in the long stock. This carrying cost fluctuates with short-term interest rates.

*Example*: If the current rate of carrying charges were 6% annually, this would be equivalent to 1% every 2 months. If the arbitrageur were to establish this example position 2 months prior to expiration, he would have a carrying cost of 0.5075 point. (His total outlay is 50.90 points, 45 for the stock and 5.90 for the options, and he would pay 1% to carry that stock and option for the two months until the ex-dividend date.) This is more than 50 cents in costs — clearly more than the 10-cent potential profit.

The arbitrageur should note that this strategy of buying the put and buying the stock to pick up the dividend might have a residual, rather profitable side effect (副作用). If the underlying stock should rally up to or above the striking price of the put, there could be rather large profits in this position.

Risk arbitrage is a strategy that is designed to lock in a profit if a certain event occurs. If that event does not occur, there could be a loss (usually quite limited).
