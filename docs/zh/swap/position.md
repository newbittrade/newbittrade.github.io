---
sort: 6 # follow a certain sequence of letters or numbers
---
# 持仓接口

&nbsp;

### 仓位列表

#### GET /api/v1/perpetual/position/{contractCode}/list

#### 请求参数：

##### 路径参数

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
contractCode|y|string|合约code||

##### Query

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
AccessKeyId|y|string|访问key||
SignatureVersion|y|string|版本||
SignatureMethod|y|string|签名方法||HmacSHA256
Signature|y|string|签名||
Timestamp|y|string|时间戳||


```json
[
    {
        "amount": "4867",
        "base": "fbtc",
        "closingAmount": "0",
        "contractCode": "fbtcusd",
        "lever": "100",
        "liqudatePrice": "3237.43",
        "maintenanceMargin": "0.02527905",
        "markPrice": "9659.25",
        "minQuoteDigit": 2,
        "minTradeDigit": 8,
        "openMargin": "0.14863957",
        "price": "9626.54",
        "quote": "usd",
        "realizedSurplus": "0.00413503",
        "side": "long",
        "size": "5.05581019",
        "type": 0
    }
]
```

#### 返回：

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
amount|y|string|持仓数量||
base|y|string|基础货币名,如BTC、ETH||
closingAmount|y|int|成交数量||
contractCode|y|string|合约||
gear|y|string|风险限额||
lever|y|string|杠杆||
liqudatePrice|y|string|强平价||
maintenanceMargin|y|string|维持保证金||
markPrice|y|string|标记价格||
minQuoteDigit|y|string|计价货币最小交易小数位||
minTradeDigit|y|string|基础货币最小交易小数位||
openMargin|y|string|开仓保证金||
price|y|string|成交均价||
quote|y|string|计价货币名，USD,CNY,USDT||
realizedSurplus|y|已实现盈亏||
side|y|string|仓位类型，long多，short空||
size|y|string|仓位价值||
type|y|string|0：全仓，1：逐仓||

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

### 获取所有档位对应的保证金率和杠杆

#### GET /v1/perpetual/public/{contractCode}/lever-gears

#### 请求参数：

##### 路径参数

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
contractCode|y|string|合约code||

##### Query

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
AccessKeyId|y|string|访问key||
SignatureVersion|y|string|版本||
SignatureMethod|y|string|签名方法||HmacSHA256
Signature|y|string|签名||
Timestamp|y|string|时间戳||


```json
{
    "code": 200,
    "data": [
        {
            "entryRate": "0.008",
            "gear": 1,
            "lever": "125",
            "maintainRate": "0.004",
            "maxOpenAmount": "100"
        }
    ]
    "msg": "success"
}

```

#### 返回：

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
entryRate|y|string|开仓保证金率||
gear|y|int|档位||
lever|y|string|杠杆||
maintainRate|y|string|维持保证金率||
maxOpenAmount|y|string|最大可开张数||

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

### 仓位和限额设置

#### GET /api/v1/perpetual/position/{contractCode}/configs

#### 请求参数：

##### 路径参数

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
contractCode|y|string|合约code||

##### Query

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
AccessKeyId|y|string|访问key||
SignatureVersion|y|string|版本||
SignatureMethod|y|string|签名方法||HmacSHA256
Signature|y|string|签名||
Timestamp|y|string|时间戳||


```json
{
  "contractCode": "btcusdt",
  "feeRate": "0.00065",
  "fundRate": "0.00375",
  "indexPrice": "37591.04",
  "longPositionConfigDetails": {
    "initOpenMarginRate": "0.008",
    "lever": "125",
    "maintainRate": "0.004",
    "maxOpenAmount": "100",
    "side": "long"
  },
  "makerFeeRate": "0.00035",
  "markPrice": "37704.1",
  "shortPositionConfigDetails": {
    "initOpenMarginRate": "0.008",
    "lever": "125",
    "maintainRate": "0.004",
    "maxOpenAmount": "100",
    "side": "short"
  },
  "takerFeeRate": "0.00065",
  "type": 0,
  "unitAmount": "0.01"
}
```


#### 返回：

**main**

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
contractCode|y|string|合约code||
feeRate|y|int|手续费率||
fundRate|y|string|资金费率||
indexPrice|y|string|指数价格||
markPrice|y|string|标记价格||
type|y|string|0：全仓，1：逐仓||
unitAmount|y|string|张数：一张合约对应的quote面值||
makerFeeRate|y|string|maker手续费率||
takerFeeRate|y|string|taker手续费率||

**|longPositionConfigDetails||shortPositionConfigDetails|仓位详情**

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
lever|y|string|杠杆||
side|y|string|方向||
maxOpenAmount|y|string|最大可开张数||
lever|y|string|杠杆||
initOpenMarginRate|y|string|初始保证金率||

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;



### 设置杠杆

#### POST /api/v1/perpetual/position/{contractCode}/lever

#### 请求参数：

##### 路径参数

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
contractCode|y|string|合约code||

##### Query

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
AccessKeyId|y|string|访问key||
SignatureVersion|y|string|版本||
SignatureMethod|y|string|签名方法||HmacSHA256
Signature|y|string|签名||
Timestamp|y|string|时间戳||

##### Body(json)

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
type|y|int|杠杆类型||全仓:0,逐仓:1
shortLever|y|int|做空杠杆||
longLever|y|string|做多杠杆||

```json
{
    "code":200,
    "data":
    {
        "shortLever":26,
        "type":1,
        "longLever": 10
    },
    "msg":"success"
}
```

#### 返回：

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
lever|y|string|杠杆||

&nbsp;

&nbsp;

&nbsp;

