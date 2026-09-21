# Brief Strategy Report

## Dataset

The current implementation uses daily XAU/USD OHLC data. The latest fresh run
used data from:

```text
2012-11-14 to 2022-03-04
```

## Strategy Summary

The strategy searches for support/resistance style reversal structures:

- normal buy pinbars near prior lows
- reverse sell pinbars near prior highs
- two-candle pinbar combinations
- doji candles confirmed by the following candle

The scanner applies historical validation through lookback candles. For normal
signals, the lookback reference is the prior candle low. For reverse signals,
the lookback reference is the prior candle high.

## Latest Backtest Snapshot

The latest fresh all-signal run produced:

```text
Normal buy signals: 6
Reverse sell signals: 4
Total signals: 10
Wins: 2
Losses: 8
Win rate: 20.00%
Total R: -6.00R
Cumulative return at 1R = 1%: -6.00%
Compounded return: -5.87%
Max drawdown: -6.00R
```

## Latest Signal List

```text
2015-07-02 | normal/buy   | single pinbar | single           | LB 19 | prior 2015-06-05 | loss | -1R
2016-03-24 | normal/buy   | double pinbar | current+next     | LB 19 | prior 2016-02-26 | loss | -1R
2016-03-28 | normal/buy   | double pinbar | previous+current | LB 20 | prior 2016-02-26 | win  |  1R
2016-06-15 | reverse/sell | double pinbar | current+next     | LB 32 | prior 2016-05-02 | loss | -1R
2016-06-16 | reverse/sell | double pinbar | previous+current | LB 33 | prior 2016-05-02 | loss | -1R
2018-02-28 | normal/buy   | double pinbar | current+next     | LB 39 | prior 2018-01-04 | loss | -1R
2021-01-11 | normal/buy   | single pinbar | single           | LB 18 | prior 2020-12-14 | loss | -1R
2021-06-14 | normal/buy   | single pinbar | single           | LB 18 | prior 2021-05-19 | loss | -1R
2021-12-27 | reverse/sell | double pinbar | current+next     | LB 20 | prior 2021-11-26 | loss | -1R
2021-12-28 | reverse/sell | double pinbar | previous+current | LB 21 | prior 2021-11-26 | win  |  1R
```

## Observations

The current rule set is restrictive and produces a small number of trades over
the available historical sample. In the latest run, performance was negative:
the strategy won 2 of 10 trades and ended at -6R.

The next useful research step is to test whether entry timing, stop placement,
or the confirmation candle rules improve the distribution without loosening the
signal definition too much.
