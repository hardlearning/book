# CHAPTER 37 How Volatility Affects Popular Strategies

## 37.1 VEGA

Vega is the amount by which an option's price changes when volatility changes by one percentage point.

*Example*: XYZ is selling at 50, and the July 50 call is trading at 7.25. Assume that there is no dividend, that short-term interest rates are 5%, and that July expiration is exactly three months away. With this information, one can determine that the implied volatility of the July 50 call is 70%. If implied volatility were to rise to 71%, the July 50 call would theoretically be worth 7.35. Hence, the vega of this option is 0.10=(7.35-7.25)/(71-70).

If implied volatility increases, the price of the option will increase, and if implied volatility decreases, the price of the option will decrease.

In fact, it can be stated that a call and a put with the same terms have the same vega.

*Example*: In this case, let the stock price fluctuate while holding interest rate (5%), implied volatility (70%), time (3 months), dividends (0), and the strike price (50) constant.

|Stock Price|Implied Volatility July 50 Call Price|Theoretical Call Price|Vega|
|--|--|--|--|
|30|70%|0.47|0.028|
|40||2.62|0.073|
|50||7.25|0.098|
|60||14.07|0.092|
|70||22.35|0.091|

Example: In this example, the following items are held fixed: stock price (50), strike price (50), implied volatility (70%), risk-free interest rate (5%), and dividend (0). But now, we let time fluctuate.

|Stock Price|Implied Volatility|Time Remaining|Theoretical Call Price|Vega|
|--|--|--|--|--|
|50|70%|One year|14.60|0.182|
|||Six months|10.32|0.135|
|||Three months|7.25|0.098|
|||Two months|5.87|0.080|
|||One month|4.16|0.058|
|||Two weeks|2.87|0.039|
|||One week|1.96|0.028|
|||One day|0.73|0.010|

The passage of time (时间流逝) results not only in a decreasing call price, but in a decreasing vega as well.

*Example*: Again, some factors will be kept constant — the stock price (50), the time to July expiration (3 months), the risk-free interest rate (5%), and the dividend (0).

|Stock Price|Implied Volatility|Theoretical Call Price|Vega|
|--|--|--|--|
|50|10%|1.34|0.097|
||30%|3.31|0.099|
||50%|5.28|0.099|
||70%|7.25|0.098|
||100%|10.16|0.096|
||150%|14.90|0.093|
||200%|19.41|0.088|

Vega is surprisingly constant over a wide range of implied volatilities. Vega begins to decline only if implied volatility gets exceedingly high.

## 37.2 IMPLIED VOLATILITY AND DELTA

When implied volatility gets very high, the delta of the option doesn't change much.

## 37.3 EFFECTS ON NEUTRALITY

the "delta-neutral" spread is a spread whose profitability is supposedly ambivalent to market movement, at least for short time frames and limited stock price changes.

*Example*: Suppose that XYZ is trading at 100, that the options have an implied volatility of 40%, and that one is considering buying a six-month straddle with a striking price of 100. The following data summarize the situation, including the option prices and the deltas:

> XYZ Common: 100; Implied Volatility: 40%

|Option|Price|Delta|
|--|--|--|
|XYZ October 100 call|12.00|0.60|
|XYZ October 100 put|10.00|-0.40|

The delta of the call is 1.5 times that of the put (in absolute value). One must buy three puts and two calls in order to have a delta-neutral position.

Most experienced option traders know that the delta of an at-the-money calls is somewhat higher than that of an at-the-money put.

> AAA Common: 100; Implied Volatility: 110%

|Option|Price|Delta|
|--|--|--|
|AAA October 100 call|31.00|0.67|
|AAA October 100 put|28.00|-0.33|

The delta-neutral ratio here is two-to-one (67 divided by 33), not three-to-two as in the earlier case — even though both stock prices are 100 and both sets of options have six months remaining.

A trader wishing to remain delta-neutral must monitor not only changes in stock price, but changes in implied volatility as well.

## 37.4 POSITION VEGA

The "position vega" is merely the quantity of options held, times the vega, times the shares per options (which is normally 100).

*Example*: Using a simple call spread as an example, assume the following prices exist:

|Security|Position|Vega|Position Vega|
|--|--|--|--|
|XYZ Stock|No position|||
|XYZ July 50 call|Long 3 calls|0.098|+0.294|
|XYZ July 70 call|Short 5 calls|0.076|-0.380|
|Net Position Vega:|||-0.086|

A negative position vega indicates that the position will profit if implied volatility decreases. A positive position vega indicates that the position will profit if implied volatility rises.

## 37.5 OUTRIGHT OPTION PURCHASES AND SALES

An increase in implied volatility can overcome days, even weeks, of time decay.

Example: Suppose that XYZ is trading at 100 and one is interested in analyzing a 3-month call with striking price of 100. Furthermore, suppose that implied volatility is currently at 20%. Given these assumptions, the Black-Scholes model tells us that the call would be trading at a price of 4.64.

