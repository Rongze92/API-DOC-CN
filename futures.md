# 合约交易

## 公共

### 安全类型: [None](general-info.md#jie-kou-jian-quan-lei-xing)

公共下方的接口不需要API-key或者签名就能自由访问

{% swagger baseUrl="https://futuresopenapi.xxx.com" path="/fapi/v1/ping" method="get" summary=" 测试连接" %}
{% swagger-description %}
&#x20;测试REST API的连通性
{% endswagger-description %}

{% swagger-response status="200" description=" 连接正常" %}
```
{}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://futuresopenapi.xxx.com" path="/fapi/v1/time" method="get" summary="获取服务器时间" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200" description="" %}
```
{
    "serverTime":1607702400000,
    "timezone":中国标准时间
}
```
{% endswagger-response %}
{% endswagger %}

#### Response:

| 名称         | 类型     | 例子            | 描述     |
| ---------- | ------ | ------------- | ------ |
| serverTime | long   | 1607702400000 | 服务器时间戳 |
| timezone   | string | 中国标准时间        | 服务器时区  |

{% swagger baseUrl="https://futuresopenapi.xxx.com" path="/fapi/v1/contracts" method="get" summary="合约列表" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200" description="" %}
```
[
    {
        "symbol": "H-HT-USDT",
        "pricePrecision": 8,
        "side": 1,
        "maxMarketVolume": 100000,
        "multiplier": 6,
        "minOrderVolume": 1,
        "maxMarketMoney": 10000000,
        "type": "H",
        "maxLimitVolume": 1000000,
        "maxValidOrder": 20,
        "multiplierCoin": "HT",
        "minOrderMoney": 0.001,
        "maxLimitMoney": 1000000,
        "status": 1
    }
]
```
{% endswagger-response %}
{% endswagger %}

#### Response:

| 名称              | 类型     | 例子           | 描述                           |
| --------------- | ------ | ------------ | ---------------------------- |
| symbol          | string | `E-BTC-USDT` | 合约名称                         |
| status          | number | `1`          | 合约状态（0：不可交易，1：可交易            |
| type            | string | `S`          | 合约类型 (E:永续合约，S:模拟合约，其他为混合合约) |
| side            | number | `1`          | 合约方向 (0: 反向，1：正向)            |
| multiplier      | number | `0.5`        | 合约面值                         |
| multiplierCoin  | string | `BTC`        | 合约面值单位                       |
| pricePrecision  | number | `4`          | 价格精度                         |
| minOrderVolume  | number | `10`         | 最小下单量                        |
| minOrderMoney   | number | `10`         | 最小下单金额                       |
| maxMarketVolume | number | `100000`     | 市价单最大下单数量                    |
| maxMarketMoney  | number | `100000`     | 市价最大下单金额                     |
| maxLimitVolume  | number | `100000`     | 限价单最大下单数量                    |
| maxValidOrder   | number | `100000`     | 最大有效委托的订单数量                  |

## 行情相关

### 安全类型: [None](general-info.md#jie-kou-jian-quan-lei-xing)

行情下方的接口不需要API-Key或者签名就能自由访问

{% swagger baseUrl="https://futuresopenapi.xxx.com" path="/fapi/v1/depth" method="get" summary=" 订单薄" %}
{% swagger-description %}
&#x20;市场订单薄深度信息
{% endswagger-description %}

{% swagger-parameter in="query" name="limit" type="integer" %}
&#x20;默认100; 最大100
{% endswagger-parameter %}

{% swagger-parameter in="query" name="contractName" type="string" %}
&#x20;合约合约名称 如 E-BTC-USDT
{% endswagger-parameter %}

{% swagger-response status="200" description=" 成功获取深度信息" %}
```java
{
  "bids": [
    [
      "3.90000000",   // 价格
      "431.00000000"  // 数量
    ],
    [
      "4.00000000",
      "431.00000000"
    ]
  ],
  "asks": [
    [
      "4.00000200",  // 价格
      "12.00000000"  // 数量
    ],
    [
      "5.10000000",
      "28.00000000"
    ]
  ]
}
```
{% endswagger-response %}
{% endswagger %}

#### Response:

| 名称   | 类型   | 例子              | 描述                         |
| ---- | ---- | --------------- | -------------------------- |
| time | long | `1595563624731` | 当前时间(Unix Timestamp, 毫秒ms) |
| bids | list | 如下              | 订单薄买盘信息                    |
| asks | list | 如下              | 订单薄卖盘信息                    |

bids和asks所对应的信息代表了订单薄的所有价格以及价格对应的数量的信息, 由最优价格从上倒下排列

| 名称  | 类型    | 例子      | 描述        |
| --- | ----- | ------- | --------- |
| ' ' | float | `131.1` | 价格        |
| ' ' | float | `2.3`   | 当前价格对应的数量 |

{% swagger baseUrl="https://futuersopenapi.xxx.com" path="/fapi/v1/ticker" method="get" summary=" 行情ticker" %}
{% swagger-description %}
24小时价格变化数据
{% endswagger-description %}

{% swagger-parameter in="query" name="contractName" type="string" %}
&#x20;合约名称 如 E-BTC-USDT
{% endswagger-parameter %}

{% swagger-response status="200" description=" 成功获取ticker信息" %}
```java
{
    "high": "9279.0301",
    "vol": "1302",
    "last": "9200",
    "low": "9279.0301",
    "rose": "0",
    "time": 1595563624731
}
```
{% endswagger-response %}
{% endswagger %}

#### Response:

| 名称   | 类型     | 例子              | 描述  |
| ---- | ------ | --------------- | --- |
| time | long   | `1595563624731` | 时间戳 |
| high | float  | `9900`          | 最高价 |
| low  | float  | `8800.34`       | 最低价 |
| last | float  | `8900`          | 最新价 |
| vol  | float  | `4999`          | 交易量 |
| rose | string | +0.5            | 涨跌幅 |

{% swagger baseUrl="https://futuersopenapi.xxx.com" path="/fapi/v1/index" method="get" summary=" 获取指数/标记价格" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="contractName" type="string" %}
&#x20;合约名称 如 E-BTC-USDT
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="string" %}
&#x20;默认100; 最大1000
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```java
{
    "markPrice": 581.5,
    "indexPrice": 646.3933333333333,
    "lastFundingRate": 0.001,
    "contractName": "E-ETH-USDT",
    "time": 1608273554063
}
```
{% endswagger-response %}
{% endswagger %}

#### **Response:**

| 名称                | 类型     | 例子           | 描述     |
| ----------------- | ------ | ------------ | ------ |
| `indexPrice`      | float  | `0.055`      | 指数价格   |
| `markPrice`       | float  | `0.0578`     | 标记价格   |
| `contractName`    | string | `E-BTC-USDT` | 合约名称   |
| `lastFundingRate` | float  | `0.123`      | 本期资金费率 |

{% swagger baseUrl="https://futuresopenapi.xxx.com" path="/fapi/v1/klines" method="get" summary="K线/蜡烛图数据" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="contractName" type="string" %}
&#x20;合约名称 如 E-BTC-USDT
{% endswagger-parameter %}

{% swagger-parameter in="query" name="interval" type="string" %}
&#x20;k线图区间, 可识别发送的值为： `1min`,`5min`,`15min`,`30min`,`1h`,`1day`,`1week`,`1month`（min=分钟，h=小时,day=天，week=星期，month=月）
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="integer" %}
&#x20;默认100; 最大300
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```java
[
    {
        "high": "6228.77",
        "vol": "111",
        "low": "6228.77",
        "idx": 1594640340,
        "close": "6228.77",
        "open": "6228.77"
    },
    {
        "high": "6228.77",
        "vol": "222",
        "low": "6228.77",
        "idx": 1587632160,
        "close": "6228.77",
        "open": "6228.77"
    },
    {
        "high": "6228.77",
        "vol": "333",
        "low": "6228.77",
        "idx": 1587632100,
        "close": "6228.77",
        "open": "6228.77"
    }
]
```
{% endswagger-response %}
{% endswagger %}

#### **Response:**

| 名称      | 类型    | 例子              | 描述           |
| ------- | ----- | --------------- | ------------ |
| `idx`   | long  | `1538728740000` | 开始时间戳，毫秒（ms） |
| `open`  | float | `36.00000`      | 开盘价          |
| `close` | float | `33.00000`      | 收盘价          |
| `high`  | float | `36.00000`      | 最高价          |
| `low`   | float | `30.00000`      | 最低价          |
| `vol`   | float | `2456.111`      | 成交量          |

## 交易相关

### 安全类型: [TRADE](general-info.md#jie-kou-jian-quan-lei-xing)

交易下方的接口都需要[签名和API-key验证](general-info.md#xu-yao-qian-ming-de-jie-kou-trade-yu-userdata)

{% swagger baseUrl="https://futuresopenapi.xxx.com" path="/fapi/v1/order" method="post" summary="创建订单" %}
{% swagger-description %}
创建单个新订单
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-TS" type="string" %}
时间戳
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" %}
您的API-KEY
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" %}
签名
{% endswagger-parameter %}

{% swagger-parameter in="body" name="volume" type="number" %}
下单张数, <mark style="color:red;">市价开仓时这里单位是价值</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="price" type="number" %}
下单价格
{% endswagger-parameter %}

{% swagger-parameter in="body" name="contractName" type="string" %}
合约名称 如 `E-BTC-USDT`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="string" %}
订单类型, `LIMIT/MARKET`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="side" type="string" %}
买卖方向, `BUY/SELL`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="open" type="string" %}
开平仓方向, `OPEN/CLOSE`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="positionType" type="number" %}
持仓类型, `1:全仓/2:逐仓`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="clientOrderId" type="string" %}
客户端下单标识, 长度小于32位的字符串
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timeInForce" type="string" %}
`IOC, FOK, POST_ONLY`
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```java
{
    "orderId": 256609229205684228
}
```
{% endswagger-response %}
{% endswagger %}

#### Response:

| 名称      | 类型     | 例子                   | 描述   |
| ------- | ------ | -------------------- | ---- |
| orderId | string | `256609229205684228` | 订单ID |

{% swagger method="post" path="/conditionOrder" baseUrl="https://futuresopenapi.xxx.com/fapi/v1" summary="创建条件单" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-TS" type="string" %}
时间戳
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" %}
您的API-KEY
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" %}
签名
{% endswagger-parameter %}

{% swagger-parameter in="body" name="volume" type="number" %}
&#x20;下单数量, <mark style="color:red;">市价开仓时这里单位是价值</mark>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="price" type="number" %}
下单价格
{% endswagger-parameter %}

{% swagger-parameter in="body" name="contractName" type="string" %}
合约名称 如 `E-BTC-USDT`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="string" %}
订单类型, `LIMIT/MARKET`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="side" type="string" %}
买卖方向, `BUY/SELL`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="open" type="string" %}
开平仓方向, `OPEN/CLOSE`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="positionType" type="number" %}
持仓类型, `1:全仓/2:逐仓`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="clientOrderId" type="string" %}
客户端下单标识, 长度小于32位的字符串
{% endswagger-parameter %}

{% swagger-parameter in="body" name="triggerPrice" type="string" %}
触发价
{% endswagger-parameter %}

{% swagger-parameter in="body" name="triggerType	" type="string" %}
条件单类型，`1:止损/2:止盈/3:追涨/4杀跌`
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "orderId": 256609229205684228
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://futuresopenapi.xxx.com" path="/fapi/v1/cancel" method="post" summary=" 取消订单" %}
{% swagger-description %}
&#x20;**限速规则: 20次/2s**
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" %}
&#x20;签名
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" %}
&#x20;您的API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" %}
&#x20;时间戳
{% endswagger-parameter %}

{% swagger-parameter in="body" name="contractName" type="string" %}
&#x20;合约名称如 `E-BTC-USDT`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="orderId" type="string" %}
&#x20;订单ID
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```java
{
    "orderId": 256609229205684228
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://futuresopenapi.xxx.com" path="/fapi/v1/order" method="get" summary="订单详情" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="contractName" required="true" type="string" %}
合约名称
{% endswagger-parameter %}

{% swagger-parameter in="query" name="orderId" required="true" type="string" %}
订单ID&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="query" name="clientOrderId" type="string" %}
客户端唯一标识
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
[
    {
       "side": "BUY",
       "executedQty": 0,
       "orderId": 259396989397942275,
       "price": 10000.0000000000000000,
       "origQty": 1.0000000000000000,
       "avgPrice": 0E-8,
       "transactTime": "1607702400000",
       "action": "OPEN",
       "contractName": "E-BTC-USDT",
       "type": "LIMIT",
       "status": "INIT"
    }
]


