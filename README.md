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