- Stock Price: 100
- Strike Price: 100
- Time Remaining: 3 months
- Implied Volatility: 20%
- Theoretical Call Value: 4.64

Now, suppose that a month passes. If implied volatility remained the same (20%), the call would lose nearly a point of value due to time decay. Implied volatility had to increase to 26% completely counteract the effect of that time decay.

- Stock Price: 100
- Strike Price: 100
- Time Remaining: 2 months
- Implied Volatility: 25.9%
- Theoretical Call Value: 4.64

An experienced option trader knows that many stocks have implied volatilities that can fluctuate in the 20% to 40% range quite easily.

Implied volatility often explodes during a market crash.

|Stock Price|Implied Volatility Necessary for Call to Maintain Value|
|--|--|
|100|20% (the initial parameters)|
|95|33%|
|90|44%|
|85|55%|
|80|67%|
|75|78%|
|70|89%|

## 37.6 TIME VALUE PREMIUM IS A MISNOMER

An option’s price is composed of two parts: (1) intrinsic value, which is the "real" part of the option's value — the distance by which the option is in-the-money, and (2) "excess value" — often called time value premium.

The five factors influencing excess value are:

1. stock price movements,
2. changes in implied volatility,
3. the passage of time,
4. changes in the dividend (if any exist), and
5. changes in interest rates.

In fact, to measure them one uses the "greeks": delta, vega, theta (there is no "greek" for dividend change), and rho.

If implied volatility increases, the excess value portion of the option will increase and, if implied volatility decreases, so will excess value.

If the call is in-the-money, then an increase in stock price will result in a decrease of excess value. That is, a deeply in-the-money option is composed primarily of intrinsic value, while excess value is quite small. However, when the call is out-of-the-money, the effect is just the opposite: Then, an increase in call price will result in an increase in excess value, because the stock price increase is bringing the stock closer to the option's striking price.

The part of the delta that addresses excess value is this:

- Out-of-the-money call: 100% of the delta affects the excess value.
- In-the-money call: "1.00 minus delta" affects the excess value. (So, if a call is very deeply in-the-money and has a delta of 0.95, then the delta only has 1.00-0.95, or 0.05, room to increase. Hence it has little effect on what small amount of excess value remains in this deeply in-the-money call.)

## 37.7 VOLATILITY AND THE PUT OPTION

A put option tends to lose its premium fairly quickly as it becomes an in-the-money option. This is due to the realities of conversion arbitrage. In a conversion arbitrage, an arbitrageur or market-maker buys stock and buys the put, while selling the call. If he carries the position to expiration, he will have to pay carrying costs on the debit incurred to establish the position. Furthermore, he would earn any dividends that might be paid while he holds the position.

In a perfect world, all option prices would be so accurate that there would be no profit available from a conversion. That is, the following equation (1) would apply:

$$
\begin{aligned}
(1) \quad &\text{Call price}+\text{Strike price}-\text{Stock price}-\text{Put price}+\text{Dividend}-\text{Carrying cost}=0 \\
&\text{Carriying cost}=\text{Strike price}/(1+r)^t \\
&t=\text{time to expiration} \\
&r=\text{interest rate}
\end{aligned}
$$

Now, it is also known that the time value premium of a put is the amount by which its value exceeds intrinsic value. The intrinsic value of an in-the-money put option is merely the difference between the strike price and the stock price. Hence, one can write the following equation (2) for the time value premium (TVP) of an in-the-money put option:

$$
(2) \quad \text{Put TVP}=\text{Put price}-\text{Strike price}+\text{Stock price}
$$

The arbitrage equation, (1), can be rewritten as:

$$
(3) \quad \text{Put price}-\text{Strike price}+\text{Stock price}=\text{Call price}+\text{Dividends}-\text{Carrying cost}
$$

and substituting equation (2) for the terms in equation (3), one arrives at:

$$
(4) \quad \text{Put TVP}=\text{Call price}+\text{Dividends}-\text{Carrying cost}
$$

In other words, the time value premium of an in-the-money put is the same as the (out-of-the-money) call price, plus any dividends to be earned until expiration, less any carrying costs over that same time period.

The time value premium of an in-the-money put disappears rather quickly.

A put won't appreciate in value as much as one might expect, even when the stock drops, since the put loses its time value premium quickly.

A short put is at risk of assignment as soon as there is no time value premium left in the put. Thus, a put can be assigned well in advance of expiration — even a LEAPS put!

An increase in implied volatility also may increase the price of a put, but if the put is too far in-the-money, a modest increase in implied volatility still won't budge the put.

## 37.8 STRADDLE OR STRANGLE BUYING AND SELLING

If a straddle buyer is careful to buy straddles in situations in which implied volatility is "low," he can make money in one of two ways. Either (1) the underlying price makes a move great enough in magnitude to exceed the initial cost of the straddle, or (2) implied volatility increases quickly enough to overcome the deleterious effects of time decay.

## 37.9 CALL BULL SPREADS

Assumption Set 1:

- Stock Price: 100
- Time to Expiration: 4 months
- Position: Long Call Struck at 90
- Short Call Struck at 110

