# Notebooks Directory

This directory contains the core analysis notebooks organized by workflow stage.

## Directory Structure

### 01_event_filter/
Event identification and filtering. Data files should be placed here:
- Event dates and classifications
- Market impact criteria

### 02_data_conversion/
Convert high-frequency (millisecond) data to minute and hourly aggregations.

**Notebooks:**
- `data_convertor_BTC.ipynb` - Bitcoin data conversion
- `data_convertor_DOGE.ipynb` - Dogecoin data conversion
- `data_convertor_SHIB.ipynb` - Shiba Inu data conversion
- `data_convertor_USDT.ipynb` - Tether data conversion

**Key Features:**
- Parallel processing for efficiency
- Month-by-month batch processing
- Computes 6 liquidity metrics: spread, effective spread, depth, volume, trade price, number of trades

**Expected Runtime:** Several hours for BTC on free Colab resources

### 03_event_hour_detection/
Detect precise event impact timing within the event day.

**Notebooks:**
- `detect_event_hour.ipynb` - Event hour detection using ±18-hour window

**Method:**
- Analyzes hourly high-low price differences
- Selects hour with maximum volatility as event hour
- Parameterized detection windows for robustness testing

### 04_panel_generation/
Generate event study panel datasets.

**Notebooks:**
- `minute_panel_generator.ipynb` - Creates minute-level panels (±24 hours)
- `hourly_panel_generator.ipynb` - Creates hourly panels with baseline and post-event data

**Panel Structure:**
- Rows: Time relative to event (negative = before, 0 = event hour, positive = after)
- Columns: Each event as a separate column
- Fills missing data for cross-month events

### 05_analysis/
Statistical analysis and visualization.

**Notebooks:**
- `panel_EDA_visualization.ipynb` - Exploratory data analysis with charts
- `peak_recovery_analysis.ipynb` - Measures impact intensity and recovery time
- `regression_analysis.ipynb` - Econometric analysis with robustness tests

**Analyses:**
- Time series visualization of liquidity metrics
- Peak detection and recovery time calculation
- Panel regression with fixed effects
- Spillover analysis across cryptocurrencies

## Workflow

1. **Prepare Event Data** → Place event filter files in `01_event_filter/`
2. **Convert Raw Data** → Run notebooks in `02_data_conversion/` for each coin
3. **Detect Event Hours** → Run `03_event_hour_detection/detect_event_hour.ipynb`
4. **Generate Panels** → Run notebooks in `04_panel_generation/`
5. **Analyze Results** → Run analysis notebooks in `05_analysis/`

## Data Paths

All notebooks use Google Drive paths by default (for Colab). Update these paths if running locally:
```python
# Example path structure
data_folder = "/path/to/your/data"
event_file = "/path/to/your/event_filter.csv"
```

## Notes

- Most notebooks are designed for Google Colab
- Some processes are computationally intensive (especially BTC conversion)
- Ensure sufficient disk space for intermediate results
- All output files are CSV format for compatibility

