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
