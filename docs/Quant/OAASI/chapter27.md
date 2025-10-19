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

Example: The normal quarterly rate of XYZ is $1.00 per share. Suppose its special dividend in the fourth quarter has ranged from an extra $1.00 to $3.00 over the past five years. XYZ is trading at 55 about two weeks before the company is going to announce the dividend for the fourth quarter. Furthermore, suppose the January 60 put is trading at 7.50. This put has 2.50 points of time value premium. If the arbitrageur buys XYZ at 55 and also buys the January 60 put at 7.50, he is setting up a risk arbitrage. A special dividend of $1.50 plus the regular dividend of $1.00 would add up to $2.50, thus covering his risk in the position.

If a relatively high-yield stock is about to go ex-dividend, holders of the calls will attempt to sell. They do so because the stock will drop in price, thereby generally forcing the call to drop in price as well, because of the dividend.

The effect of these call holders attempting to sell their calls may often produce a discount option, and therefore a basic call arbitrage may be possible.

Since he must sell the stock to set up the arbitrage, he cannot afford to wind up the day being short any stock, for he will then have to pay out the dividend the following day. (因为他必须卖出股票来建立这个套利，在这一天结束时他不能持有这个卖空股票的头寸，否则第二天就要支付股息)

## 27.3 CONVERSIONS AND REVERSALS

A conversion consists of buying the underlying entity, and also buying a put option and selling a call option such that both options have the same terms. This position will have a locked-in profit if the total cost of the position is less than the striking price of the options.

*Example*: The following prices exist:

- XYZ common, 55;
- XYZ January 50 call, 6.50; 
- XYZ January 50 put, 1.

Suppose that these options are for 100 shares of XYZ. The total cost of this conversion is 49.50 — 55 for the stock, plus 1 for the put, less 6.50 for the call. Since 49.50 is less than the striking price of 50, there is a locked-in profit on this position. It makes no difference how far above 50 the stock might be; the result will be the same.

In a reversal, the trader sells the underlying entity short, sells a put, and buys a call. Again, the put and call have the same terms. A reversal will be profitable if the initial credit (sale price) is greater than the striking price of the options.

*Example*: A different set of prices will be used to describe a reversal:

- XYZ common, 55;
- XYZ January 60 call, 2;
- XYZ January 60 put, 7.50.

Suppose that these options are for 100 shares of XYZ. The total credit of the reversal is 60.50 — 55 from the stock sale, plus 7.50 from the put sale, less the 2-point cost of the call. Since 60.50 is greater than the striking price of the options, 60, there is a locked-in profit equal to the differential of 50 cents.

The conversion involves buying stock, and the trader will thus receive any dividends paid by the stock during the life of the arbitrage. However, the converter also has to pay out a rather large sum of money to set up his arbitrage, and must therefore deduct the cost of carrying the position from his potential profits.

In the example above, the conversion position cost 49.50 points to establish. If the trader's cost of money were 6% annually, he would thus lose $0.06/12 \times 49.50=0.2475$ point per month for each month that he holds the position. This is nearly 25 cents per month. Recall that the potential profit in the example is 50 cents, so that if one held the position for more than two months, his earning costs would wipe out his profit.

If one prefers formulae, the profit potentials of a conversion or a reversal can be stated as:

$$
\begin{aligned}
&\text{Conversion profit}=\text{Striking price}+\text{Call price}-\text{Underlying price}-\text{Put price}+\text{Dividends to be received}-\text{Carrying cost of position} \\
&\text{Reversal profit}=\text{Underlying}+\text{Put}-\text{Strike}-\text{Call}+\text{Carrying cost}-\text{Dividends}
\end{aligned}
$$

Example: It is assumed that XYZ stock is going to pay a 50-cent dividend during the life of the position, and that the position will have to be held for three months at a carrying cost of 6% per year. If the arbitrageur were interested in a conversion with a striking price of 50, and the options are for 100 shares of XYZ, his fixed cost would be:

$$
\begin{aligned}
\text{Conversion fixed cost}&=\text{Carrying rate}\times\text{Time held}\times\text{Striking price}-\text{Dividend to be received} \\
&=0.06\times\frac{3}{12}\times 50-0.50 \\
&=0.75-0.50=0.25
\end{aligned}
$$

The arbitrageur would know that if the profit potential was greater than 25 cents, he could establish the conversion for an eventual profit.

## 27.4 MORE ON CARRYING COSTS

Simplistically, the carrying cost is computed by multiplying the debit of the position by the interest rate charged and the time that the position will be held. That is, it could be formulated as:

$$
\text{Carrying cost}=\text{Strike}\times r \times t
$$

