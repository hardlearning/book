# CHAPTER 10 The Butterfly Spread

The butterfly spread is a neutral position that is a combination of both a bull spread and a bear spread.

There are three striking prices involved in a butterfly spread. Using only calls, the butterfly spread consists of buying one call at the lowest striking price, selling two call at middle striking price and buying one call at the highest striking price.

*Example*: A butterfly spread is established by buying a July 50 call for 12, selling 2 July 60 calls for 6 each, and buying a July 70 call for 3.

- XYZ common: 60
- XYZ July 50 call: 12
- XYZ July 60 call: 6
- XYZ July 70 call: 3

Butterfly spread:

- Buy 1 July 50 call: $1,200 debit
- Sell 2 July 60 calls: $1,200 credit
- Buy 1 July 70 call: $300 debit
- Net debit: $300 (plus commissions)

The risk is limited in a butterfly spread, both to the upside and to the downside, and is equal to the amount of the net debit required to establish the spread. In the example above, the risk is limited to $300 plus commissions.

Table 10-2 and Figure 10-1 depict the results of this butterfly spread at various prices at expiration.

TABLE 10-2. Results of butterfly spread at expiration.

|XYZ Price at Expiration|July 50 Profit|July 60 Profit|July 70 Profit|Total Profit|
|--|--|--|--|--|
|40|-$1,200|+$1,200|-$300|-$300|
|50|-1,200|+1,200|-300|-300|
|53|-900|+1,200|-300|0|
|56|-600|+1,200|-300|+300|
|60|-200|+1,200|-300|+700|
|64|+200|+400|-300|+300|
|67|+500|-200|-300|0|
|70|+800|-800|-300|-300|
|80|+1,800|-2,800|+700|-300|

![FIGURE 10-1](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-10-1.png?raw=true)

When the options expire in the same month and the striking prices are evenly spaced (the spacing is 10 points in this example), the following formulae can be used to quickly compute the important details of the butterfly spread:

- Net investment = Net debit of the spread
- Maximum profit = Distance between strikes - Net debit
- Downside break-even = Lowest strike + Net debit
- Upside break-even = Highest strike - Net debit

In the example, the distance between strikes is 10 points, the net debit is 3 points, the lowest strike used is 50, and the highest strike is 70. These formulae would then yield the following results for this example spread.

- Net investment = 3 points = $300
- Maximum profit = 10 - 3 = $700
- Downside break-even = 50 + 3 = 53
- Upside break-even = 70 - 3 = 67