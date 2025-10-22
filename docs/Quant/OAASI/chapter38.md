# CHAPTER 38 The Distribution of Stock Prices

## 38.1 MISCONCEPTIONS ABOUT VOLATILITY

The lognormal distribution is what's commonly used to describe stock prices because its shape is intuitively similar to the way stocks behave — they can't go below zero, they can rise to infinity, and most of the time they don't go much of anywhere.

## 38.3 THE DISTRIBUTION OF STOCK PRICES

### 38.3.1 THE "BIG" PICTURE

There is a much greater chance of a large standard deviation move than the lognormal distribution would indicate. The high probabilities on the ends of the distribution are called "fat tails" by most mathematicians and stock market practitioners alike.

## 38.6 THE PRICING OF OPTIONS

Most options are underpriced, since traders and market-makers are using the Black-Seholes model to price them.

## 38.7 THE PROBABILITY OF STOCK PRICE MOVEMENT

*Example*: Suppose that a trader is considering buying a straddle on XYZ. The five-month straddle is selling for a price of 8, with the stock currently trading near 40. A probability calculator will help him to determine the chances that XYZ can rise to 48 or fall to 32 (the break-even points) prior to the options' expiration. However, the probability calculator's answer will depend heavily on the volatility estimate that the trader plugs into the probability calculator. Suppose that the following information is known about the historical volatility of XYZ:

- 10-day historical volatility: 22%
- 20-day historical volatility: 20%
- 50-day historical volatility: 28%
- 100-day historical volatility: 33%

Since one is buving options in this strategy he should use the lowest of the above historical volatility measures as his volatility estimate. So, in this example, he should use the 20-day historical volatility because it is the lowest of the four choices that he has.

Similarly, if one is considering the sale of options or is taking a position with a negative vega, then he should use the highest historical volatility when making his probability projections.

When a longer lookback period is required, there is another method that can be used: Go back in a historical database of prices for the underlying and compute the 20-day, 50-day, and 100-day historical volatilities for all the time periods in the database, or at least during a fairly large segment of the past prices. Then use the median of those calculations for your volatility estimates.

*Example*: A trader decides to look back over the last 1,000 trading days for XYZ. A 100-day historical volatility can be computed, using 100 consecutive trading days of data, for 901 of those days (beginning with the 100th day and continuing through the 1,000th day, which is presumably the current trading day). Admittedly, these are not completely unique time periods; there would only be ten non-overlapping (independent) consecutive 100-day periods in 1,000 days of data. However, let's assume that the 901 periods are used. One can then arrive at a distribution of 100-day historical volatilities. Suppose it looks something like this:

|Percentile|100-Day Historical|
|--|--|
|0th|34%|
|10th|37%|
|20th|43%|
|30th|45%|
|40th|46%|
|50th|48%|
|60th|51%|
|70th|58%|
|80th|67%|
|90th|75%|
|100th|81%|

In other words, the 901 historical volatilities (100 days in each) are sorted and then the percentiles are determined. The above table is just a snapshot of where the percentiles lie. The median of the above figures is 48% — the 100-day volatility at the 50th percentile.

One could perform similar analyses on the 1,000 days of historical data to determine where the 10-day, 20-day, and 50-day historical volatilities were over that time. Those could be sorted and arranged in percentile format, using the 50th percentile (median) as a good estimate of volatility. 

Using 1,000 days of data:
- Median 100-day historical volatility: 48%
- Median 50-day historical volatility: 49%
- Median 20-day historical volatility: 52%
- Median 10-day historical volatility: 49%

If these were all the data that one had, then he would probably use a volatility estimate of 48% in his option models or probability calculators.

### 38.7.1 THE ENDPOINT CALCULATION

Probability of stock being below price q at end of time period, t

$$
P(\text{below})=N\left(\frac{\ln(\frac{q}{p})}{v_t}\right)
$$

- N = cumulative normal distribution
- p = current price of the stock
- q = price in question
- ln = natural logarithm for the time period in question

If one is interested in computing the probability of the stock being above the given price, the formula is

$$
P(\text{above})=1-P(\text{below})
$$

In the above formula, $v_t=v\sqrt{t}$ where $t$ is time to expiration in years and $v$ is annual volatility.

*Example*: Suppose a trader is a seller of naked put options. He sells OEX October 550 puts naked, with OEX currently trading at 600. There are essentially three scenarios that can occur:

1. OEX might never fall to 550 by expiration. In this case, he would have a very comfortable trade that was never in jeopardy, and the options would expire worthless.
2. OEX might fall below 550 and remain there until expiration. In this case, he would surely have a loss unless OEX were just a tiny bit below 550.
3. OEX might fall below 550 at some time between when the trade was established and when expiration occurred, but then subsequently rally back above 550 by the time expiration arrived.

The simple probability calculator formula shown above does not take into account the trader's third scenario. Since it is only concerned with where the stock is at expiration of the options, only scenarios 1 and 2 apply to it.

Suppose that the volatility estimate is 25%, there are 30 days until expiration, and the prices are as stated in the previous example: OEX is at 600, and the striking price of the naked put being sold is 550. The resulting probabilities might be something like this:

|Scenario|Actual Probability of Occurrence|
|--|--|
|1. OEX never falls below 550|67%|
|2. OEX falls below 550 and remains there|19%|
|3. OEX falls below 550 but rallies later|14%|

The probabilities stated above are the "real" probabilities of the three various scenarios occurring. However, if one were using the simple probability calculator presented above, he would only have the following information:

- Probability of OEX being above 550 at expiration: 81%
- Probability of OEX being below 550 at expiration: 19%

The difference — the other 14% — is the probability of the third scenario occurring. The simple probability calculator doesn't account for that scenario at all.