If the stock remains unchanged at 100, and implied volatility increases dramatically, the price of the 90-110 call bull spread will shrink.

In a call bull spread, one would subtract the vega of the call that is sold from that of the call that is bought in order to arrive at the position vega of the call bull spread.

|Implied Volatility|90-110 Call Bull Spread(Theoretical Value)|Position Vega|
|--|--|--|
|20%|10.54|-0.67|
|30%|9.97|-0.48|
|40%|9.54|-0.38|
|50%|9.18|-0.33|
|60%|8.87|-0.30|
|70%|8.58|-0.28|
|80%|8.30|-0.26|

Since these vegas are all negative, they indicate that the spread will shrink in value if implied volatility rises and that the spread will expand in value if implied volatility decreases.

If implied volatility shrinks while the stock rises, the profit outlook will improve.

If the stock drops and the implied volatility drops too, then ones losses would be worse.

If this discussion had looked at bull spreads as put credit spreads instead of call debit spreads, perhaps these conclusions would not have seemed so unusual.

If bull spread strategy used on a volatile stock, you won't get much expansion in the spread even if the stock makes a nice move upward in your favor. In fact, for high implied volatility situations, the bull spread won't expand out to its maximum price until expiration draws nigh.

Often, the bull spread is established because the option trader feels the options are "too expensive" and thus the spread strategy is a way to cut down on the total debit invested.

The bull spread and the call purchase have opposite position vegas, too. That is, a rise in implied volatility will help the call purchase but will harm the bull spread.

If one wants to use the bull spread to effectively reduce the cost of buying an expensive at-the-money option, then at least make sure the striking prices are quite wide apart. That will allow for a reasonable amount of price appreciation in the bull spread if the underlying rises in price. Also, one might want to consider establishing the bull spread with striking prices that are both out-of-the-money. Then, if the stock rallies strongly, a greater percentage gain can be had by the spreader.

### A FAMILIAR SCENARIO?

If you really think a call option is too expensive and want to reduce its cost, try this strategy: Buy the call and simultaneously sell a credit put spread (bull spread) using slightly out-of-the-money puts.

*Example*: With XYZ at 100, a trader is bullish and wants to buy the July 100 calls, which expire in two months. However, upon inspection, he finds that they are trading at 10 — an implied volatility of 59%. He knows that, historically, the implied volatility of this stock’s options range from approximately 40% to 60%, so these are very expensive options. If he buys them now and implied volatility returns to its median range near 50%, he will suffer from the decrease in implied volatility.

As a possible remedy, he considers selling an out-of-the-money put credit spread at the same time that he buys the calls.

Suppose the following prices exist:

- XYZ: 100
- July 100 call: 10 (as stated above)
- July 90 put: 5
- July 80 put: 2

The entire bullish position would now consist of the following:

- Buy 1 July 100 call at 10
- Buy 1 July 80 put at 2
- Sell 1 July 90 put at 5
- Net expenditure: 7 point debit (plus commission)

First, one can see that the bullish spread position has a total risk of 17 points, if XYZ is below 80 (the lower striking price of the put spread) at expiration. That, of course, is more than the 10-point cost of the July 100 call by itself.

Note also that the bullish spread position would have a loss of 10 points (the same as the call) at a price of 87 for the common at expiration. Hence, the combined position actually has less risk than the outright call purchase as long as XYZ is 87 or higher at expiration.

## 37.10 VERTICAL PUT SPREADS

Assume that a stock is selling at 100, and one is going to sell a put with a 110 strike and buy a put with a 90 strike. That is a put credit (bull) spread. Also assume that the options have four months of life remaining.

|Implied Volatility|90-110 Put Bull Spread (Theoretical Value)|
|--|--|
|20%|9.15 credit (Short option trading at parity)|
|30%|9.70 credit|
|40%|10.12 credit|
|50%|10.46 credit|
|60%|10.78 credit|
|70%|11.05 credit|
|80%|11.33 credit|

One would not rationally sell this credit spread if implied volatility were as low as 20%, because at that low level of volatility, the in-the-money December 110 put is trading for 10 dollars — parity — and thus would immediately be at risk of early assignment.

An increase in implied volatility increases the value of the spread. Now, if one had sold this spread to begin with, he would thus be losing money when implied volatility increased.

The lesson to be learned is this: If one is considering using bull spreads in which at least one of the options is at- or in-the-money, then a call bull spread is a superior choice over a put bull spread.

## 37.11 PUT BEAR SPREADS

In a vertical put spread one buys the put with the higher strike and sells the put with the lower strike to construct a simple put bear spread. Actually, a sudden increase in implied volatility is of help to the bear put spread. That is, the spread will widen out slightly.

Once again, it seems that the outright purchase of an option is probably superior to a spread.

## 37.12 CALENDAR SPREADS

An increase in implied volatility will cause a calendar spread to widen out. Both options will become more expensive, of course, since the increase in implied volatility affects both of them, but the absolute price change will be greatest in the long-term option.
