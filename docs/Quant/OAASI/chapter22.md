# CHAPTER 22 Basic Put Spreads

## 22.1 BEAR SPREAD

A put hear spread is established by selling a put at a lower strike while buying a put at a higher strike.

The put bear spread is a debit spread. This is true because a put with a higher striking price will sell for more than a put with a lower striking price.

*Example*: The following prices exist:

- XYZ common, 55;
- XYZ January 50 put, 2; and
- XYZ January 60 put, 7.

Buying the January 60 put and selling the January 50 would establish a bear spread for a 5-point debit.

TABLE 22-1. Put bear spread.

|XYZ Price at Expiration|January 50 Put Profit|January 60 Put Profit|Total Profit|
|--|--|--|--|
|40|-$800|+$1,300|+$500|
|45|-300|+800|+500|
|50|+200|+300|+500|
|55|+200|-200|0|
|60|+200|-700|-500|
|70|+200|-700|-500|
|80|+200|-700|-500|

![FIGURE 22-1](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-22-1.png?raw=true)

The following formulae allow one to quickly compute the meaningful statistics regarding a put bear spread:

- Maximum risk = Initial debit
- Maximum profit = Difference between strikes - Initial debit
- Break-even price = Higher striking price - Initial debit

## 22.2 BULL SPREAD

A bull spread can be established with put options by buying a put at a lower striking price and simultaneously selling a put with a higher striking price.

Example: The same prices can be used:

- XYZ common, 55;
- XYZ January 50 put, 2; and
- XYZ January 60 put, 7.

The bull spread is constructed by buying the January 50 put and selling the January 60 put. This is a credit spread. The credit is 5 points in this example.

If the underlying stock advances by January expiration and is anywhere above 60 at that time, both puts would expire worthless and the spreader would make a profit of the entire credit — 5 points in this example.

If XYZ were anywhere below 50 at expiration, the differential between the two puts would widen to 10 points. Thus, the spreader would have to pay 10 points to buy the spread back, or to close out the position. Since he initially took in a 5-point credit, this means his loss is equal to 5 points = 10-5.

The following formulae allow one to quickly compute the details of a bullish put spread:

- Maximum potential risk = Initial collateral requirement = Difference in striking prices - Net credit received
- Maximum potential profit = Net credit
- Break-even price = Higher striking price - Net credit

## 22.3 CALENDAR SPREAD

In a calendar spread, a near-term option is sold and a longer-term option is bought, both with the same striking price. This definition applies to either a put or a call calendar spread.

*Example*: XYZ is at 50 and a January 50 put is selling for 2 points while an April 50 put is selling for 3 points. A neutral calendar spread can be established for a 1-point debit by selling the January 50 put and buying the April 50 put.

Neutral call calendar spreads are generally superior to neutral put calendar spreads. Since the amount of time value premium is usually greater in a call option (unless the underlying stock pays a large dividend), the spreader who is interested in selling time value would be better off utilizing call options.

With put options, a bearish strategy can be constructed using a calendar spread. In this case, one would establish the spread with out-of-the-money puts.

*Example*: With XYZ at 55, one would sell the January 50 put for 1 point and buy the April 50 put for 1.50.
