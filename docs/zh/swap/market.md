---
sort: 3 # follow a certain sequence of letters or numbers
---
# 行情接口

&nbsp;

### 可用合约列表

#### GET /api/v1/perpetual/public

#### 返回：

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
code|y|int|状态，200：成功||
msg|y|string|提示||
data|y|object|合约信息||

```json
{
    "code": 200,
    "msg": "success",
    "data": [
        {
            "amount24": "3848",
            "base": "btc",
            "code": "btcusd",
            "direction": 1,
            "env": 1,
            "fluctuation": "-10.04",
            "fund": "0.00375",
            "high": "9100",
            "indexPrice": "7913.84",
            "low": "8100",
            "markPrice": "7918.29",
            "maxLever": 100,
            "minQuoteDigit": 2,
            "minTradeDigit": 8,
            "price": "8100",
            "quote": "usd",
            "size24": "4.39717319",
            "totalPosition": "1830",
            "unitAmount": 10
        }
    ],
}
```



##### 合约信息返回：

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
code|y|string|合约code||
base|y|string|基础货币名,如btc、usdt||
quote|y|string|计价货币名，usd,usdt||
direction|y|string|方向 0:正向合约,1:反向合约||
minTradeDigit|y|string|基础货币最小交易小数位||
minQuoteDigit|y|string|计价货币最小交易小数位||
price|y|string|最新价||
quote|y|string|涨跌幅||
fluctuation|y|string|涨跌幅||
high|y|string|最高价||
low|y|string|最低价||
amount24|y|string|24小时成交张数||
size24|y|string|24小时成交价值||
totalPosition|y|string|最低价持仓量||
fund|y|string|资金费率||
markPrice|y|string|标记价格||
indexPrice|y|string|指数价格||
unitAmount|y|string|一张合约对应的quote面值,默认1||
env|y|string|是否测试盘 0:线上盘,1:测试盘||
maxLever|y|string|最大杠杆||

&nbsp;

&nbsp;

&nbsp;

&nbsp;


### K线

#### GET /api/v1/perpetual/public/{contractCode}/candles

#### 请求参数：

##### 路径参数

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
contractCode|y|string|合约code||

##### Query

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
kline|y|string|k线类型||1min,3min,5min,15min,30min,1hour,2hour,4hour,6hour,12hour,day,week
since|n|int|时间戳,默认值0||
size|n|int|k线数量||

#### 返回：

```json
{
    "code":0,
    "data":[
        [
            1543405500000,//时间
            "100",//最低
            "100",//最高
            "100",//开盘价
            "100",//收盘价
            "0"//成交量
        ]
    ],
    "msg":"success"
}
```

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
code|y|int|状态，200：成功||
msg|y|string|提示||
data|y|object|||


&nbsp;

&nbsp;

&nbsp;
&nbsp;

&nbsp;

&nbsp;


### 深度信息

#### GET /api/v1/perpetual/public/products/{contractCode}/orderbook

##### 路径参数

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
contractCode|y|string|合约code||

&nbsp;

```json
{
    "asks": [
      //卖一
        [
            "9721.47",  //价格
            "225",      //张数
            "225"       //总张数
        ]
    ],
    "bids": [
      //买一
        [
            "9720", 
            "480",
            "480"
        ]
    ]
}
```

#### 返回：

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
asks|y|object|卖盘||
bids|y|object|买盘||


&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;
&nbsp;

&nbsp;

&nbsp;

### 最新交易数据

#### GET /api/v1/perpetual/public/{contractCode}/fills

#### 请求参数：

##### 路径参数

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
contractCode|y|string|合约code||

```json
{
    "code": 200,
    "data": [
        [
            "9695.28",  //成交价格
            "496",      //张数
            "long",     //方向
            1582269058972, //时间
            9916897     //成交id
        ]
    ],
    "msg": "success"
}
```

#### 返回：

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
code|y|string|状态码||
data|y|object|返回结果||
msg|y|string|消息||


&nbsp;
&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

### 资金费用历史

#### GET /api/v1/perpetual/public/{contractCode}/fee-rate

##### 路径参数

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
contractCode|y|string|合约code||
page|n|int|页码||
pageSize|n|int|大小||

&nbsp;

#### 返回：

```json
{
    "code":200,
    "data":
    {
            "amount24":830768400,
            "contractCode":"etcusd",
            "createdDate":1546603201000,
            "feeRate":-0.00375,
            "id":5,
            "insuranceSize":0,
            "modifyDate":1546603201000,
            "size24":8307684,
            "timeIndex":1546603201000,
            "userPositionAmount":198000000
    },
    "msg":"success"
}
```

&nbsp;

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
amount24|y|string|24小时成交量||
contractCode|y|string|合约code||
createdDate|y|string|创建时间||
feeRate|y|string|资金费率||
id|y|string|主键id||
insuranceSize|y|string|风险准备金||
modifyDate|y|string|修改时间||
size24|y|string|24小时成交价值||
timeIndex|y|string|生成当前数据的时间||
userPositionAmount|y|string|持仓总量||

&nbsp;

&nbsp;

&nbsp;
