# Market Microstructure Project - Cryptocurrency Liquidity Analysis

## Important Notice

The multi-cryptocurrency, millisecond-level trade and quote dataset used throughout this study was purchased by the supervising professor and remains his personal or institutional property. Redistribution is not permitted and the raw files are not bundled with this repository. Users who are interested in reproducing the entire analysis will prepare the equivalent datasets on their own.

To reproduce the full workflow, assemble datasets with the specifications below (file naming can be adapted in the notebooks):

| Dataset                      | Instruments                           | Frequency & Granularity                                                       | Required Fields                                                                                                           | Expected Folder               |
| ---------------------------- | ------------------------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| Trades                       | BTC-USD, DOGE-USD, SHIB-USD, USDT-USD | Millisecond timestamps (stored as microseconds) in compressed daily CSV files | `timestamp`, `price`, `amount` (or `size`), optional `side`                                                     | `data/raw/<symbol>/trades/` |
| Quotes / Order Book          | Same as above                         | Millisecond snapshots; level-1 mandatory, deeper levels optional              | `timestamp`, `bid_price`, `ask_price`, `bid_size`, `ask_size`, optional depth ladders (`price_n`, `size_n`) | `data/raw/<symbol>/quotes/` |
| Event Calendar               | All covered assets                    | Daily (announcement date) with optional time stamps                           | `event_date`, `event_time` (if available), `event_type`, `description`, optional `event_id`                     | `data/events/`              |
| Exchange Metadata (optional) | Any                                   | As provided by the vendor                                                     | Venue identifiers, data-source labels, mapping tables for symbol names                                                    | `data/raw/metadata/`        |

The pipeline expects raw feeds to be organized by instrument and date. Conversion notebooks assume daily compressed CSV files; adjust loaders if your provider uses alternative formats. Minute-level and hourly aggregates are generated within the repository and saved under `results/`.

## Project Overview

This repository contains the research process of examining how major events impact cryptocurrency liquidity using high-frequency trading data. The central question is simple: when a regulatory announcement or economic shock hits, how does the market’s liquidity react, how quickly does it recover, and how much the stress spills over different coins?

The study covers four cryptocurrencies—Bitcoin, Dogecoin, Shiba Inu, and Tether—across 76 major events between 2020 and 2024.

---

## Our Approach

### 1. Data Processing Pipeline

- **Input**: High-frequency trade and quote data (millisecond-level)
- **Output**: Aggregated minute-level and hourly liquidity metrics
- **Metrics Computed**:

  - Bid-Ask Spread
  - Effective Spread
  - Market Depth (±1% around mid-price)
  - Trading Volume
  - Number of Trades
  - Average Trade Price
- **Challenge**: Massive millisecond-level trade and quote data
- **Solution**: Aggregate through a modular pipeline
- **Metrics**: Effective spread, quoted bid-ask spread, market depth (±1% around mid-price), trading volume, trade count, average trade price
- **Engineering choices**: Month-by-month processing for memory control, `ProcessPoolExecutor` for parallelism, merge trades and quotes with `pd.merge_asof` (2-second tolerance) before resampling

### 2. Event Hour Detection

- Markets react at specific moments rather than at announcement timestamps
- Scan ±18 hours around each event to find the hour with the maximum price high-low range
- Tested multiple detection windows (±1, ±2, ±4, ±6, ±12, ±18, ±24 hours) and selected ±18 hours for the best balance of accuracy and robustness

### 3. Panel Data Construction

- Align events on a common timeline for comparative analysis
- **Baseline**: 30 days of pre-event data to capture normal conditions
- **Event window**: ±24 hours at the minute level for high-resolution shock dynamics
- **Post-event observation**: 10 days to measure recovery
- Output panels hold time along rows and events across columns for each liquidity metric

### 4. Peak & Recovery Analysis

- **Standardized intensity**
  ```
  Intensity = (Peak Spread - Baseline Mean) / Baseline Std
  ```
- **Recovery time**: 20-minute moving average, market considered recovered after 20 consecutive minutes below 1.5 × baseline mean
- **Findings**: Average intensity 6.45 standard deviations; average recovery 113 minutes; strong positive correlation between shock size and recovery duration (Pearson 0.51, Spearman 0.70)

### 5. Statistical Robustness

- Intensity distribution is right-skewed (skewness 2.81)
- Applied Box-Cox transformation to approach normality (skewness ≈ 0.01)
- Used Median Absolute Deviation for outlier detection and built bootstrap confidence intervals
- Compared crypto-specific versus macro events—no significant difference in shock intensity or recovery time

---

## Research & Technical Challenges

### Pinpointing the Actual Event Clock

- **Problem**: Announcement timestamps did not match the true moment of market reaction. Exchanges incorporate information at different speeds and some official release times were only approximate.
- **What we tried**: Compared fixed-hour windows (±1, ±2, ±4, ±6, ±12, ±18, ±24 hours) and evaluated how often each window surfaced a unique volatility spike. Added guardrails so the detected hour must exceed baseline volatility by 3 standard deviations.
- **Outcome**: ±18 hours delivered the best recall without surfacing unrelated volatility. We also log secondary peaks (within ±2 hours of the primary) to flag potential multi-stage reactions.

### Synchronizing Trades and Quotes at Millisecond Resolution

- **Problem**: Quoted books and trades arrive on separate feeds with microsecond offsets, gaps, and occasional clock drift. Naively merging them creates negative spreads or lost depth.
- **What we did**: Cleaned extreme quotes (spreads < 0 or > 5%), forward-filled level-1 quotes for gaps up to 2 seconds, and used `pd.merge_asof` with a 2-second tolerance plus direction="backward" to ensure the trade uses the latest valid quote. When no quote matched, the trade was excluded from liquidity metrics but logged for diagnostics (≈3.1% of trades per month).

### Reconstructing Order-Book Depth from Partial Snapshots

- **Problem**: Some days provided only top-of-book data while others included 10-level depth. We needed consistent ±1% market depth metrics.
- **Solution**: Standardized by integrating size within the price band. When only level-1 was available, we constrained the depth calculation to reported sizes and tagged the day with a coverage flag so downstream analysis could test robustness with and without limited-depth sessions.

### Maintaining Cross-Month Continuity

- **Issue**: Event windows that straddle month boundaries lacked the necessary baseline minutes because source files were stored month-by-month.
- **Fix**: The pipeline automatically detects boundary events, loads the preceding month, and splices in the missing minutes before resampling. Without this automation, roughly 10% of panels needed manual patching and baseline averages were biased downward.

---

## Impact & Results Summary

- Liquidity shocks average 6.45 standard deviations above baseline
- Median recovery time is roughly 60 minutes (mean 113 minutes)
- Bigger shocks take meaningfully longer to recover—a key insight for risk management and trading strategies
- The pipeline scales to billions of records and generalizes to other event studies

---

## Repository Structure

```
notebooks/
  01_event_filter/
  02_data_conversion/
  03_event_hour_detection/
  04_panel_generation/
  05_analysis/
data/
  raw/
  processed/
  events/
results/
  panels/
  figures/
  statistics/
```

Raw high-frequency data is proprietary and excluded from version control. Generated panels, figures, and stats are stored under `results/` and ignored by git.

---

## Getting Started

1. Install dependencies: `pip install -r requirements.txt`
2. Obtain the proprietary trade, quote, and event datasets and place them under `data/raw` and `data/events`
3. Execute notebooks in the order shown above, adapting paths as needed for local or Colab environments

---

## Credits

- Author: Yixuan Guo
- Academic project for the Financial Management course
- Data provided by the course professor
