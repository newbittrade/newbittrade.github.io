---
sort: 5 # follow a certain sequence of letters or numbers
---
# 下单接口

&nbsp;

### 下单

#### POST /api/v1/perpetual/products/{contractCode}/order

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
type|y|string|类型||10 限价或条件单 11 市价
triggerBy|n|string|触发类型||条件单选项，如果不是条件单此字段必须为NULL，指数价格：index，标记价格：mark，最新价格：last
triggerPrice|n|string|条件单选项 触发价
side|y|string|方向||open_long 开多 open_short 开空 close_long 平多 close_short 平空
price|y|string|价格||
ioc|n|int|订单若不能立即成交则未成交的部分立即取消|0|0: 关闭，1: 开启
amount|y|int|数量||
beMaker|n|int|时间戳|0|被动委托：0:不被动委托 1:被动委托

```json
{
   "id": "1237893454356"
}
```

#### 返回：

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
id|y|long|订单id||


&nbsp;


### 批量下单

#### POST /api/v1/perpetual/products/{contractCode}/batch-order

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
		"amount": 1,
		"lang": "zh_CN",
		"platform": 1,
		"price": "2.94",
		"side": "open_long",
		"type": 10,
		"tag": 1
	}
]
```

##### Body(list-json)

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
type|y|string|类型||10 限价或条件单 11 市价
side|y|string|方向||open_long 开多 open_short 开空 close_long 平多 close_short 平空
price|y|string|价格||
amount|y|int|数量||
beMaker|n|int|时间戳|0|被动委托：0:不被动委托 1:被动委托
ioc|n|int|订单若不能立即成交则未成交的部分立即取消|0|0: 关闭，1: 开启
tag|n|string|标签||下单时用户所定义的标签，下单后返回

&nbsp;

&nbsp;


```json
[
    {
        "orderId": 80742077438016,
        "tag": "1"
    }
]
```


#### 返回(list-json)：

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
id|y|long|订单id||



&nbsp;

&nbsp;

&nbsp;


### 订单列表

#### GET /api/v1/perpetual/products/{contractCode}/list

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
        "amount": "300.0000000000000000",
        "avgPrice": "0E-16",
        "base": "",
        "contractCode": "fbtcusd",
        "contractDirection": 0,
        "createdDate": 1582225542000,
        "dealAmount": "0E-16",
        "detailSide": "open_long",
        "direction": "",
        "fee": "0E-16",
        "id": 69109290623152,
        "orderSize": "0.32258064",
        "price": "9300.0000000000000000",
        "profit": "0E-16",
        "quote": "",
        "reason": 0,
        "refConditionOrderId": 0,
        "refOrderCondition": null,
        "side": "long",
        "source": "",
        "status": 0,
        "systemType": 10,
        "triggerBy": "",
        "triggerPrice": ""
    }
]
```


#### 返回：

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
amount|y|string|数量||
avgPrice|y|string|平均成交价||
base|y|string|基础货币名,如btc、fbtc||
contractCode|y|string|是Base和Quote之间的组合 P_BTC_USDT，R_BTC_USDT||
contractDirection|y|int|合约方向 0:正向,1:反向||
createdDate|y|string|创建时间||
dealAmount|y|string|已成交数量||
detailSide|y|string|订单方向 1.开多open_long 2.开空open_short 3.平多close_long 4.平空close_short||
direction|y|string|条件单：触发方向，greater大于，less小于||
fee|y|string|该笔订单成交后交的手续费: 正表示得手续费,负表示付手续费||
id|y|long|订单id||
orderSize|y|string|订单价值||
price|y|string|委托价格||
profit|y|string|该笔订单成交后对应的盈亏: 正表示盈利,负表示亏损||
quote|y|string|计价货币名，usd,cny,usdt||
reason|y|int|该笔订单取消的理由，0是默认值，没有理由||
refConditionOrderId|y|long|条件单id||
refOrderCondition|y|object|条件单详情||
side|y|string|订单方向，long多，short空||
source|y|string|来源||
status|y|int|状态 0:等待成交 1:部分成交 2:已经成交 -1:已经撤销||
systemType|y|int|10:限价 11:市价 13:强平单 14:爆仓单 15：穿仓 16：强减||
triggerBy|y|string|条件单触发类型，指数价格：index，标记价格：mark，最新价格：last||
triggerPrice|y|string|条件单触发价格||

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;