where r is the interest rate and t is the time that the position will be held. Relating this formula for the carrying cost to the conversion profit formula given above, one would get:

$$
\begin{aligned}
\text{Conversion profit}&=\text{Call}-\text{Underlying}-\text{Put}+\text{Dividends}+\text{Strike}-\text{Carrying cost} \\
&=\text{Call}-\text{Underlying}-\text{Put}+\text{Dividends}+\text{Strike}(1-rt)
\end{aligned}
$$

The absolutely correct formula to include both present value and the compounding effect would necessitate replacing the factor strike (1-rt) in the profit formula by the factor

$$
\frac{\text{Strike}}{(1+r)^t}
$$

## 27.5 BACK TO CONVERSIONS AND REVERSALS

*Example*: XYZ is going to pay a 50-cent dividend, the position will be held for three months, and the money will earn interest at a rate ot $\frac{1}{2}$ of 1% per month. If the trader were contemplating an arbitrage with a striking price of 30, the fixed cost would be:

$$
\begin{aligned}
\text{Reversal fixed cost}&=\text{Dividend to be paid}-\text{Interest rate per month}\times\text{Months held}\times\text{Striking price} \\
&=0.50-0.005\times 3\times 30 \\
&=0.50-0.045=0.005
\end{aligned}
$$

It is often possible that there will be a fixed credit (固定收入), not a fixed cost, in a reversal arbitrage.

### BORROWING STOCK TO SELL SHORT

If the stock to be sold short in the reversal were available in one of the margin accounts, the arbitrageur could borrow that stock and earn the full carrying rate on it. This is called "using box stock," since stock held in margin accounts is generally referred to as being in the "box."

Reversals are generally easier positions for the arbitrageur to locate than are conversions.

## 27.6 RISKS IN CONVERSIONS AND REVERSALS

The risks are fourfold in reversal arbitrage: An extra dividend is declared, the interest rate falls while the reversal is in place, an early assignment is received, or the stock is exactly at the striking price at expiration. Converters have similar risks: a dividend cut, an increase in the interest rate, early assignment, or the stock closing at the strike at expiration.

## 27.7 SUMMARY OF CONVERSION ARBITRAGE

The cost of money is the determining factor in the difference between put and call prices. In essence, the "cost" (although it may sometimes be a credit) is subtracted from the theoretical put price.

$$
\text{Put price}=\text{Striking price}+\text{Call price}-\text{Underlying price}-\text{Fixed cost}
$$

Furthermore, if the underlying is at the striking price, the formula reduces to:

$$
\text{Put price}=\text{Call price}-\text{Fixed cost}
$$

So, whenever the fixed cost, which is equal to the earning charge less the dividends, is greater than zero, the put will sell for less than the call if the underlying is at the striking price. Only in the case of a large-dividend-paying stock, when the fixed cost becomes negative (that is, it is not a cost, but a credit), does the reverse hold true.

## 27.8 THE "INTEREST PLAY"

The arbitrageur sells the underlying short and simultaneously buys an in-the-money call that is trading slightly over parity.

In fact, this "interest play" strategy is merely a reversal arbitrage without the short put.

If the underlying stock should drop dramatically in price, he could make large profits because he is short the underlying stock. In any case, he will make his interest credit less the amount of time value premium paid for the call less any dividends lost.

*Example 1*: XYZ is sold short at 60, and a January 50 call is bought for 10.25 points. Assume that the prevailing interest rate is 1% per month and that the position is established one month prior to expiration. XYZ pays no dividend. The total credit brought in from the trades is $4,975=(60-10.25)*100, so the arbitrageur will earn $49.75 in interest over the course of 1 month. If the stock is above 50 at expiration, he will exercise his call to buy stock at 50 and close the position. His loss on the security trades will be $25=[10.25-(60-50)]*100 — the amount of time value premium paid for the call option. (He makes 10 points by selling stock at 60 and buying at 50, but loses 10.25 points on the exercised call.) His overall profit is thus $24.75=49.75-25.

As interest rates rise, the arbitrageur can afford to pay more for the long call in this strategy, thus causing the call price to increase in times of high interest rates. If call prices are higher, so will put prices be, as the relationships necessary for conversion and reversal arbitrage are preserved.

## 27.9 THE BOX SPREAD

The short stock/long call position was called a synthetic put. That is, shorting the stock and buying a call is equivalent to buying a put. The reversal arbitrage therefore consists of selling a (listed) put and simultaneously buying a (synthetic) put. In a similar manner, the conversion is merely the purchase of a (listed) put and the simultaneous sale of a (synthetic) put.

A bull spread or a bear spread could be constructed with either puts or calls. Thus, if one were to simultaneously buy a (call) bull spread and buy a (put) bear spread, he could have an arbitrage.

