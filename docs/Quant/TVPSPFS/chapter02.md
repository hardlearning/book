# Chapter-2: Your first program in PineScript

## A Simple PineScript Code

```
//@version=5
indicator("IN.2 Plotting Close", overlay=true)
plot(close)
```

- The “overlay” instructs the system to plot this indicator over the existing chart. If we make “overlay=false”, the new plot will be drawn at the bottom of the candlestick chart.

## What are the Builtin Functions?

```
//@version=5
indicator(title="IN.3 Plotting RSI", overlay=false)
myCustomRSI = ta.rsi(close, 7)
plot(myCustomRSI)
```

- Till version 4, the “ta.rsi” was written as just “rsi”, now due to some reasons and upgradation to version 5, all technical analysis indicators have been moved to “ta” which stands for technical analysis.

## Example of Other Built-in Functions

1. EMA: Exponential moving average

Syntax: ta.ema(source, length) -> series[float]
```
myMA = ta.ema(close,14)
```

2. SMA: Simple Moving Average

Syntax: ta.sma(source, length) -> series[float]
```
myMA = ta.sma(close,14)
```

3. RSI: Relative Strength Index

Syntax: ta.rsi(source, length) -> series[float]
```
myRSI = ta.rsi(close,14)
```

4. ATR: Average True Value

Syntax: ta.atr(source, length) -> series[float]
```
myATR = ta.atr(close,14)
```

5. WMA: Weighted Moving Average

Syntax: ta.wma(source, length) -> series[float]
```
myWMA = ta.wma(close,14)
```

6. MACD: Moving Average Convergence/Divergence

Syntax: ta.macd (source, fast EMA period, Slow EMA period, Signal length)
```
[mLine, sLine, hLine] = ta.macd(close, 12, 26, 9)
```

7. Rising: Check whether rising for given period

Syntax: ta.rising(source, length) -> series[bool]
```
risingResult = ta.rising(close,5)
```

8. SAR: Parabolic Sar to find potential reversal

Syntax : ta.sar(start, increment, max) -> series[float]
```
sarResult = ta.sar(0.2,0.2,0.2)
```

## What are Builtin Variables?

All the built-in variables (like open, high, low, close, and volume) are “series variables” i.e. they store data in the form of a list. The latest data is written at the end of the list. For example, the current bar close can be accessed by close, whereas if you want to access close data for 4 bar back you can use close[4].
