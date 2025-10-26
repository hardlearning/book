# CHAPTER 24 Ratio Spreads Using Puts

The put option spreader may want to sell more puts than he owns. This creates a ratio spread (比率价差).

## 24.1 THE RATIO PUT SPREAD

In a ratio put spread (看跌期权比率价差), one buys a number of puts at a higher strike and sells more puts at a lower strike. This position involves naked puts, since one is short more puts than he is long.

Example: Given the following:
- XYZ common, 50;
- XYZ January 45 put, 2; and
- XYZ January 50 put, 4.

A ratio put spread might be established by buying one january 50 put and simultaneously selling two January 45 puts.

Since one would be paying 400 for the purchased put and would be collecting 400 from the sale of the two out-of-the-money puts, the spread could be done for even money.

TABLE 24-1. Ratio put spread.

|XYZ Price at Expiration|Long January 50 Put Profit|Short 2 January 45 Put Profit|Total Profit|
|--|--|--|--|
|20|+$2,600|-$4,600|-$2,000|
|30|+1,600|-2,600|-1,000|
|40|+600|-600|0|
|42|+400|-200|+200|
|45|+100|+400|+500|
|48|-200|+400|+200|
|50|-400|+400|0|
|60|-400|+400|0|

![FIGURE 24-1](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-24-1.png?raw=true)

The following formulae summarize the situation for any put ratio spread:

- Maximum upside risk = Net debit of spread (no upside risk if done for a credit)
- Maximum profit potential = Striking price differential $\times$ Number of long puts - Net debit (or plus net credit)
- Downside break-even price = Lower strike price - Maximum profit potential $\div$ Number of naked puts

There is a variation of the put ratio spread that can sometimes be even more attractive, for it pushes the downside break-even point even lower.

Example: Using three strikes in the put ratio spread. Suppose the following prices exist:

- XYZ: 127
- XYZ December 125 put: 3.00
- XYZ December 121 put: 2.00
- XYZ December 116 put: 1.25

A put ratio spread can be established as follows:

- Buy 1 Dec 125 put, and
- Sell 1 Dec 121 put, and
- Sell 1 Dec 116 put
- For a net overall credit of 0.25.

![FIGURE 24-2](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-24-2.png?raw=true)

There is a rather wide profit range for this spread, and the maximum profit is attainable over a good portion of that range.

- Downside break-even = Lower Strike - (Difference in two Higher Strikes) - Net credit = 116-(125-121)-0.25 = 111.75

The maximum profit potential of the spread is attainable at any point between the two lower strikes — anywhere between 116 and 121 in this example.

- Maximum Profit Potential = (Differenee in two Higher Strikes) + Net eredit = (125-121)+0.25 = 4.25

## 24.3 THE RATIO PUT CALENDAR SPREAD

The ratio put calendar spread (看跌期权比率跨期价差) consists of buying a longer-term put and selling a larger quantity of shorter-term puts, all with the same striking price. The position is generally established with out-of-the-money put.

Example: If XYZ were at 55, and the January 50 put was at 1.50 with the April 50 at 2, one could establish a ratio put calendar spread by buying the April 50 and selling two January 50 puts.

This is a credit position, because the sale of the two January 50 puts would bring in 300 while the cost of the April 50 put is only 200. The overall credit is 100.
