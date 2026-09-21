## Project Summary

This project implements and evaluates a technical trading strategy for
XAU/USD using daily OHLC price data.

The strategy detects bullish buy signals and bearish sell signals using:

- Single-candle pinbars
- Two-candle combined pinbars
- Doji candles with next-day confirmation
- Historical support and resistance lookbacks
- Local swing-low and swing-high validation
- Intervening-price validation

Different lookback sets are used for single pinbars and for double-pinbar
or doji patterns. All comparisons include equality.

The backtest enters at the signal candle's closing price and uses a 1:1
risk-to-reward ratio. For buy signals, the stop is placed at the signal
low. For sell signals, it is placed at the signal high. When the stop and
target are both reached during the same daily candle, the backtest records
the stop first as a conservative assumption.

The included scripts generate:

- Bullish and bearish signals
- Detailed signal information
- Signal type and formation dates
- Prior lookback date and distance
- OHLC charts with color-coded signals
- Individual trade outcomes
- Cumulative and compounded returns
- Buy and sell win rates

The tested dataset covers November 2012 through March 2022. Under the
current configuration, the strategy generated 10 tested signals, with
2 wins and 8 losses. The total result was -6R, equivalent to a compounded
return of approximately -5.87% when 1R represents 1% of account equity.

These historical results do not include spreads, slippage, commissions,
financing costs, or execution latency and should not be interpreted as
financial advice.
