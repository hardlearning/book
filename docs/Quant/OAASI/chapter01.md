# CHAPTER 1 Definitions

## 1.1 ELEMENTARY DEFINITIONS

A stock option is the right to buy or sell a particular stock at a certain price for a limited period of time.

A call option gives the owner the right to buy the underlying securitv, while a put option gives the holder the right to sell the underlying security. The price at which the stock may be bought or sold is the exercise price, also called the striking price.

### 1.1.1 DESCRIBING OPTIONS

1. the type (put or call),
2. the underlying stock name,
3. the expiration date,
4. the striking price.

### 1.1.4 THE OPTION ITSELF: OTHER DEFINITIONS

**Classes and Series**: A class of options refers to all put and call contracts on the same underlying security. A series, a subset of a class, consists of all contracts of the same class having the same expiration date and striking price.

**Opening and Closing Transactions**: An opening buy transaction creates or increases a long position in the customer's account. A closing transaction reduces the customer's position. Opening buys are often followed by closing sales; correspondingly, opening sells often precede closing buy trades.

**Open Interest**: The option exchanges keep track of the number of opening and closing transactions in each option series. This is called the open interest. Each opening transaction adds to the open interest and each closing transaction decreases the open interest. Note that the open interest does not differentiate between buyers and sellers. The magnitude of the open interest is useful in determining the liquidity of the option.

**The Holder and Writer**: Anyone who buys an option as the initial transaction (buys opening) is called the holder. On the other hand, the investor who sells an option as the initial transaction (an opening sale) is called the writer of the option.

**Exercise and Assignment**: An option holder who invokes the right to buy or sell is said to exercise the option. Whenever a holder exercises an option, somewhere a writer is assigned the obligation to fulfill the terms of the option contract.

### 1.1.5 RELATIONSHIP OF THE OPTION PRICE AND STOCK PRICE

**In- and Out-of-the-Money**: A call option is out-of-the-money (虚值) if the stock is selling below the striking price. A call option is in-the-money (实值) if the stock price is above the striking price. (Put options work in a converse manner.)

*Example*: XYZ stock is trading at $47 per share. The XYZ July 50 call option is out-of-the-money. However, the XYZ July 45 call is in-the-money.

The intrinsic value of an in-the-money call is the amount by which the stock price exceeds the striking price. If the call is out-of-the-money, its intrinsic value is zero.

The time value premium is the amount by which the option premium itself exceeds its intrinsic value. The time value premium is computed by the following formula for an in-the-money call option:

$$
\text{Call time value premium} = \text{Call option price} - (\underbrace{\text{Stock price} - \text{Striking price}}_\text{intrinsic value})
$$

*Example*: XYZ is trading at 48, and XYZ July 45 call is at 4. The premium of the option is 4. The intrinsic value is 48-45=3, and the time value is 4-3=1.

If the call is out-of-the-money, then the premium and the time value premium are the same.

*Example*: With XYZ at 48 and an XYZ July 50 call selling at 2, both the premium and the time value premium of the call are 2 points.

An option normally lias the largest amount of time value premium when the stock price is equal to the striking price. As an option becomes deeply in- or out-of-the-money, the time value premium shrinks substantially.

**Parity**: An option is said to be trading at parity with the underlying security if it is trading for its intrinsic value. Thus, if XYZ is 48 and the XYZ July 45 call is selling for 3, the call is at parity.

## 1.2 FACTORS INFLUENCING THE PRICE OF AN OPTION

1. price of the underlying stock,
2. striking price of the option itself,
3. time remaining until expiration of the option,
4. volatility of the underlying stock,
5. current risk-free interest rate (such as for 90-day Treasury bills),
6. dividend rate of the underlying stock.

### 1.2.1 THE FOUR MAJOR DETERMINANTS

**Time Value Premium Decay**: An option’s time value premium decays much more rapidly in the last few weeks of its life than it does in the first few weeks of its existence. The rate of decay is actually related to the square root of the time remaining. Thus, a 3-month option decays at twice the rate of a 9-month option, since the square root of 9 is 3.

More volatile underlying stocks have higher option prices.

### 1.2.2 THE TWO MINOR DETERMINANTS

**The Risk-Free Interest Rate**: Higher interest rates imply slightly higher option premiums, while lower rates imply lower premiums.

**The Cash Dividend Rate of the Underlying Stock**: Dividends tend to lower call option premiums: The larger the dividend of the underlying common stock, the lower the price of its call options.

*Example*: XYZ is a relatively low-priced stock with low volatility selling for $25 per share. In six months XYZ will pay $1 per share in dividends, and the stock price will then be $24. Therefore, the call buyer makes a low bid because the underlying stock's price will be reduced by the ex-dividend (除息) reduction, and the call holder does not receive the cash dividends.

## 1.3 EXERCISE AND ASSIGNMENT: THE MECHANICS

### 1.3.5 ANTICIPATING ASSIGNMENT

**Early Exercise Due to Discount**: A writer who does not want to deliver stock should buy back the option prior to expiration if the option is apparently going to trade at a discount to parity. The reason is that arbitrageurs can take advantage of discount (贴水) situations.

*Example*: XYZ is bid at $50 per share, and an XYZ January 40 call option is offered at a discount price of 9.80. The call is actually "worth" 10 points. The arbitrageur can take advantage of this situation through the following actions, all on the same day:

1. Buy the January 40 call at 9.80.
2. Sell short XYZ common stock at 50.
3. Exercise the call to buy XYZ at 40.

The arbitrageur makes 10 points from the short sale of XYZ (steps 2 and 3), from which he deducts the 9.80 points he paid for the call. Thus, his total gain is 20 cents.

If the writer can expect assignment when the option has no time value premium left in it, then conversely the option will usually not be called if time premium is left in it.

**Early Exercise Due to Dividends on the Underlying Stock**: Since the stock price is almost invariably reduced by the amount of the dividend, the option price is also most likely reduced after the ex-dividend. Since the holder of a listed option does not receive the dividend, he may decide to sell the option in the secondary market before the ex-date (除息日) in anticipation of the drop in price.

Do not conclude from this discussion that a call will be exercised for the dividend if the dividend is larger than the remaining time premium.

*Example*: XYZ stock, at 50, is going to pay its regular $1 dividend with the ex-date set for the next day. An XYZ January 40 call is selling at 10.25; it has twenty-five cents of time premium. (TVP = 10.25 + 40 - 50 = 0.25) The arbitrageur's transactions thus consist of:

1. Buy the XYZ January 40 call at 10.25.
2. Exercise the call the same day to buy XYZ at 40.
3. On the ex-date, sell XYZ at 49 and collect the $1 dividend.

He makes 9 points on the stock (steps 2 and 3), and he receives a 1-point dividend, for a total cash inflow of 10 points. However, he loses 10.25 points paying for the call. The overall transaction is a loser and the arbitrageur would thus not attempt it.

Risk arbitrage is arbitrage in which the arbitrageur runs the risk of a loss in order to try for a profit. The arbitrageur may suspect that the stock will not be discounted the full ex-dividend amount or that the call's time premium will increase after the ex-date. In either case, he might make a profit: If the stock opens down only 60 cents or if the option premium expands by 40 cents, the arbitrageur could profit on the opening.
