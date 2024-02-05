# Dexterity API Documentation

## Overview

This API is designed for retrieving fills, mark prices, and settlement data for the Dexterity Protocol, as well as checking the health of the service.

Base URL: `https://dexterity.hxro.com/`

## Endpoints

### 1. List Fills (`/fills`)

- **Description**: Retrieve a list of fill data based on the provided query parameters.
- **Method**: GET
- **Query Parameters**:
  - `product`: (required) Specifies the product to filter the fills.
  - `trg`: (optional) Target identifier for filtering fills.
  - `limit`: (optional) Maximum number of fills to return (default 50, max 50).
  - `before`: (optional) Timestamp to retrieve fills before this time.
  - `after`: (optional) Timestamp to retrieve fills after this time.
- **Example output**:
  ```json
  {
    "fills": [
      {
        "base_size": 0.1, 
        "block_timestamp": "Tue, 23 Jan 2024 20:03:34 GMT", 
        "inserted_at": "Tue, 23 Jan 2024 20:03:36 GMT", 
        "maker_client_order_id": 0, 
        "maker_order_id": "3100752596320763380398529587648057", 
        "maker_order_nonce": "26016602", 
        "maker_trg": "DzbH4iBeSSFFSdEAhMwvcY7FjWMkBa4XYzTdoGEETj7m", 
        "mpg": "4cKB5xKtDpv4xo6ZxyiEvtyX3HgXzyJUS1Y8hAfoNkMT", 
        "price": 39137.0, 
        "product": "BTCUSD-PERP", 
        "quote_size": 3913.7, 
        "slot": 243670447, 
        "taker_client_order_id": 0, 
        "taker_order_nonce": "26016639", 
        "taker_side": "bid", 
        "taker_trg": "BYxWxkfP3A8W2UqeR6b1UbvG9SgHuah2fz3LwVV5zrSW", 
        "tx_sig": "3sYZJJ4Fi91LLrKyphLDydAnxGTXHE3DjZdd93ieySnxkuyaqEZsynVB8wPL881y5wbZJagmHBoMKXzD3UB77aPK"
      }
    ]
  }
  ```

### 2. List Mark Prices (`/mark_prices`)

- **Description**: Fetch a list of mark prices for a specified product.
- **Method**: GET
- **Query Parameters**:
  - `product`: (required) Specifies the product to filter the mark prices.
  - `limit`: (optional) Maximum number of prices to return (default 50, max 1000).
  - `before`: (optional) Timestamp to retrieve prices before this time.
  - `after`: (optional) Timestamp to retrieve prices after this time.
- **Example output**:
  ```json
    {
      "mark_prices": [
        {
          "block_timestamp": "Thu, 25 Jan 2024 19:46:41 GMT", 
          "inserted_at": "Thu, 25 Jan 2024 19:46:43 GMT", 
          "mark_price": 39893.523645, 
          "mpg": "4cKB5xKtDpv4xo6ZxyiEvtyX3HgXzyJUS1Y8hAfoNkMT", 
          "product": "BTCUSD-PERP", 
          "slot": 244083906, 
          "tx_sig": "FLqgDnqcurLxVf8SCg63vKGcFDHUTFm1eyEPzKMeXsEEAVjYCUsjkzGkcSvyqUt3Xn4HQAZT6vh8hpqqdqHbgdG"
        }
     ]
   }
  ```

### 3. List Settlements (`/settlements`)

- **Description**: Obtain a list of settlements for a given product.
- **Method**: GET
- **Query Parameters**:
  - `product`: (required) Specifies the product to filter the settlements.
  - `limit`: (optional) Maximum number of settlements to return (default 50, max 1000).
  - `before`: (optional) Timestamp to retrieve settlements before this time.
  - `after`: (optional) Timestamp to retrieve settlements after this time.
