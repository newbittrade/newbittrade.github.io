---
sort: 8 # follow a certain sequence of letters or numbers
---

# WebSocket行情数据

### 接入说明

#### WebSocket域名

##### wss://wss-api.monkey.com/trade/multiple

#### 数据压缩

WebSocket行情接口返回的所有数据进行了GZIP压缩，客户端在收到数据之后需要解压。

#### 心跳消息

当用户的Websocket客户端连接到Monkey服务器后，Monkey服务器会定期（当前设为5秒）向其发送ping消息，如下：
```{"ping": "ping"}```

当用户的Websocket客户端接收到此心跳消息后，应返回pong消息，如下：
```{"pong": "pong"}```

#### 订阅主题

成功建立与Websocket服务器的连接后，Websocket客户端发送请求以订阅特定主题：
```{"sub": "topic to subscribe"}```

比如：```{"sub": "market.btc_usdt.trade.depth"}```

成功订阅后，Websocket客户端将收到确认消息：

```json
    {
      "ch": "market.btc_usdt.trade.depth",
      "code": 200,
      "msg": "SUCCESS",
      "status": "ok",
      "ts": 1632878832006
    }
```

之后, 一旦所订阅的主题有数据更新，Monkey服务器将向Websocket客户端推送更新消息。

#### 取消订阅

取消订阅的格式如下：```{"unsub": "topic to unsubscribe"}```

取消订阅成功确认。

&nbsp;

### K线数据

请求数据：```{"sub":"market.$symbol$.kline.$period$"}```


取消订阅：```{"unsub":"market.$symbol$.kline.$period$"}```

> **参数说明**

| 参数   | 数据类型 | 是否必须 | 描述     | 备注                          |
| ------ | -------- | -------- | -------- | ----------------------------- |
| symbol | String   | 是       | 交易代码 | btc_usdt                      |
| period | String   | 是       | k线周期  | 1m,5m,15m,30m,1h,2h,4h,6h,12h,1d,3d,5d,1w,1mo |

* 订阅成功或者取消订阅后，服务器返回数据:

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

返回字段说明:

###### [时间,开盘价,最高价,最低价,收盘价,成交量]
###### [ts, open, high, low, close, vol]


| 参数  | 数据类型 | 是否必填 | 描述   | 备注                                          |
| ----- | -------- | -------- | ------ | --------------------------------------- |
| ts    | String   | 是       | 时间   | 时间有效范围[1501174800000, 2556115200000] |
| open  | String   | 是       | 开盘价 | 995.37                                     |
| high  | String   | 是       | 最高价 | 996.75                                     |
| low   | String   | 是       | 最低价 | 995.36                                     |
| close | String   | 是       | 收盘价 | 996.75                                     |
| vol   | String   | 是       | 交易量 | 9.112                                      |

### 市场深度数据

请求数据：```{"sub":"market.$symbol$.trade.depth"}```


取消订阅：```{"unsub":"market.$symbol$.trade.depth"}```

> **参数说明**

| 参数   | 数据类型 | 是否必须 | 描述     | 备注     |
| ------ | -------- | -------- | -------- | -------- |
| symbol | String   | 是       | 交易代码 | btc_usdt |

* 订阅成功或者取消订阅后，服务器返回数据:

```json
    {
        "ch": "market.btc_usdt.trade.depth",
        "code": 200,
        "msg": "SUCCESS",
        "status": "ok",
        "ts": 1489474081631
    }
```

返回字段说明:

| 参数              | 数据类型        | 是否必填 | 描述                         | 默认值                |
| ----------------- | --------------- | -------- | ---------------------------- | --------------------- |
| bids              | [String,String] | 是       | 【买方价格,买方深度量】      | ["9999.39","0.0098"]  |
| asks              | [String,String] | 是       | 【卖方价格,卖方深度度量】    | ["10010.98","0.0099"] |
| last              | String          | 是       | 最新价                       | 0                     |
| open              | String          | 是       | 开盘价                       | 0                     |
| cny               | String          | 是       | 折合人民币价格               | 0                     |
| netValue          | String          | 是       | ETF净值                      | 0                     |
| buyOrSellCnyPrice | String          | 是       | 买入或者卖出人民币估值时使用 | 0                     |

### 买一卖一逐笔行情

