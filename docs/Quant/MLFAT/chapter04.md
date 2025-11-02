# 4. Financial Feature Engineering – How to Research Alpha Factors

## Building on decades of factor research

### Momentum and sentiment – the trend is your friend

Such price momentum defies the hypothesis of efficient markets, which states that past price returns alone cannot predict future performance.

### Why might momentum and sentiment drive excess returns?

Reasons for the momentum effect point to investor behavior, persistent supply and demand imbalances, a positive feedback loop between risk assets and the economy, or the market microstructure.

### How to measure momentum and sentiment

**Relative strength index (RSI)**: A high RSI (usually above 70) indicates overbought and a low RSI (typically below 30) indicates oversold. It first computes the average price change for a given number (often 14) of prior trading days with rising prices $\Delta^\text{up}_\text{p}$ and falling prices $\Delta^\text{down}_\text{p}$.

$$
\text{RSI}=100-\frac{100}{1+\frac{\Delta^\text{up}_\text{p}}{\Delta^\text{down}_\text{p}}}
$$