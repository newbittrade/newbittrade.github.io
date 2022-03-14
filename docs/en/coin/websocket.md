---
sort: 8 # follow a certain sequence of letters or numbers
---

# WebSocket Market Data

### Access instructions


#### WebSocket domain name


##### wss://wss-api.monkey.com/trade/multiple

#### Data compression

All data returned by the WebSocket quotation interface is GZIP compressed, and the client needs to decompress the data after receiving it.

#### The heartbeat message


After the user's Websocket client connects to the hot coin server, the hot coin server will send ping messages to the user periodically (currently set to 5 seconds), as follows:
```{"ping": "ping"}```

When the user's Websocket client receives this heartbeat message, it should return a PONG message as follows:
```{"pong": "pong"}```

#### Subscribe to the topic


After successfully establishing a connection to the Websocket server, the Websocket client sends a request to subscribe to a specific topic:

```{"sub": "topic to subscribe"}```

for example：```{"sub": "market.btc_usdt.trade.depth"}```

After a successful subscription, the Websocket client will receive a confirmation message:

```json
    {
      "ch": "market.btc_usdt.trade.depth",
      "code": 200,
      "msg": "SUCCESS",
      "status": "ok",
      "ts": 1632878832006
    }
```

After that, once the subscribed topic has data update, the hot coin server will push the update message to the Websocket client.

#### unsubscribe

The unsubscribe format is as follows:```{"unsub": "topic to unsubscribe"}```

Unsubscription confirmed successfully.

&nbsp;

### Kline data

Request data:```{"sub":"market.$symbol$.kline.$period$"}```


Unsubscribe:```{"unsub":"market.$symbol$.kline.$period$"}```

> **Parameters**

| Parameter   | Data Type | Mandatory | Description     | remark                          |
| ------ | -------- | -------- | -------- | ----------------------------- |
| symbol | String   | y       | symbol | btc_usdt                      |
| period | String   | y       | Kline cycle| 1m,5m,15m,30m,1h,2h,4h,6h,12h,1d,3d,5d,1w,1mo |

* After the subscription is successful or unsubscribed, the server returns data:

```json
    {
        "ch": "market.btc_usdt.kline.1m",
        "code": 200,
        "code": 200,
        "msg": "SUCCESS",
        "status": "ok",
        "ts": 1489474081631
    }
```

Field description:

###### [timestamp,open,high,low,close,volume]
###### [ts, open, high, low, close, vol]


| Parameter  | Data Type | Mandatory | Description   | remark                                          |
| ----- | -------- | -------- | ------ | --------------------------------------- |
| ts    | String   | y       | timestamp   | Time range[1501174800000, 2556115200000] |
| open  | String   | y       | open | 995.37                                     |
| high  | String   | y       | high | 996.75                                     |
| low   | String   | y       | low | 995.36                                     |
| close | String   | y       | close | 996.75                                     |
| vol   | String   | y       | volume | 9.112                                      |

### Market depth data


Request data:```{"sub":"market.$symbol$.trade.depth"}```


Unsubscribe:```{"unsub":"market.$symbol$.trade.depth"}```

> **Parameters**

| Parameter   | Data Type | Mandatory | Description     | remark     |
| ------ | -------- | -------- | -------- | -------- |
| symbol | String   | y       | symbol | btc_usdt |

* After the subscription is successful or unsubscribed, the server returns data:

```json
    {
        "ch": "market.btc_usdt.trade.depth",
        "code": 200,
        "msg": "SUCCESS",
        "status": "ok",
        "ts": 1489474081631
    }
```

Field description:

| Parameter              | Data Type        | Mandatory | Description                         | Default                |
| ----------------- | --------------- | -------- | ---------------------------- | --------------------- |
| bids              | [String,String] | y      | 【Buyer's price, buyer's depth】      | ["9999.39","0.0098"]  |
| asks              | [String,String] | y      | 【Seller price, seller depth measure】    | ["10010.98","0.0099"] |
| last              | String          | y       | last                       | 0                     |
| open              | String          | y       | open                       | 0                     |
| cny               | String          | y       | cny               | 0                     |
| netValue          | String          | y       | ETF net| 0                     |
| buyOrSellCnyPrice | String          | y       | Used when buying or selling RMB valuation| 0                     |