请求数据： ```{"sub":"market.$symbol$.trade.bbo"}```


取消订阅：```{"unsub":"market.$symbol$.trade.bbo"}```


> **参数说明**

| 参数   | 数据类型 | 是否必须 | 描述     | 备注     |
| ------ | -------- | -------- | -------- | -------- |
| symbol | String   | 是       | 交易代码 | btc_usdt |

* 订阅成功或者取消订阅后，服务器返回数据:

```json
    {
        "ch": "market.btc_usdt.trade.bbo",
        "code": 200,
        "msg": "SUCCESS",
        "status": "ok",
        "ts": 1489474081631
    }
```

返回字段说明:

| 参数              | 数据类型        | 是否必填 | 描述                         | 默认值                |
| ----------------- | --------------- | -------- | ---------------------------- | --------------------- |
| symbol              | String | 是       | 交易代码      | btc_usdt  |
| bid              | String | 是       | 买一价    | 0 |
| bidSize              | String          | 是       | 买一量                       | 0                     |
| ask              | String          | 是       | 卖一价                       | 0                     |
| askSize               | String          | 是       | 卖一量               | 0                     |
| last          | String          | 是       | 最新价                      | 0                     |

### 24H聚合行情数据

请求数据：```{"sub":"market.$symbol$.24h.tickers"}```


取消订阅：```{"unsub":"market.$symbol$.24h.tickers"}```

> **参数说明**

| 参数   | 数据类型 | 是否必须 | 描述     | 备注     |
| ------ | -------- | -------- | -------- | -------- |
| symbol | String   | 是       | 交易代码 | btc_usdt |

* 订阅成功或者取消订阅后，服务器返回数据:

```json
    {
        "ch": "market.btc_usdt.24h.tickers",
        "code": 200,
        "msg": "SUCCESS",
        "status": "ok",
        "ts": 1489474081631
    }
```

返回字段说明:

| 参数          | 数据类型 | 是否必填 | 描述                     | 备注 |
| ------------- | -------- | -------- | ------------------------ | ---- |
| sellShortName | String   | 是       | 卖方币种简称:BTC      |      |
| sellSymbol    | String   | 是       | 卖方币种全称:bitcoin  |      |
| buyShortName  | String   | 是       | 买方币种简称:ETH      |      |
| buySymbol     | String   | 是       | 买方币种全称:ethereum |      |
| high          | String   | 是       | 最高价                   |      |
| open          | String   | 是       | 开盘价                   |      |
| low           | String   | 是       | 最低价                   |      |
| close         | String   | 是       | 收盘价                   |      |
| volume        | String   | 是       | 交易量                   |      |
| change        | String   | 是       | 涨跌幅                   |      |
| cny           | String   | 是       | 折合人民币的最新价       |      |
| tradeId       | Integer  | 是       | 交易代码ID                   |      |
| last          | String   | 是       | 最新价(原始价格)         |      |
| imageUrl      | String   | 是       |                          |      |
| netValue      | String   | 否       | ETF净值                  |      |

### 实时成交明细

请求数据：```{"sub":"market.$symbol$.trade.detail"}```


取消订阅：```{"unsub":"market.$symbol$.trade.detail"}```

> **参数说明**

| 参数   | 数据类型 | 是否必须 | 描述     | 备注     |
| ------ | -------- | -------- | -------- | -------- |
| symbol | String   | 是       | 交易代码 | btc_usdt |

* 订阅成功或者取消订阅后，服务器返回数据:

```json
    {
        "ch": "market.btc_usdt.trade.detail",
        "code": 200,
        "msg": "SUCCESS",
        "status": "ok",
        "ts": 1489474081631
    }
```

返回字段说明:

| 参数      | 数据类型 | 是否必填 | 默认值                    | 描述                                       | 备注 |
| --------- | -------- | -------- | ------------------------- | ------------------------------------------ | ---- |
| amount    | String   | 是       | 成交量                    | 0.0099                                     |      |
| ts        | String   | 是       | 成交时间                  | 有效时间范围[1501174800000, 2556115200000] |      |
| tradeId   | Integer  | 是       | 交易代码ID              | 交易代码ID                                 |      |
| price     | String   | 是       | 成交价格                  | 401.74                                     |      |
| direction | String   | 是       | 买单【buy】或卖单【sell】 | [buy/sell]                                 |      |








