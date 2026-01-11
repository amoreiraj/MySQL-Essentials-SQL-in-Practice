# The NASDAQ dataset contains the following columns:

- `ticker`  
  Stock symbol (e.g., AAPL, MSFT). This will populate `dim_symbol.ticker`.

- `date`  
  Trading date for the price record. This will populate `fact_price_daily.price_date`.

- `open`  
  Opening price on that date. This will populate `fact_price_daily.open_price`.

- `high`  
  Highest price reached during that trading day. This will populate `fact_price_daily.high_price`.

- `low`  
  Lowest price reached during that trading day. This will populate `fact_price_daily.low_price`.

- `close`  
  Closing price on that date. This will populate `fact_price_daily.close_price`.

---

## Core Tables

### `dim_symbol`

dim_symbol is a dimension table that stores one record per traded instrument (stock ticker).

Its purpose is to: 

- Centralize symbol information in a single place

- Avoid repeating ticker strings in large price tables

- Enable efficient joins and future extensibility (exchange, sector, industry, etc.)

Columns

### `symbol_id`

Surrogate primary key used internally by the database. This key is referenced by fact tables instead of repeating the ticker text.

### `ticker`

The stock symbol (e.g., AAPL, MSFT).Enforced as UNIQUE to prevent duplicates.

```sql
CREATE TABLE IF NOT EXISTS dim_symbol (
  symbol_id INT AUTO_INCREMENT PRIMARY KEY,
  ticker VARCHAR(16) NOT NULL UNIQUE
);
```

### `fact_price_daily`

fact_price_daily is a fact table that stores daily price observations for each symbol.

Each row represents:

- One trading day for one stock

- This table is the analytical backbone of the project and is used for:

- Returns calculations

- Volatility analysis

- Moving averages

- Rankings and time-series analytics


### `symbol_id`

Foreign key referencing dim_symbol.Identifies which stock the price data belongs to.

- **price_date**: Trading date of the observation.

- **open_price**: Opening price of the stock on that day.

**high_price**: Highest traded price during the day.

**low_price**: Lowest traded price during the day.

**close_price**: Closing price of the stock.

**volume**: Number of shares traded during the day.

--- 
## Composite Primary key

The composite primary key (symbol_id, price_date) guarantees:

- One record per symbol per day

- No duplicate daily observations

```sql
CREATE TABLE IF NOT EXISTS fact_price_daily (
  symbol_id INT NOT NULL,
  price_date DATE NOT NULL,
  open_price DECIMAL(18,6) NULL,
  high_price DECIMAL(18,6) NULL,
  low_price  DECIMAL(18,6) NULL,
  close_price DECIMAL(18,6) NULL,
  volume BIGINT NULL,
  PRIMARY KEY (symbol_id, price_date),
  CONSTRAINT fk_price_symbol
    FOREIGN KEY (symbol_id) REFERENCES dim_symbol(symbol_id)
);
```
---

## Index: idx_price_date

This index accelerates queries that filter or aggregate by date, which is extremely common in time-series analysis.

Typical use cases:

- Monthly and yearly aggregations

- Rolling window calculations

- Market-wide queries for a specific trading day

```sql 
CREATE INDEX idx_price_date ON fact_price_daily(price_date);
```

----

