# XAU/USD Pinbar and Doji Strategy

This project implements and backtests a daily XAU/USD strategy based on pinbar,
double-pinbar, and confirmed-doji reversal patterns.

## What It Does

- Loads XAU/USD daily OHLC data.
- Detects normal buy signals.
- Detects reverse sell signals.
- Supports single-candle pinbars, two-candle pinbars, and confirmed doji setups.
- Applies separate lookback sets for single pinbars versus double pinbars/dojis.
- Runs a 1:1 risk/reward backtest.
- Exports signal CSVs, trade details, summaries, and an OHLC chart with signal markers.

## Current Strategy Rules

### Normal Buy Pinbar

Open and close must both be greater than or equal to:

```text
Low + (High - Low) * 0.618
```

### Reverse Sell Pinbar

Open and close must both be less than or equal to:

```text
Low + (High - Low) * 0.382
```

### Doji

The candle body must satisfy:

```text
abs(Close - Open) <= (High - Low) * 0.382
```

Normal doji confirmation requires the next candle to be bullish and close in the
upper part of its range. Reverse doji confirmation requires the next candle to be
bearish and close in the lower part of its range.

## Lookbacks

Single pinbar lookbacks:

```text
18, 19, 20, 32, 33, 37, 38, 56, 57, 75, 76
```

Double pinbar and doji lookbacks:

```text
18, 19, 20, 21, 32, 33, 34, 37, 38, 39, 56, 57, 58, 75, 76, 77
```

## Main Files

- `work/all_signals_updated.py` - merged signal scanner for both normal and reverse strategies.
- `work/backtest_all_signals_updated.py` - backtest runner using the merged scanner.
- `work/run_fresh_all_signals_backtest_chart.py` - fresh full run that rebuilds data, signals, backtest, and chart.

## Typical Commands

Run the merged signal scanner:

```bash
python3 work/all_signals_updated.py
```

Run the backtest:

```bash
python3 work/backtest_all_signals_updated.py
```

Run the fresh report/chart generator:

```bash
python3 work/run_fresh_all_signals_backtest_chart.py
```

## Outputs

The scripts write outputs under `outputs/`, including:

- all-signal CSV files
- backtest trade CSV files
- signal detail CSV files
- summary text files
- SVG/PNG charts

## Backtest Assumptions

- Normal signals are buy trades.
- Reverse signals are sell trades.
- Entry is the signal candle close.
- Buy stop is the signal low.
- Sell stop is the signal high.
- Target is 1R from entry.
- If stop and target both touch inside the same daily candle, stop is counted first.
- Each signal is tested independently, so overlapping trades are allowed.
