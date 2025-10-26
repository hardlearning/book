# CHAPTER 18 Buying Puts in Conjunction with Call Purchases

Example: An investor initially purchased an XYZ October 50 call for 3 points when the stock was at 48. After the stock had risen to 58, the call would be worth about 9 points. If there was an October 60 put, it might be selling for 4 points, and the call holder could buy this put to lock in some of his profits. His position, after purchasing the put, would be:

- Long 1 October 50 call at 3 points
- Long 1 October 60 put at 4 points
- Net cost: 7 points

He would own a "strangle" — any position consisting of both a put and a call with differing terms — that is always worth at least 10 points. Because he paid only 7 points for the combination. No matter what happens, a 3-point profit is locked in.

## 18.1 STRADDLE BUYING

A straddle purchase consists of buying both a put and a call with the same terms — same underlying stock, striking price, and expiration date.

Example: The following prices exist:

- XYZ common, 50;
- XYZ July 50 call, 3; and
- XYZ July 50 put, 2.

If one purchased both the July 50 call and the July 50 put, he would be buying a straddle. This would cost 5 points plus commissions.

TABLE 18-1. Results of straddle purchase at expiration.

|XYZ Price at Expiration|Call Profit|Put Profit|Total Straddle Profit|
|--|--|--|--|
|30|-$300|+$1,800|+$1,500
|40|-300|+800|+500|
|45|-300|+300|0|
|50|-300|-200|-500|
|55|+200|-200|0|
|60|+700|-200|+500|
|70|+1,700|-200|+1,500|

![FIGURE 18-1](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-18-1.png?raw=true)

### 18.1.1 QUIVALENCES

Straddle buying is equivalent to the reverse hedge, a strategy described in Chapter 4 in which one sells the underlying stock short and purchases two calls on the underlying stock.

## 18.4 BUYING A STRANGLE

A strangle is a position that consists of both a put and a call, which generally have the same expiration date, but different striking prices.

Example: One might buy a strangle consisting of an XYZ January 45 put and an XYZ January 50 call.

- XYZ common, 47;
- XYZ January 45 put, 2; and
- XYZ January 50 call, 2.

In this example, both options are out-of-the-money when purchased. This is the most normal application of the strangle purchase.

The investment — $400 in the example — is generally smaller than that required to buy a straddle on XYZ.

TABLE 18-2. Results at expiration of a strangle purchase.

|XYZ Price at Expiration|Put Profit|Call Profit|Total Profit|
|--|--|--|--|
|25|+$1,800|-$200|+$1,600|
|35|+800|-200|+600|
|41|+200|-200|0|
|43|0|-200|-200|
|45|-200|-200|-400|
|47|-200|-200|-400|
|50|-200|-200|-400|
|54|-200|+200|0|
|60|-200|+800|+600|
|70|-200|+1,800|+1,600|

![FIGURE 18-2](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-18-2.png?raw=true)

The example above is one in which both options are out-of-the-money. It is also possible to construct a very similar position by utilizing in-the-money options.

Example: With XYZ at 47 as before, the in-the-money options might have the following prices:

- XYZ January 45 call, 4; and 
- XYZ January 50 put, 4. 

If one purchased this in-the-money strangle, he would pay a total cost of 8 points. However, the value of this strangle will always be at least 5 points, since the striking price of the put is 5 points higher than that of the call.

Because the strangle will always be worth at least 5 points, the most that the in-the-money strangle buyer can lose is 3 points in this example.

Thus, even though it requires a larger initial investment, the in-the-money strange may often be a superior strategy to the out-of-the-money strangle, from a buyer's viewpoint.