### 撤单

#### DELETE /api/v1/perpetual/products/{contractCode}/order/{id}

#### 请求参数：

##### 路径参数

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
contractCode|y|string|合约code||
id|y|long|订单id||

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
    "msg": "success",
    "data": null
}
```

#### 返回：

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
code|y|int|状态，200：成功||
msg|y|string|提示||
data|y|object|||


&nbsp;

&nbsp;

&nbsp;




### 批量撤单

#### DELETE /api/v1/perpetual/products/{contractCode}/orders

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
    "msg": "success",
    "data": null
}
```

#### 返回：

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
code|y|int|状态，200：成功||
msg|y|string|提示||
data|y|object|||



&nbsp;

&nbsp;

&nbsp;



### 根据订单号批量撤单

#### DELETE /api/v1/perpetual/products/{contractCode}/batch-delete-order

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
	80581909355536,
	80581909355537
]

```

##### Body(list)

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
id|y|string|订单号||


```json
{
    "code": 200,
    "msg": "success",
    "data": null
}
```

#### 返回：

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
code|y|int|状态，200：成功||
msg|y|string|提示||
data|y|object|||

&nbsp;

&nbsp;

&nbsp;


### 订单详情

#### GET /api/v1/perpetual/products/{contractCode}/{id}

#### 请求参数：

##### 路径参数

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
contractCode|y|string|合约code||
id|y|long|订单id||

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
    "amount": "300.0000000000000000",
    "avgPrice": "0E-16",
    "base": "",
    "contractCode": "fbtcusd",
    "contractDirection": 0,
    "createdDate": 1582225542000,
    "dealAmount": "0E-16",
    "detailSide": "open_long",
    "direction": "",
    "fee": "0E-16",
    "id": 69109290623152,
    "orderSize": "0.32258064",
    "price": "9300.0000000000000000",
    "profit": "0E-16",
    "quote": "",
    "reason": 0,
    "refConditionOrderId": 0,
    "refOrderCondition": null,
    "side": "long",
    "source": "",
    "status": 0,
    "systemType": 10,
    "triggerBy": "",
    "triggerPrice": ""
}
```


#### 返回：

参数名称|是否必须|类型|描述|默认值|取值范围
------------- | ------------- |  ------------- | ------------- |  ------------- | -------------
amount|y|string|数量||
avgPrice|y|string|平均成交价||
base|y|string|基础货币名,如btc、fbtc||
contractCode|y|string|是Base和Quote之间的组合 P_BTC_USDT，R_BTC_USDT||
contractDirection|y|int|合约方向 0:正向,1:反向||
createdDate|y|string|创建时间||
dealAmount|y|string|已成交数量||
detailSide|y|string|订单方向 1.开多open_long 2.开空open_short 3.平多close_long 4.平空close_short||
direction|y|string|条件单：触发方向，greater大于，less小于||
fee|y|string|该笔订单成交后交的手续费: 正表示得手续费,负表示付手续费||
id|y|long|订单id||
orderSize|y|string|订单价值||
price|y|string|委托价格||
profit|y|string|该笔订单成交后对应的盈亏: 正表示盈利,负表示亏损||
quote|y|string|计价货币名，usd,cny,usdt||
reason|y|int|该笔订单取消的理由，0是默认值，没有理由||
refConditionOrderId|y|long|条件单id||
refOrderCondition|y|object|条件单详情||
side|y|string|订单方向，long多，short空||
source|y|string|来源||
status|y|int|状态 0:等待成交 1:部分成交 2:已经成交 -1:已经撤销||
systemType|y|int|10:限价 11:市价 13:强平单 14:爆仓单 15：穿仓 16：强减||
triggerBy|y|string|条件单触发类型，指数价格：index，标记价格：mark，最新价格：last||
triggerPrice|y|string|条件单触发价格||