- **Example output**:
  ```json
  {
    "settlements": [
      {
        "block_timestamp": "Thu, 25 Jan 2024 19:37:30 GMT", 
        "elapsed": 3622.0, 
        "full_period": 86400.0, 
        "index_price": 39832.647, 
        "inserted_at": "Thu, 25 Jan 2024 19:37:31 GMT", 
        "mark_price": 39924.5, 
        "mpg": "4cKB5xKtDpv4xo6ZxyiEvtyX3HgXzyJUS1Y8hAfoNkMT", 
        "product": "BTCUSD-PERP", 
        "result": -3.67412, 
        "slot": 244082564, 
        "tx_sig": "39p78ZWtAoRmsVsjfM3mwcjp8a4vQ7sxKXj5xA8HWioDnQUJurYmJechcCKmFEtu4xcsyLhfVZ6WJn4qDmJhTVgC"
      }
    ]
  }
  ```

### 4. Health Check (`/health`)

- **Description**: Check the health of the API service.
- **Method**: GET
- **Example output**:
  ```json
  {
    "response": "OK"
  }
  ```

### 5. Calculate Margin Levels (`/margin_levels`)

- **Description**: Calculates and returns the margin levels for groups of products based on their correlation and the provided positions & product data.
- **Method**: POST
- **Request Body**:
  - JSON object containing an array of positions per MPG:
    - `mpg`: The name of the Market Product Group.
    - `positions`: An array of position objects, where each object includes:
      - `product`: Product name.
      - `position_weight`: USD notional value of the position.
      - `product_std`: The % standard deviation of the product's price (STD/MARK_PRICE).
- **Example Output**:
  ```json
  [
    [
      "STAKECHIP",
      [
        {
          "initial_margin": 16.0,
          "maintenance_margin": 8.0,
          "products": [
            "SOLUSD-PERP",
            "MSOLUSD-PERP",
            "JSOLUSD-PERP"
          ]
        },
        {
          "initial_margin": 30.14,
          "maintenance_margin": 15.07,
          "products": [
            "BTCUSD-PERP"
          ]
        }
      ]
    ],
  ]
  ```

## Examples

### Curl Examples

#### Fetching for Positions Margin Levels

```bash
  curl -X POST https://dexterity.hxro.com/margin_levels \
  -H "Content-Type: application/json" \
  -d '[
      {
          "mpg": "STAKECHIP",
          "positions": [
              {"product": "SOLUSD-PERP", "position_weight": -48, "product_std": 0.051},
              {"product": "MSOLUSD-PERP", "position_weight": 111.96, "product_std": 0.05},
              {"product": "BTCUSD-PERP", "position_weight": 200.96, "product_std": 0.05},
              {"product": "JSOLUSD-PERP", "position_weight": 40.96, "product_std": 0.05}
          ]
      },
      {
          "mpg": "BLUECHIP",
          "positions": [
              {"product": "SOLUSD-PERP", "position_weight": -200, "product_std": 0.05},
              {"product": "ETHUSD-PERP", "position_weight": 50.96, "product_std": 0.06},
              {"product": "BTCUSD-PERP", "position_weight": 200.96, "product_std": 0.02}
          ]
      }
  ]'
  ```

### JavaScript Examples

#### Fetching Fills

```javascript
fetch('https://dexterity.hxro.com/fills?product=BTC&limit=10')
  .then(response => response.json())
  .then(data => console.log(data));
```

#### Fetching Mark Prices

```javascript
fetch('https://dexterity.hxro.com/mark_prices?product=BTC&limit=10')
  .then(response => response.json())
  .then(data => console.log(data));
```

### Python Examples

#### Fetching Fills

```python
import requests

response = requests.get('https://dexterity.hxro.com/fills?product=BTC&limit=10')
fills = response.json()
print(fills)
```

#### Fetching Mark Prices

```python
import requests

response = requests.get('https://dexterity.hxro.com/mark_prices?product=BTC&limit=10')
mark_prices = response.json()
print(mark_prices)
```