```
{% endswagger-response %}
{% endswagger %}

#### Response:

| 名称             | 类型     | 例子                   | 描述                                                                                                    |
| -------------- | ------ | -------------------- | ----------------------------------------------------------------------------------------------------- |
| `orderId`      | long   | `150695552109032492` | 订单ID（系统生成                                                                                             |
| `contractName` | string | `E-BTC-USDT`         | 合约名称                                                                                                  |
| `price`        | float  | `10.5`               | 委托价格                                                                                                  |
| `origQty`      | float  | `10.5`               | 委托数量                                                                                                  |
| `executedQty`  | float  | `10.1`               | 成交数量                                                                                                  |
| `avgPrice`     | float  | `10.5`               | 成交均价                                                                                                  |
| `symbol`       | string | `BHTUSDT`            | 币对名称                                                                                                  |
| `status`       | string | `NEW`                | 订单状态。可能出现的值为：`NEW`(新订单，无成交)、`PARTIALLY_FILLED`（部分成交）、`FILLED`（全部成交）、`CANCELED`（已取消）和`REJECTED`（订单被拒绝） |
| `side`         | string | `NEW`                | 订单方向。可能出现的值只能为：BUY（买入做多） 和 SELL（卖出做空）                                                                 |
| `action`       | string | `OPEN`               | `OPEN/CLOSE`                                                                                          |
| `transactTime` | long   | `1607702400000`      | 订单创建时间                                                                                                |

{% swagger baseUrl="https://futuresopenapi.xxx.com" path="/fapi/v1/openOrders" method="get" summary=" 当前订单" %}
{% swagger-description %}
&#x20;**限速规则:** \
**获取当前合约, 该用户的当前委托**
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" %}
&#x20;签名
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" %}
&#x20;您的API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="string" %}
&#x20;时间戳
{% endswagger-parameter %}

{% swagger-parameter in="query" name="contractName" type="string" %}
&#x20;合约名称 `E-BTC-USDT`
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```java
[
    {
       "side": "BUY",
       "executedQty": 0,
       "orderId": 259396989397942275,
       "price": 10000.0000000000000000,
       "origQty": 1.0000000000000000,
       "avgPrice": 0E-8,
       "transactTime": "1607702400000",
       "action": "OPEN",
       "contractName": "E-BTC-USDT",
       "type": "LIMIT",
       "status": "INIT"
    }
]