*Example*: The following prices exist:

- XYZ common, 55
- XYZ January 50 call, 7
- XYZ January 50 put, 1
- XYZ January 60 call, 2
- XYZ January 60 put, 5.50

The arbitrageur could establish the box spread in this example by executing the following transactions:

||||
|--|--|--|
|Buy a call bull spread:|||
|Buy XYZ January 50 call|7 debit||
|Sell XYZ January 60 call|2 credit||
|Net call cost||5 debit|
|Buy a put bear spread:|||
|Buy XYZ January 60 put|5.5 debit||
|Sell XYZ January 50 put|1 credit||
|Net put cost||4.5 debit|
|Total cost of position||9.5 debit|

No matter where XYZ is at January expiration, this position will be worth 10 points. The arbitrageur has locked in a risk-free profit of 50 cents, since he "bought" the box spread for 9.50 points and will be able to "sell" it for 10 points at expiration.

If XYZ is above 60 at expiration, the puts will expire worthless and the call bull spread will be at its maximum potential of 10 points. Thus, the position can be liquidated for 10 points if XYZ is above 60 at expiration.

Now assume that XYZ is between 50 and 60 at expiration. In that case, the out-of-the-money, written options would expire worthless — the January 60 call and the January 50 put. This would leave a long, in-the-money combination consisting of a January 50 call and a January 60 put. These two options must have a total value of 10 points at expiration with XYZ between 50 and 60.

Finally, assume that XYZ is below 50 at expiration. The calls would expire worthless if that were true, but the remaining put spread would be at its maximum potential of 10 points. Again, the box spread could be liquidated for 10 points.

The arbitrageur must pay a cost to carry the position. In the prior example, if interest rates were 6% and he had to hold the box for 3 months, it would cost him an additional 14 cents ($0.06 \times 9.50 \times\frac{3}{12}$).

Whenever the arbitrageur observes that a call spread and a put spread using the same strikes and that are both debit spreads (支出价差) can be bought for less than the difference in the strikes plus carrying costs, he should execute the arbitrage.

It might sometimes be possible for the arbitrageur to "sell" both spreads. That is, he would establish a credit call spread and a credit put spread, using the same strikes. If this credit were greater than the difference in the striking prices, a risk-free profit would he locked in.

*Example*: Assume that a different set of prices exists:

- XYZ common, 75
- XYZ April 70 call, 8.50
- XYZ April 70 put, 1
- XYZ April 80 call, 3
- XYZ April 80 put, 6

By executing the following transactions, the box spread could be "sold":

||||
|--|--|--|
|Sell a call (bear) spread:|||
|Buy April 80 call|3 debit||
|Sell April 70 call|8.50 credit||
|Net credit on calls||5.50 credit|
|Sell a put (bull) spread:|||
|Buy April 70 put|1 debit||
|Sell April 80 put|6 credit||
|Net credit on puts||5 credit|
|Total credit of position||10.50 credit|

In this case, no matter where XYZ is at expiration, the position can be bought back for 10 points. This means that the arbitrageur has locked in risk-free profit of 50 cents.

Assume that XYZ is above 80 at April expiration. The puts will expire worthless, and the call spread will have widened to 10 points — the cost to buy it back.

If XYZ were between 70 and 80 at April expiration, the long, out-of-the-money options would expire worthless and the in-the-money combination would cost 10 points to buy back. ( For example, the arbitrageur could let himself be put at 80, buying stock there, and called at 70, selling the stock there.)

If XYZ were below 70 at expiration, the calls would expire worthless and the put spread would have widened to 10 points.

Only two questions need to be answered for establishing a risk-free arbitrage with the box spread:

1. If one were to establish a debit call spread and a debit put spread, using the same strikes, would the total cost be less than the difference in the striking prices plus carrying costs? If the answer is yes, an arbitrage exists.
2. Alternatively, if one were to sell both spread — establishing a credit call spread and a credit put spread — would the total credit received plus interest earned be greater than the difference in the striking prices? If the answer is yes, an arbitrage exists.

## 27.12 RISK ARBITRAGE USING OPTIONS

### 27.12.1 MERGERS (并购)

