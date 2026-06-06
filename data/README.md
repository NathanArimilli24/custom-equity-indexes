# Data

This project uses **CRSP** (Center for Research in Security Prices) monthly stock data,
accessed through **WRDS** (Wharton Research Data Services). CRSP data is licensed and
**cannot be redistributed**, so no raw data files are included in this repository.

## How to get the data

1. Obtain a WRDS account with a CRSP subscription (most universities provide access).
2. Set up your WRDS credentials once by running `wrds.Connection()` in Python and following
   the prompt; this creates a `~/.pgpass` file so no passwords are stored in the code.
3. Run [`code/custom_equity_indexes.ipynb`](../code/custom_equity_indexes.ipynb). It pulls
   everything it needs directly from WRDS at run time.

## Tables used

| Table | Purpose |
|-------|---------|
| `crsp.msf` | Monthly stock file: price (`prc`), shares outstanding (`shrout`), return (`ret`) |
| `crsp.msenames` | Name/exchange history, used to filter share codes and exchanges |
| `crsp.msedelist` | Delisting returns (`dlret`), used to mitigate survivorship bias |
| `crsp.stocknames` | Ticker-to-`permno` mapping for the ETF benchmarks (SPY, DIA, QQQ) |

## Universe filters

- U.S. common shares only: `shrcd IN (10, 11)`
- Major exchanges only: `exchcd IN (1, 2, 3)` (NYSE, AMEX, NASDAQ)
- Non-null price and shares outstanding

The default run (2000-2024) pulls roughly 1.2 million security-month records.
