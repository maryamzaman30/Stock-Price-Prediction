# AI/ML Engineering Internship - DevelopersHub Corporation

This project is a part of my **AI/ML Engineering Internship** at **DevelopersHub Corporation**, Islamabad.

## Internship Details

- **Company:** DevelopersHub Corporation, Islamabad 🇵🇰
- **Internship Period:** July - August 2025


# Stock Price Prediction Project

## Task Objective

This project demonstrates how to predict next-day stock closing prices using machine learning models with historical stock data. The primary goal is to develop predictive models that can forecast stock prices based on technical indicators and historical price patterns, providing insights into potential stock price movements.

## Dataset Used

- **Stock Symbol**: AAPL (Apple Inc.)
- **Data Source**: Yahoo Finance (yfinance API)
- **Time Period**: August 16, 2019 to August 15, 2024
- **Data Points**: 1,258 trading days
- **Features**: OHLCV (Open, High, Low, Close, Volume) data

### ⚠️ Data Fetching Note

Despite following all recommended procedures to retrieve historical stock data using the `yfinance` Python library, I encountered persistent errors across multiple tickers (e.g., AAPL, TSLA, GOOGL, MSFT). Specifically, the library returned:

```
JSONDecodeError: Expecting value: line 1 column 1 (char 0)
```

This error typically indicates that the response from Yahoo Finance was empty or malformed. To resolve this, I attempted the following:

- Upgraded `yfinance` to the latest version
- Inserted delays between requests to avoid throttling
- Disabled multithreading
- Broke requests into smaller time chunks
- Verified internet connectivity and firewall settings
- Attempted direct downloads from Yahoo Finance’s website

Unfortunately, Yahoo Finance has recently restricted CSV downloads behind a Yahoo Finance Gold subscription, and the web interface no longer allows free access to downloadable historical data.

### ✅ Workaround

To proceed with the analysis, I sourced a clean and publicly available dataset from GitHub containing historical data for Apple Inc. (AAPL). This ensures continuity with the project’s objectives while maintaining data integrity and relevance.

Dataset from GitHub - https://github.com/kishoreramakrishnan-ds/stock-market-analysis-aapl/blob/main/AAPL.csv

### Data Structure
The dataset contains daily stock information including:
- Opening, High, Low, and Closing prices
- Adjusted closing prices
- Trading volume
- Date index for time-series analysis

## Models Applied

### 1. Linear Regression
- **Purpose**: Baseline model for stock price prediction
- **Features**: 26 engineered technical indicators
- **Training**: 80% of data for training, 20% for testing
- **Scaling**: StandardScaler applied to normalize features

### 2. Random Forest Regressor
- **Purpose**: Advanced ensemble model for improved prediction accuracy
- **Features**: Same 26 engineered features as Linear Regression
- **Hyperparameters**: Default scikit-learn parameters
- **Advantage**: Captures non-linear relationships and feature interactions

## Feature Engineering

The project creates 26 technical indicators from raw OHLCV data:

### Price Movement Features
- Price changes and returns
- High-Low spreads
- Open-Close differences

### Moving Averages
- 5-day, 10-day, and 20-day moving averages
- Price position relative to moving averages
- Moving average ratios

### Volume Features
- Volume changes and ratios
- Price-volume relationships

### Technical Indicators
- Candlestick patterns (body size, shadows)
- Price momentum indicators
- Lagged features (previous day values)

## Key Results and Findings

### Model Performance Comparison

| Model | MAE | RMSE | R² |
|-------|-----|------|----|
| Linear Regression | $2.04 | $2.82 | 0.9718 |
| Random Forest | $6.66 | $12.14 | 0.4777 |

### Key Insights

1. **Linear Regression Superiority**: 
   - Achieved significantly better performance with R² = 0.9718
   - Lower error rates (MAE: $2.04, RMSE: $2.82)
   - More suitable for this specific prediction task

2. **Random Forest Performance**:
   - Moderate performance with R² = 0.4777
   - Higher error rates (MAE: $6.66, RMSE: $12.14)
   - Better at capturing complex non-linear patterns

3. **Feature Importance**:
   - Moving averages and price ratios are most predictive
   - Technical indicators provide valuable trend information
   - Volume features contribute to prediction accuracy

4. **Data Coverage**:
   - 5+ years of historical data provides robust training
   - Models trained on 1,006 days, tested on 252 days
   - Covers various market conditions including COVID-19 period

### Limitations and Considerations

- **Market Volatility**: Models may struggle during high volatility periods
- **Feature Dependence**: Performance heavily relies on technical indicators
- **Market Regime Changes**: Models may need retraining for different market conditions
- **Single Stock Focus**: Results specific to AAPL, may not generalize to other stocks

## Technical Implementation

- **Language**: Python 3.x
- **Key Libraries**: pandas, numpy, scikit-learn, matplotlib, seaborn
- **Data Processing**: Feature engineering, scaling, train-test splitting
- **Evaluation Metrics**: MAE, RMSE, R² score
- **Visualization**: Price predictions, error analysis, feature importance plots

## Future Enhancements

1. **Additional Features**: Market sentiment, economic indicators, sector performance
2. **Advanced Models**: LSTM networks, XGBoost, ensemble methods
3. **Multi-Stock Analysis**: Extend to portfolio of stocks
4. **Real-time Updates**: Implement live data feeds and model retraining
5. **Risk Management**: Incorporate prediction confidence intervals and risk metrics

## Usage

1. Install required dependencies: `pip install -r requirements.txt`
2. Run the Jupyter notebook: `jupyter notebook stock_price_prediction.ipynb`
3. Execute cells sequentially to perform the complete analysis
4. Modify stock symbols or parameters as needed

## Dependencies

- yfinance==0.2.36
- pandas==2.1.4
- numpy==1.24.3
- matplotlib==3.7.2
- seaborn==0.12.2
- scikit-learn==1.3.2
- jupyter==1.0.0
