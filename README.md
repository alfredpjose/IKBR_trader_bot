﻿# IBKR Trading Bot

A modular, extensible trading bot for Interactive Brokers with a focus on strategy development and testing.

## Overview

This bot provides a framework for implementing and executing trading strategies with Interactive Brokers (IBKR). It supports both paper trading and live trading, with a focus on safety, extensibility, and strategy development.

## Features

- Connect to IBKR via TWS or IB Gateway API
- Paper trading support for safe testing
- Multiple strategy support
- Real-time and historical data handling
- Order management with various order types
- Performance tracking and reporting
- Backtesting framework

## Getting Started

### Prerequisites

- Python 3.7+
- Interactive Brokers account
- TWS (Trader Workstation) or IB Gateway installed and running
- IBKR Python API installed

### Installation

1. Clone this repository:
```bash
git clone https://github.com/alfredpjose/IKBR_trader_bot.git
cd IKBR_trader_bot
```

2. Install the required dependencies:
```bash
pip install -r requirements.txt
```

3. Install the IBKR Python API:
```bash
pip install ibapi
```

### Setting Up IBKR TWS or IB Gateway

1. Launch TWS or IB Gateway
2. Go to Edit -> Global Configuration -> API -> Settings
3. Enable "Enable ActiveX and Socket Clients"
4. Set the Socket port to 7497 for paper trading or 7496 for live trading
5. Disable "Read-Only API"
6. Check "Allow connections from localhost only" (for security)

### Configuration

Customize the settings in `src/config/settings.py` or create a custom configuration file:

```python
# Example custom configuration
{
    "IBKR_HOST": "127.0.0.1",
    "IBKR_PORT": 7497,
    "IBKR_CLIENT_ID": 1,
    "MAX_POSITIONS": 5,
    "MAX_POSITION_SIZE": 0.1,
    "ENABLE_STOP_LOSS": true,
    "STOP_LOSS_PERCENT": 0.05
}
```

### Running the Bot

#### Test Connection

First, test the connection to IBKR:

```bash
python src/main.py --test-connection
```

#### Run in Paper Trading Mode

To run the bot in paper trading mode:

```bash
python src/main.py --mode paper
```

#### Run with a Specific Strategy

To run the bot with a specific strategy:

```bash
python src/main.py --mode paper --strategy momentum
```

#### Run with a Custom Configuration

To run the bot with a custom configuration file:

```bash
python src/main.py --mode paper --config path/to/config.json
```

## Project Structure

```
IKBR_trader_bot/
├── src/                          # Main source code
│   ├── main.py                   # Application entry point
│   ├── config/                   # Configuration files
│   ├── core/                     # Core functionality
│   ├── connectors/               # IBKR API connectors
│   ├── strategies/               # Trading strategies
│   ├── data/                     # Data handling
│   ├── backtesting/              # Backtesting engine
│   └── utils/                    # Utilities
├── tests/                        # Unit and integration tests
├── logs/                         # Log files
└── historical_data/              # Historical price data
```

## Creating Custom Strategies

To create a custom strategy, inherit from the `BaseStrategy` class:

```python
from src.strategies.base_strategy import BaseStrategy

class MyCustomStrategy(BaseStrategy):
    def __init__(self, **kwargs):
        super().__init__(name="MyStrategy", **kwargs)
        # Custom initialization
    
    def generate_signals(self):
        # Implement your strategy logic here
        # Return a list of signals
        signals = []
        return signals
```

## Safety Features

- Paper trading mode for safe testing
- Position size limits
- Stop-loss protection
- Risk management checks
- Disconnect handling

## Disclaimer

This trading bot is provided for educational and research purposes only. Trading securities involves risk, and you should only trade with money you can afford to lose.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
