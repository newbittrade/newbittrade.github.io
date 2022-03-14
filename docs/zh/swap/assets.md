---
sort: 4 # follow a certain sequence of letters or numbers
---
# 资产接口

&nbsp;

### 我的资产

#### GET /api/v1/perpetual/account/assets/{contractCode}

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
    "nextRewardTimestamp": 86400000,
    "accountRights": "211.73425366",
    "realizedSurplus": "-1996.67028101",
    "unRealizedSurplus": "0",
    "orderMargin": "111.32734888",
    "positionMargin": "55.30721388",
    "env": 0,
    "currencyCode": "usdt",
    "availableMargin": "45.09969088"
}
```

#### 返回：

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
currencyCode|y|string|币种||
env|y|int|是否测试币 0:线上币,1:测试币||
availableMargin|y|string|可用保证金||
realizedSurplus|y|string|已实现盈亏||
orderMargin|y|string|委托保证金||
positionMargin|y|string|仓位保证金||
unRealizedSurplus|y|string|未实现盈亏||
accountRights|y|string|账户权益||

&nbsp;

&nbsp;

&nbsp;


### 资产列表

#### GET /api/v1/perpetual/account/assets

#### 请求参数：

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
    "availableBalance": "9875.254090",
    "currencyCode": "USDT",
    "env": "0",
    "frozenBalance": "0.000000",
    "orderMargin": "15.823570",
    "positionMargin": "89.352729",
    "positionAccountRights": "10456.925390",
    "realizedSurplus": "583.993103",
    "unRealizedSurplus": "-15.505000"
  }
]
```

#### 返回：

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
availableBalance|y|string|可用余额||
currencyCode|y|string|币种||
env|y|int|是否测试币 0:线上币,1:测试币||
frozenBalance|y|string|可用冻结（出现在划转审核）||
orderMargin|y|string|订单保证金||
positionMargin|y|string|仓位保证金||
positionAccountRights|y|string|账户权益||
realizedSurplus|y|string|已实现盈亏||
unRealizedSurplus|y|string|未实现盈亏||

&nbsp;

&nbsp;

&nbsp;


### 成交记录
#### GET /api/v1/perpetual/bills/deal-record

#### 请求参数：

##### Query

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
AccessKeyId|y|string|访问key||
SignatureVersion|y|string|版本||
SignatureMethod|y|string|签名方法||HmacSHA256
Signature|y|string|签名||
Timestamp|y|string|时间戳||
startDate|n|long|开始时间||
endDate|n|long|结束时间||
contractCode|n|string|合约code||
page|n|integer|页数|1|
pageSize|n|integer|每页数量|20|
startId|n|long|开始id||
endId|n|long|结束id||



```json
{
    "code": 200,
    "data": {
        "data": [
            {
                "amount": "6",
                "contractCode": "btcusdt",
                "createDate": "2021-11-14 20:52:03",
                "currencyCode": "usdt",
                "dealType": 1,
                "detailSide": "close_long",
                "fee": "1.3579752900000000",
                "id": "666746374653476864",
                "makerTaker": "maker",
                "orderId": 125090120907072,
                "price": "64665.4900000000000000",
                "profit": "0.9555748956901509",
                "refOrderId": 125090122965326,
                "size": "3879.9294000000000000",
                "userId": "2000011"
            }
        ],
        "pageNum": 1,
        "pageSize": 20,
        "totalCount": 112677
    },
    "msg": "success"
}

```

#### 返回：

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
amount|y|string|成交数量||
contractCode|y|string|合约code||
createDate|y|string|创建时间||
currencyCode|y|string|币种||
dealType|y|string|成交类型，1：自成交，2：与其他用户成交||
detailSide|y|string|开平方向||
fee|y|string|手续费||
id|y|long|成交记录id||
makerTaker|y|string|maker or taker||
orderId|y|long|订单id||
price|y|string|成交价格||
profit|y|string|收益||
refOrderId|y|long|关联订单id||
size|y|string|成交价值||
userId|y|long|uid||


&nbsp;