```
{% endswagger-response %}
{% endswagger %}

#### **Response:**

| 名称             | 类型     | 例子                   | 描述                                                                                                     |
| -------------- | ------ | -------------------- | ------------------------------------------------------------------------------------------------------ |
| `orderId`      | long   | `150695552109032492` | 订单ID（系统生成）                                                                                             |
| `contractName` | string | `E-BTC-USDT`         | 合约名称                                                                                                   |
| `price`        | float  | `4765.29`            | 订单价格                                                                                                   |
| `origQty`      | float  | `1.01`               | 订单数量                                                                                                   |
| `executedQty`  | float  | `1.01`               | 已经成交订单数量                                                                                               |
| `avgPrice`     | float  | `4754.24`            | 订单已经成交的平均价格                                                                                            |
| `type`         | string | `LIMIT`              | 订单类型。可能出现的值只能为:`LIMIT`(限价)和`MARKET`（市价）                                                                |
| `side`         | string | `BUY`                | 订单方向。可能出现的值只能为：`BUY`（买入做多） 和 `SELL`（卖出做空）                                                              |
| `status`       | string | `NEW`                | 订单状态。可能出现的值为：`NEW`(新订单，无成交)、`PARTIALLY_FILLED`（部分成交）、`FILLED`（全部成交）、`CANCELED`（已取消）和`REJECTED`（订单被拒绝）. |
| `action`       | string | `OPEN`               | `OPEN/CLOSE`                                                                                           |
| `transactTime` | long   | `1607702400000`      | 订单创建时间,                                                                                                |

{% swagger method="post" path="/fapi/v1/orderHistorical" baseUrl="https://futuresopenapi.xxx.com" summary="历史委托" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" %}
签名
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" %}
您的API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="string" %}
时间戳
{% endswagger-parameter %}

{% swagger-parameter in="body" name="contractName" type="string" %}
合约名称 `E-BTC-USDT`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="limit" type="string" %}
分页条数, 默认100; 最大1000
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fromId" type="long" %}
从这条记录开始检索
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
[
    {
        "side":"BUY",
        "clientId":"0",
        "ctimeMs":1632903411000,
        "positionType":2,
        "orderId":777293886968070157,
        "avgPrice":41000,
        "openOrClose":"OPEN",
        "leverageLevel":26,
        "type":4,
        "closeTakerFeeRate":0.00065,
        "volume":2,
        "openMakerFeeRate":0.00025,
        "dealVolume":1,
        "price":41000,
        "closeMakerFeeRate":0.00025,
        "contractId":1,
        "ctime":"2021-09-29T16:16:51",
        "contractName":"E-BTC-USDT",
        "openTakerFeeRate":0.00065,
        "dealMoney":4.1,
        "status":4
    }
]
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/fapi/v1/profitHistorical" baseUrl="https://futuresopenapi.xxx.com" summary="盈亏记录" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" %}
签名
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" %}
您的API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="string" %}
时间戳
{% endswagger-parameter %}

{% swagger-parameter in="body" name="contractName" type="string" %}
合约名称 `E-BTC-USDT`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="limit" type="string" %}
分页条数, 默认100; 最大1000
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fromId" type="long" %}
从这条记录开始检索
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
[
    {
        "side":"SELL",
        "positionType":2,
        "tradeFee":-5.23575,
        "realizedAmount":0,
        "leverageLevel":26,
        "openPrice":44500,
        "settleProfit":0,
        "mtime":1632882739000,
        "shareAmount":0,
        "openEndPrice":44500,
        "closeProfit":-45,
        "volume":900,
        "contractId":1,
        "historyRealizedAmount":-50.23575,
        "ctime":1632882691000,
        "id":8764,
        "capitalFee":0
    }
]
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://futuresopenapi.xxx.com" path="/fapi/v1/myTrades" method="get" summary=" 交易记录" %}
{% swagger-description %}
&#x20;**限速规则: 20次/2s**
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" %}
&#x20;签名
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" %}
&#x20;您的API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" %}
&#x20;时间戳
{% endswagger-parameter %}

{% swagger-parameter in="query" name="contractName" type="string" %}
&#x20;合约名称 如 E-BTC-USDT
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="string" %}
&#x20;分页条数, 默认100; 最大1000
{% endswagger-parameter %}

{% swagger-parameter in="query" name="fromId" type="long" %}
&#x20;从这个tradeId开始检索
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```java
[
  {
    "symbol": "ETHBTC",
    "id": 100211,
    "bidId": 150695552109032492,
    "askId": 150695552109032493,
    "price": "4.00000100",
    "qty": "12.00000000",
    "time": 1499865549590,
    "isBuyer": true,
    "isMaker": false,
    "fee":"0.001"
  },...
]
```
{% endswagger-response %}
{% endswagger %}

#### **Response:**

| 名称           | 类型      | 例子                 | 描述                     |
| ------------ | ------- | ------------------ | ---------------------- |
| symbol       | string  | ETHBTC             | 币种名称(交易对)              |
| tradeId      | number  | 28457              | 交易ID                   |
| bidId        | long    | 150695552109032492 | 买方订单ID                 |
| askId        | long    | 150695552109032493 | 卖方订单ID                 |
| bidUserId    | integer | 10024              | 买方用户ID                 |
| askUserId    | integer | 10025              | 卖方用户ID                 |
| price        | float   | 4.01               | 成交价格                   |
| qty          | float   | 12                 | 交易数量                   |
| amount       | float   | 5.38               | 成交金额                   |
| time         | number  | 1499865549590      | 交易时间戳                  |
| fee          | number  | 0.001              | 交易手续费                  |
| side         | string  | buy                | 当前订单方向 BUY 买入, SELL 卖出 |
| contractName | string  | E-BTC-USDT         | 合约名称                   |
| isMaker      | boolean | true               | 是否是maker               |
| isBuyer      | boolean | true               | 是否买方                   |

## 账户

### 安全类型:[ USER\_DATA](general-info.md#jie-kou-jian-quan-lei-xing)

账户下方的接口都需要[签名和API-key验证](general-info.md#xu-yao-qian-ming-de-jie-kou-trade-yu-userdata)

{% swagger baseUrl="https://futuresopenapi.xxx.com" path="/fapi/v1/account" method="get" summary=" 账户信息" %}
{% swagger-description %}
&#x20;**限速规则: 20次/2s**
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" %}
&#x20;签名
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" %}
&#x20;您的API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" %}
&#x20;时间戳
{% endswagger-parameter %}

{% swagger-response status="200" description=" 获取账户信息成功" %}
```java
{
    "account": [
        {
            "marginCoin": "USDT",
            "accountNormal": 999.5606,
            "accountLock": 23799.5017,
            "partPositionNormal": 9110.7294,
            "totalPositionNormal": 0,
            "achievedAmount": 4156.5072,
            "unrealizedAmount": 650.6385,
            "totalMarginRate": 0,
            "totalEquity": 99964804.560,
            "partEquity": 13917.8753,
            "totalCost": 0,
            "sumMarginRate": 873.4608,
            "positionVos": [
                {
                    "contractId": 1,
                    "contractName": "E-BTC-USDT",
                    "contractSymbol": "BTC-USDT",
                    "positions": [
                        {
                            "id": 13603,
                            "uid": 10023,
                            "contractId": 1,
                            "positionType": 2,
                            "side": "BUY",
                            "volume": 69642.0,
                            "openPrice": 11840.2394,
                            "avgPrice": 11840.3095,
                            "closePrice": 12155.3005,
                            "leverageLevel": 24,
                            "holdAmount": 7014.2111,
                            "closeVolume": 40502.0,
                            "pendingCloseVolume": 0,
                            "realizedAmount": 8115.9125,
                            "historyRealizedAmount": 1865.3985,
                            "tradeFee": -432.0072,
                            "capitalFee": 2891.2281,
                            "closeProfit": 8117.6903,
                            "shareAmount": 0.1112,
                            "freezeLock": 0,
                            "status": 1,
                            "ctime": "2020-12-11T17:42:10",
                            "mtime": "2020-12-18T20:35:43",
                            "brokerId": 21,
                            "marginRate": 0.2097,
                            "reducePrice": 9740.8083,
                            "returnRate": 0.3086,
                            "unRealizedAmount": 2164.5289,
                            "openRealizedAmount": 2165.0173,
                            "positionBalance": 82458.2839,
                            "settleProfit": 0.4883,
                            "indexPrice": 12151.1175,
                            "keepRate": 0.005,
                            "maxFeeRate": 0.0025
                        }
                    ]
                }
            ]
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

#### Response:

| 名称        | 类型   | 描述   |
| --------- | ---- | ---- |
| `account` | `[]` | 余额集合 |

`account` field:

| 名称                  | 类型     | 例子    | 描述         |
| ------------------- | ------ | ----- | ---------- |
| marginCoin          | string | USDT  | 保证金币种      |
| accountNormal       | float  | 10.05 | 余额帐户       |
| accountLock         | float  | 10.07 | 保证金冻结帐户    |
| partPositionNormal  | float  | 10.07 | 逐仓保证金余额    |
| totalPositionNormal | float  | 10.07 | 全仓占用的初始保证金 |
| achievedAmount      | float  | 10.07 | 已实现盈亏      |
| unrealizedAmount    | float  | 10.05 | 未实现盈亏      |
| totalMarginRate     | float  | 10.05 | 全仓保证金率     |
| totalEquity         | float  | 10.07 | 全仓权益       |
| partEquity          | float  | 10.07 | 逐仓权益       |
| totalCost           | float  | 10.07 | 全仓占用的成本    |
| sumMarginRate       | float  | 10.07 | 全账户的保证金率   |
| positionVos         | \[ ]   |       | 仓位合约记录     |

`positionVos` field:

| 名称             | 类型      | 例子         | 描述   |
| -------------- | ------- | ---------- | ---- |
| contractId     | integer | 2          | 合约id |
| contractName   | string  | E-BTC-USDT | 合约名称 |
| contractSymbol | string  | BTC-USDT   | 合约币对 |
| positions      | \[ ]    |            | 仓位明细 |

`positions` field:

| 名称                    | 类型      | 例子    | 描述                             |
| --------------------- | ------- | ----- | ------------------------------ |
| id                    | integer | 2     | 仓位id                           |
| uid                   | integer | 10023 | 用户ID                           |
| positionType          | integer | 1     | 持仓类型(1: 全仓，2: 逐仓)              |
| side                  | string  | SELL  | 持仓方向( BUY: 多仓, SELL: 空仓        |
| volume                | float   | 1.05  | 持仓数量                           |
| openPrice             | float   | 1.05  | 开仓价格                           |
| avgPrice              | float   | 1.05  | 持仓均价                           |
| closePrice            | float   | 1.05  | 平仓均价                           |
| leverageLevel         | float   | 1.05  | 杠杆倍数                           |
| holdAmount            | float   | 1.05  | 持仓保证金                          |
| closeVolume           | float   | 1.05  | 已平仓数量                          |
| pendingCloseVolume    | float   | 1.05  | 已挂出平仓单的数量                      |
| realizedAmount        | float   | 1.05  | 已实现盈亏                          |
| historyRealizedAmount | float   | 1.05  | 历史累计已实现盈亏                      |
| tradeFee              | float   | 1.05  | 交易手续费                          |
| capitalFee            | float   | 1.05  | 资金费用                           |
| closeProfit           | float   | 1.05  | 平仓盈亏                           |
| shareAmount           | float   | 1.05  | 分摊金额                           |
| freezeLock            | integer | 0     | 持仓冻结状态 (0: 正常，1: 爆仓冻结，2: 交割冻结) |
| status                | integer | 0     | 仓位有效性(0: 无效 ，1：有效)             |
| ctime                 | time    |       | 创建时间                           |
| mtime                 | time    |       | 更新时间                           |
| brokerId              | integer | 1023  | 商户id                           |
| lockTime              | time    |       | 爆仓锁仓时间                         |
| marginRate            | float   | 1.05  | 保证金率                           |
| reducePrice           | float   | 1.05  | 强减价格                           |
| returnRate            | float   | 1.05  | 回报率(收益率)                       |
| unRealizedAmount      | float   | 1.05  | 未实现盈亏                          |
| openRealizedAmount    | float   | 1.05  | 开仓未实现盈亏                        |
| positionBalance       | float   | 1.05  | 仓位价值                           |
| indexPrice            | float   | 1.05  | 最新标记价格                         |
| keepRate              | float   | 1.05  | 阶梯最低维持保证金率                     |
| maxFeeRate            | float   | 1.05  | 平仓最大手续费率                       |

