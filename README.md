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
  [
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
  ```

### 2. List Mark Prices (`/mark_prices`)

- **Description**: Fetch a list of mark prices for a specified product.
- **Method**: GET
- **Query Parameters**:
  - `product`: (required) Specifies the product to filter the mark prices.
  - `limit`: (optional) Maximum number of prices to return (default 50, max 1000).
  - `before`: (optional) Timestamp to retrieve prices before this time.
  - `after`: (optional) Timestamp to retrieve prices after this time.

### 3. List Settlements (`/settlements`)

- **Description**: Obtain a list of settlements for a given product.
- **Method**: GET
- **Query Parameters**:
  - `product`: (required) Specifies the product to filter the settlements.
  - `limit`: (optional) Maximum number of settlements to return (default 50, max 1000).
  - `before`: (optional) Timestamp to retrieve settlements before this time.
  - `after`: (optional) Timestamp to retrieve settlements after this time.

### 4. Health Check (`/health`)

- **Description**: Check the health of the API service.
- **Method**: GET

## Examples

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