### Buy and sell every price

Request data: ```{"sub":"market.$symbol$.trade.bbo"}```


Unsubscribe:```{"unsub":"market.$symbol$.trade.bbo"}```


> **Parameters**

| Parameter   | Data Type | Mandatory | Description     | remark     |
| ------ | -------- | -------- | -------- | -------- |
| symbol | String   | y       | symbol | btc_usdt |

* After the subscription is successful or unsubscribed, the server returns data:

```json
    {
        "ch": "market.btc_usdt.trade.bbo",
        "code": 200,
        "msg": "SUCCESS",
        "status": "ok",
        "ts": 1489474081631
    }
```

Field description:

| Parameter              | Data Type        | Mandatory | Description                         | Default                |
| ----------------- | --------------- | -------- | ---------------------------- | --------------------- |
| symbol              | String | y       | symbol      | btc_usdt  |
| bid              | String | y       | Buy a price    | 0 |
| bidSize              | String          | y       | Buy a quantity                       | 0                     |
| ask              | String          | y       | Sold for a price                       | 0                     |
| askSize               | String          | y        | Sell a quantity of              | 0                     |
| last          | String          | y        | last                      | 0                     |

### 24H aggregate market data

Request data:```{"sub":"market.$symbol$.24h.tickers"}```


Unsubscribe:```{"unsub":"market.$symbol$.24h.tickers"}```

> **Parameters**

| Parameter   | Data Type | Mandatory | Description     | remark     |
| ------ | -------- | -------- | -------- | -------- |
| symbol | String   | y        | symbol | btc_usdt |

* After the subscription is successful or unsubscribed, the server returns data:

```json
    {
        "ch": "market.btc_usdt.24h.tickers",
        "code": 200,
        "msg": "SUCCESS",
        "status": "ok",
        "ts": 1489474081631
    }
```

Field description:

| Parameter          | Data Type | Mandatory | Description                     | remark |
| ------------- | -------- | -------- | ------------------------ | ---- |
| sellShortName | String   | y        | sellShortName:BTC      |      |
| sellSymbol    | String   | y        | sellSymbol:bitcoin  |      |
| buyShortName  | String   | y        | buyShortName:ETH      |      |
| buySymbol     | String   | y        | buySymbol:ethereum |      |
| high          | String   | y        | high                   |      |
| open          | String   | y        | open                   |      |
| low           | String   | y        | low                   |      |
| close         | String   | y        | close                   |      |
| volume        | String   | y        | volume                   |      |
| change        | String   | y        | change                   |      |
| cny           | String   | y        | cny       |      |
| tradeId       | Integer  | y        | tradeId                   |      |
| last          | String   | y        | last         |      |
| imageUrl      | String   | y        |                          |      |
| netValue      | String   | y        | ETF net                  |      |

### Real-time transaction details


Request data:```{"sub":"market.$symbol$.trade.detail"}```


Unsubscribe:```{"unsub":"market.$symbol$.trade.detail"}```

> **Parameters**

| Parameter   | Data Type | Mandatory | Description     | remark     |
| ------ | -------- | -------- | -------- | -------- |
| symbol | String   | y        | symbol | btc_usdt |

* After the subscription is successful or unsubscribed, the server returns data:

```json
    {
        "ch": "market.btc_usdt.trade.detail",
        "code": 200,
        "msg": "SUCCESS",
        "status": "ok",
        "ts": 1489474081631
    }
```

Field description:

| Parameter      | Data Type | Mandatory | Default                    | Description                                       | remark |
| --------- | -------- | -------- | ------------------------- | ------------------------------------------ | ---- |
| amount    | String   | y        | amount                    | 0.0099                                     |      |
| ts        | String   | y        | time                  | time range[1501174800000, 2556115200000] |      |
| tradeId   | Integer  | y        | tradeId              | tradeId                                 |      |
| price     | String   | y        | price                  | 401.74                                     |      |
| direction | String   | y        | buy/sell | [buy/sell]                                 |      |








