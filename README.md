# Cryptocurrency Liquidity Analysis

A comprehensive research project analyzing the impact of major events on cryptocurrency market liquidity using high-frequency trading data.

## 🎯 Project Overview

This project examines how significant events (economic, regulatory, and technical) affect cryptocurrency market liquidity across multiple coins (BTC, DOGE, SHIB, USDT). The analysis pipeline processes high-frequency data from millisecond-level to minute and hourly aggregations, identifies event impact points, and performs quantitative analysis on liquidity recovery patterns.

### Key Research Questions
- How do different types of events impact cryptocurrency liquidity?
- What is the intensity and duration of liquidity shocks?
- How quickly does market liquidity recover after major events?
- Are there spillover effects across different cryptocurrencies?

## 📊 Methodology

### 1. Event Identification & Filtering
- Identify major events affecting cryptocurrency markets (economic, regulatory, technical)
- Filter events based on their significance and data availability

### 2. Data Processing Pipeline
- **Input**: High-frequency trade and quote data (millisecond-level)
- **Output**: Aggregated minute-level and hourly liquidity metrics
- **Metrics Computed**:
  - Bid-Ask Spread
  - Effective Spread
  - Market Depth (±1% around mid-price)
  - Trading Volume
  - Number of Trades
  - Average Trade Price

### 3. Event Hour Detection
- Identifies the precise hour when an event impacts the market
- Uses price volatility (high-low difference) as the detection criterion
- Searches within an ±18-hour window around the event date

### 4. Panel Data Generation
- Creates event study panels with data before and after each event
- **Minute-level panels**: ±24 hours (1,440 minutes) around event hour
- **Hourly panels**: ±30 days baseline + 10 days post-event observation

### 5. Statistical Analysis
- **Exploratory Data Analysis**: Visualization of liquidity patterns
- **Peak & Recovery Analysis**: Measures intensity and recovery time
- **Regression Analysis**: Quantifies event impacts with robustness tests
- **Spillover Analysis**: Examines cross-cryptocurrency effects

## 📁 Project Structure

```
Crypto_Liquidity/
├── README.md                          # Project documentation
├── requirements.txt                   # Python dependencies
├── .gitignore                         # Git ignore patterns
│
├── notebooks/                         # Analysis notebooks
│   ├── 01_event_filter/              # Event identification (data files only)
│   ├── 02_data_conversion/           # Millisecond to minute/hour conversion
│   │   ├── data_convertor_BTC.ipynb
│   │   ├── data_convertor_DOGE.ipynb
│   │   ├── data_convertor_SHIB.ipynb
│   │   └── data_convertor_USDT.ipynb
│   ├── 03_event_hour_detection/      # Precise event timing
│   │   └── detect_event_hour.ipynb
│   ├── 04_panel_generation/          # Event study panel creation
│   │   ├── minute_panel_generator.ipynb
│   │   └── hourly_panel_generator.ipynb
│   └── 05_analysis/                  # Statistical analysis
│       ├── panel_EDA_visualization.ipynb
│       ├── peak_recovery_analysis.ipynb
│       └── regression_analysis.ipynb
│
├── data/                             # Data files (not included - no copyright)
│   ├── raw/                          # High-frequency trade & quote data
│   ├── processed/                    # Converted minute/hourly data
│   └── events/                       # Event filter files
│
└── results/                          # Analysis outputs (gitignored)
    ├── panels/                       # Generated panel datasets
    ├── figures/                      # Visualization outputs
    └── statistics/                   # Statistical results
```

## 🚀 Getting Started

### Prerequisites

```bash
Python 3.8+
Jupyter Notebook / Google Colab
pandas, numpy, matplotlib, seaborn, scikit-learn
```

### Installation

1. Clone this repository:
```bash
git clone https://github.com/yourusername/Crypto_Liquidity.git
cd Crypto_Liquidity
```

2. Install required packages:
```bash
pip install -r requirements.txt
```

### Data Requirements

⚠️ **Note**: The high-frequency trading data used in this project is proprietary and not included in this repository.

To replicate this analysis, you will need:
- High-frequency trade data with columns: timestamp, price, volume
- High-frequency quote data with columns: timestamp, bid_price, ask_price, bid_size, ask_size
- Event filter file with: event_date, event_type

### Usage

1. **Data Conversion** (notebooks/02_data_conversion/):
   - Process raw millisecond data into minute-level metrics
   - Run separately for each cryptocurrency
   - Output: `minute_liquidity_YYYY_MM.csv` files

2. **Event Hour Detection** (notebooks/03_event_hour_detection/):
   - Identify precise timing of market impact
   - Input: hourly price data + event dates
   - Output: event hour timestamps

3. **Panel Generation** (notebooks/04_panel_generation/):
   - Create event study datasets
   - Align data across multiple events
   - Output: panel DataFrames for each metric

4. **Analysis** (notebooks/05_analysis/):
   - Visualize liquidity patterns around events
   - Quantify impact intensity and recovery time
   - Perform regression and spillover analysis

## 📈 Key Findings

*(Add your research findings here when publishing)*

## 🛠️ Technical Details

### Data Processing
- **Parallel Processing**: Utilizes multi-core processing for large datasets
- **Memory Optimization**: Processes data month-by-month to handle large files
- **Missing Data Handling**: Fills cross-month gaps for events on the 1st of each month

### Event Detection Parameters
- **Detection Window**: ±18 hours around event date
- **Baseline Period**: 30 days before event
- **Post-Event Period**: 10 days after event
- **Impact Criterion**: Maximum high-low price difference

### Statistical Methods
- Panel data regression with fixed effects
- Robustness tests with different model specifications
- Vector autoregression for spillover analysis

## 📚 References

*(Add relevant academic papers and data sources)*

## 👤 Author

**Yixuan GUO**

- Academic Project: Financial Management Course
- Institution: *(Add your institution)*

## 📄 License

This project is for academic and educational purposes only. The data used is proprietary and not included in this repository.

## 🙏 Acknowledgments

- Data provided by course professor
- Thanks to the Financial Management course team

## 📞 Contact

For questions or collaboration opportunities, please contact:
*(Add your contact information)*

---

**Note**: This is a research project developed for academic purposes. The code is provided as-is for educational reference. Data is not included due to copyright restrictions.

