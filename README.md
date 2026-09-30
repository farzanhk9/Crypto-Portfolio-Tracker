import requests1

def get_price(symbol):
    url = "https://api.coingecko.com/api/v3/simple/price"
    params = {
        "ids": symbol,
        "vs_currencies": "usd"
    }

    response = requests.get(url, params=params, timeout=10)
    response.raise_for_status()

    data = response.json()
    return data[symbol]["usd"]


def calculate_portfolio(assets):
    total = 0

    print("\n--- Portfolio ---")

    for asset in assets:
        symbol = asset["symbol"]
        amount = asset["amount"]

        try:
            price = get_price(symbol)
            value = price * amount
            total += value

            print(
                f"{symbol.upper():10} "
                f"{amount:<12} "
                f"${price:<12,.2f} "
                f"Value: ${value:,.2f}"
            )

        except Exception as error:
            print(f"Could not get price for {symbol}: {error}")

    print("-" * 45)
    print(f"Total Portfolio Value: ${total:,.2f}")


if __name__ == "__main__":

    my_assets = [
        {"symbol": "bitcoin", "amount": 0.01},
        {"symbol": "ethereum", "amount": 0.1},
        {"symbol": "solana", "amount": 1}
    ]

    calculate_portfolio(my_assets)

# Crypto Portfolio Tracker

A simple Python tool for tracking cryptocurrency portfolio value.

## Features

- Fetches live crypto prices
- Calculates individual asset values
- Calculates total portfolio value
- Simple and beginner-friendly

## Installation

```bash
pip install -r requirements.txt
    