*Example*: XYZ, which is selling for $50 per share, offers to buy out LMN and is offering to swap one share of its (XYZ's) stock for every two shares of LMN. (每股XYZ股票兑换2股LMN股票) This would mean that LMN should be worth $25 per share if the acquisition goes through as proposed. On the day the takeover is proposed, LMN stock would probably rise to about $22 per share. The arbitrageur would sell short XYZ and, for every share that he is short, he would buy 2 shares of LMN stock. His profit potential is equal to the remaining differential between the current market price of LMN (22) and the takeover price (25).

If the acquiring company (XYZ) has in-the-money puts, then the purchase of those puts may be used instead of selling XYZ short. The advantage is that if XYZ rallies dramatically during the time it takes for the merger to take effect, then the arbitrageur's profits will be increased.

*Example*: As above, assume that XYZ is at 50 and is acquiring LMN in a 2-for-l stock deal. LMN is at 22. Suppose that XYZ rallies to 60 by the time the deal closes. This would pull LMN up to a price of 30. If one had been short 100 XYZ at 50 and long 200 LMN at 22, then his profit would be $600 — a $1,600 gain on the 200 long LMN minus a $1,000 loss on the XYZ short sale.

Assume that he buys 200 LMN as before, but now buys an XYZ July 55 put with little time premium, say at 5.50 points, then he would have nearly the same dollars of profit if the merger should go through with XYZ below 55.

However, when XYZ rallies to 60, his profit increases. He would still make the $1,600 on LMN as it rose from 22 to 30, but now would only lose $550 on the XYZ put — a total profit of $1,050 as compared to $600 with an all-stock position.

It is necessary to have a plus tick in order to sell stock short. When many arbitrageurs are trying to sell a stock short at the same time, it may be difficult to sell such stock short. (要卖空股票时，需遵守正点价差规则，即卖空的价格不得低于前一成交价。如果许多套利者在同时卖空同一股票，那就不容易在这个股票上卖空。)

### 27.12.2 LIMITS ON THE MERGER

In some merger situations, the acquiring company (XYZ) promises to give the shareholders of the company being acquired (LMN) an amount of stock equal to a set dollar price. This amount of stock would be paid even if the acquiring company rose or fell moderately in price.

*Example*: The company says that it wants the offer to be worth $25 per share to LMN shareholders as long as XYZ is between 45 and 55. Given this information, we can determine the maximum and minimum number of shares that LMN shareholders will receive: The maximum is the stated price, 25, divided by the lower limit, 45, or 0.556 shares; the minimum is 25 divided by the higher limit, 55, or 0.455.

A merger of this type is said to have "hooks" — the prices at which the ratio steadies. This makes it difficult to arbitrage.

Problems arise if XYZ begins to fall below 45 well before the closing of the merger, the lower "hook" in the merger. If it should remain below 45, then one should set up the arbitrage as being short 0.556 shares of XYZ for each share of LMN that is held long.

*Example*: A merger is announced as described in the preceding example: XYZ is to acquire LMN at a stated value of $25 per share, with the stipulation that each share of LMN will be worth at least 0.455 shares of XYZ and at most 0.556 shares. These share ratios equate to prices of 45 and 55 on XYZ.

Suppose that XYZ drops immediately in price after the merger is announced, and it falls to 40. Furthermore, suppose that the merger is expected to close sometime during July and that there are XYZ August 45 puts trading at 5.50. This represents only 50 cents time value premium. The arbitrageur could then set up the arbitrage by buying 10,000 LMN and buying 56 of those puts. Smaller investors might buy 1,000 LMN and buy 6 puts. Either of these is in approximately the proper ratio of 1 LMN to 0.556 XYZ.

### 27.12.3 TENDER OFFERS (要约收购)

In a tender offer, the acquiring company normally offers to exchange cash for shares of the company to be acquired. (兼并公司通常用现金交换被兼并公司的股票)

*Example*: XYZ proposes to buy back part of its own stock. It has offered to pay $70 per share for half the company. Based on the fundamentals of the company, it is expected that the remaining stock will sell for approximately $40 per share. Thus, the average share of XYZ is worth 55 if the tender offer is completed (one-half can be sold at 70, and the other half will be worth 40).

There are two ways to make money in this situation. One is to buy XYZ at the current price, say 52, and tender it. The remaining portion would be sold at the lower price, say 40, when XYZ reopened after the tender expired. This method would yield a profit of $3=(40+70)/2-52 per share if exactly 50% of the shares are accepted at 70 in the tender offer.

The other way to trade this tender offer might be to buy puts on XYZ.

*Example*: XYZ is at 52. As before, there is a tender offer for half the stock at 70, with no plans for the remainder. The July 55 puts sell for 15, and the July 50 puts sell for 10. It is common that both puts would be predicting the same price in the after-market: 40.

|||
|--|--|
|Initial purchase:||
|Buy 200 XYZ at 52|10,400 debit|
|Buy 1 July 50 put at 10|1,000 debit|
|Total Cost|$11,400 debit|
|Closing sale:||
|Sell 100 XYZ at 70 via tender|7,000 credit|
|Sell 100 XYZ at 50 via put exercise|5,000 credit|
|Total proceeds|$12,000|
|Total profit: $600||
