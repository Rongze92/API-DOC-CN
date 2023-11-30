# 币币交易

## 公共

### 安全类型: [None](general-info.md#jie-kou-jian-quan-lei-xing)

公共下方的接口不需要API-key或者签名就能自由访问

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/ping" method="get" summary=" 测试连接" %}
{% swagger-description %}
&#x20;测试REST API的连通性\
\
**Demo:**\
`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/TestConnectivity.java`
{% endswagger-description %}

{% swagger-response status="200" description=" 连接正常" %}
```
{}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/time" method="get" summary=" 服务器时间" %}
{% swagger-description %}
&#x20;服务器时间\
\
**Demo:**\
`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/CheckServerTime.java`
{% endswagger-description %}

{% swagger-response status="200" description=" 获取服务器时间成功" %}
```java
{
    "timezone": "GMT+08:00",
    "serverTime": 1595563624731
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/symbols" method="get" summary="币对列表 " %}
{% swagger-description %}
&#x20;市场支持的币对集合\
\
**Demo:**\
`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/PairsList.java`
{% endswagger-description %}

{% swagger-response status="200" description="获取币对列表成功" %}
```java
{
    "symbols": [
        {
            "quantityPrecision": 3,
            "symbol": "sccadai",
            "pricePrecision": 6,
            "baseAsset": "SCCA",
            "quoteAsset": "DAI"
        },
        {
            "quantityPrecision": 8,
            "symbol": "btcusdt",
            "pricePrecision": 2,
            "baseAsset": "BTC",
            "quoteAsset": "USDT"
        },
        {
            "quantityPrecision": 3,
            "symbol": "bchusdt",
            "pricePrecision": 2,
            "baseAsset": "BCH",
            "quoteAsset": "USDT"
        },
        {
            "quantityPrecision": 2,
            "symbol": "etcusdt",
            "pricePrecision": 2,
            "baseAsset": "ETC",
            "quoteAsset": "USDT"
        },
        {
            "quantityPrecision": 2,
            "symbol": "ltcbtc",
            "pricePrecision": 6,
            "baseAsset": "LTC",
            "quoteAsset": "BTC"
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

#### Response:

| 名称                | 类型      | 例子        | 描述     |
| ----------------- | ------- | --------- | ------ |
| symbol            | string  | `BTCUSDT` | 币对名称   |
| baseAsset         | string  | `BTC`     | base货币 |
| quoteAsset        | string  | `USDT`    | 计价货币   |
| pricePrecision    | integer | `2`       | 价格精度   |
| quantityPrecision | integer | `6`       | 数量精度   |

## 行情

### 安全类型: [None](general-info.md#jie-kou-jian-quan-lei-xing)

行情下方的接口不需要API-Key或者签名就能自由访问

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/depth" method="get" summary=" 订单薄" %}
{% swagger-description %}
&#x20;市场订单薄深度信息\
\
**Demo:**\
`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/Depth.java`
{% endswagger-description %}

{% swagger-parameter in="query" name="limit" type="integer" required="true" %}
&#x20;默认100; 最大100
{% endswagger-parameter %}

{% swagger-parameter in="query" name="symbol" type="string" required="true" %}
&#x20;币对名称 E.g. BTCUSDT
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

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/ticker" method="get" summary=" 行情ticker" %}
{% swagger-description %}
24小时价格变化数据\
\
**Demo:**\
`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/Ticker.java`
{% endswagger-description %}

{% swagger-parameter in="query" name="symbol" type="string" required="true" %}
&#x20;币对名称 E.g. `BTCUSDT`
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

| 名称   | 类型    | 例子              | 描述  |
| ---- | ----- | --------------- | --- |
| time | long  | `1595563624731` | 时间戳 |
| high | float | `9900`          | 最高价 |
| low  | float | `8800.34`       | 最低价 |
| last | float | `8900`          | 最新价 |
| vol  | float | `4999`          | 交易量 |
| open | float | `5000`          | 开盘价 |

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/trades" method="get" summary=" 最近成交" %}
{% swagger-description %}
**Demo:**\
`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/RecentTradesList.java`\

{% endswagger-description %}

{% swagger-parameter in="query" name="symbol" type="string" required="true" %}
&#x20;币对名称 E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="string" required="true" %}
&#x20;默认100; 最大1000
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```java
{
    "list":[
        {
            "price":"3.00000100",
            "qty":"11.00000000",
            "time":1499865549590,
            "side":"BUY"
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

#### **Response:**

| 名称      | 类型     | 例子              | 描述               |
| ------- | ------ | --------------- | ---------------- |
| `price` | float  | `0.055`         | 交易价格             |
| `time`  | long   | `1537797044116` | 当前Unix时间戳，毫秒(ms) |
| `qty`   | float  | `5`             | 数量（张数）           |
| `side`  | string | `BUY/SELL`      | 主动单方向            |

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/klines" method="get" summary="K线/蜡烛图数据" %}
{% swagger-description %}
**Demo:**\
`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/KlineCandlestickData.java`\

{% endswagger-description %}

{% swagger-parameter in="query" name="symbol" type="string" required="true" %}
&#x20;币对名称 E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="interval" type="string" required="true" %}
&#x20;k线图区间, 可识别发送的值为： `1min`,`5min`,`15min`,`30min`,`60min`,`1day`,`1week`,`1month`（min=分钟，h=小时,day=天，week=星期，month=月）
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="integer" required="true" %}
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

## 交易

### 安全类型: [TRADE](general-info.md#jie-kou-jian-quan-lei-xing)

交易下方的接口都需要[签名和API-key验证](general-info.md#xu-yao-qian-ming-de-jie-kou-trade-yu-userdata)

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/order" method="post" summary=" 创建新订单" %}
{% swagger-description %}
**Demo:**\
**`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/NewOrder.java`**\
\
**限速规则: 100次/2s**
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" required="true" %}
&#x20;签名
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" required="true" %}
&#x20;您的API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" required="true" %}
&#x20;时间戳
{% endswagger-parameter %}

{% swagger-parameter in="body" name="symbol" type="string" required="true" %}
&#x20;币对名称 E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="volume" type="number" required="true" %}
&#x20;订单数量
{% endswagger-parameter %}

{% swagger-parameter in="body" name="side" type="string" required="true" %}
&#x20;订单方向, `BUY/SELL`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="string" required="true" %}
&#x20;订单类型, `LIMIT/MARKET`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="price" type="number" %}
&#x20;订单价格, 对于`LIMIT`订单必须发送
{% endswagger-parameter %}

{% swagger-parameter in="body" name="newClientOrderId" type="string" required="false" %}
&#x20;客户端订单标识
{% endswagger-parameter %}

{% swagger-parameter in="body" name="recvWindow" type="integer" %}
&#x20;时间窗口
{% endswagger-parameter %}

{% swagger-response status="200" description=" 发送新订单成功" %}
```java
{
    'symbol': 'LXTUSDT', 
    'orderId': '150695552109032492', 
    'clientOrderId': '157371322565051',
    'transactTime': '1573713225668', 
    'price': '0.005452', 
    'origQty': '110', 
    'executedQty': '0', 
    'status': 'NEW',
    'type': 'LIMIT', 
    'side': 'SELL'
}
```
{% endswagger-response %}
{% endswagger %}

#### **Response:**

| 名称              | 类型      | 例子                   | 描述                                                                                                     |
| --------------- | ------- | -------------------- | ------------------------------------------------------------------------------------------------------ |
| `orderId`       | long    | `150695552109032492` | 订单ID（系统生成）                                                                                             |
| `clientOrderId` | string  | `213443`             | 订单ID（自己发送的）                                                                                            |
| `symbol`        | string  | `BTCUSDT`            | 币对名称                                                                                                   |
| `transactTime`  | integer | `1273774892913`      | 订单创建时间                                                                                                 |
| `price`         | float   | `4765.29`            | 订单价格                                                                                                   |
| `origQty`       | float   | `1.01`               | 订单数量                                                                                                   |
| `executedQty`   | float   | `1.01`               | 已经成交订单数量                                                                                               |
| `type`          | string  | `LIMIT`              | 订单类型`LIMIT`(限价)`MARKET`（市价）                                                                            |
| `side`          | string  | `BUY`                | 订单方向。可能出现的值只能为：`BUY`（买入做多） 和 `SELL`（卖出做空）                                                              |
| `status`        | string  | `NEW`                | 订单状态。可能出现的值为：`NEW`(新订单，无成交)、`PARTIALLY_FILLED`（部分成交）、`FILLED`（全部成交）、`CANCELED`（已取消）和`REJECTED`（订单被拒绝）. |

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/order/test" method="post" summary=" 创建测试订单" %}
{% swagger-description %}
**Demo:** \
**`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/TestNewOrder.java`**\
\
创建和验证新订单, 但不会送入撮合引擎
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" required="true" %}
&#x20;签名
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" required="true" %}
&#x20;您的API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" required="true" %}
&#x20;时间戳
{% endswagger-parameter %}

{% swagger-parameter in="body" name="recvWindow" type="integer" required="false" %}
&#x20;时间窗口
{% endswagger-parameter %}

{% swagger-parameter in="body" name="symbol" type="string" required="true" %}
&#x20;币对名称 E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="volume" type="number" required="true" %}
&#x20;订单数量
{% endswagger-parameter %}

{% swagger-parameter in="body" name="side" type="string" required="true" %}
&#x20;订单方向, `BUY/SELL`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="string" required="true" %}
&#x20;订单类型, `LIMIT/MARKET`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="price" type="number" %}
&#x20;订单价格, 对于`LIMIT`订单必须发送
{% endswagger-parameter %}

{% swagger-parameter in="body" name="newClientOrderId" type="string" %}
&#x20;客户端订单标识
{% endswagger-parameter %}

{% swagger-response status="200" description=" 创建测试订单成功" %}
```
{}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/batchOrders" method="post" summary=" 批量下单" %}
{% swagger-description %}
**Demo:** \
**`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/BatchOrders.java`**\
\
**限速规则: 50次/2s 一个批量最多10个订单**
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" required="true" %}
&#x20;签名
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" required="true" %}
&#x20;您的API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" required="true" %}
&#x20;时间戳
{% endswagger-parameter %}

{% swagger-parameter in="body" name="orders" type="array" required="true" %}
&#x20;批量订单信息  最多10条
{% endswagger-parameter %}

{% swagger-parameter in="body" name="symbol" type="string" required="true" %}
&#x20;币对名称 E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```java
{
    "ids": [
        165964665990709251,
        165964665990709252,
        165964665990709253
    ]
}
```
{% endswagger-response %}
{% endswagger %}

#### Resquest `orders` field:

| 名称          | 类型     | 例子             | 描述 |
| ----------- | ------ | -------------- | -- |
| `price`     | folat  | 1000           | 价格 |
| `volume`    | folat  | 20.1           | 数量 |
| `side`      | string | `BUY/SELL`     | 方向 |
| `batchType` | string | `LIMIT/MARKET` | 类型 |

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/order" method="get" summary=" 订单查询" %}
{% swagger-description %}
**Demo:**\
`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/QueryOrder.java` \
\
**限速规则: 20次/2s**
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" required="true" %}
&#x20;签名
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" required="true" %}
&#x20;您的API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" required="true" %}
&#x20;时间戳
{% endswagger-parameter %}

{% swagger-parameter in="query" name="orderId" type="string" required="true" %}
&#x20;订单id
{% endswagger-parameter %}

{% swagger-parameter in="query" name="newClientOrderId" type="string" %}
&#x20;客户端订单标识
{% endswagger-parameter %}

{% swagger-parameter in="query" name="symbol" type="string" required="true" %}
&#x20;币对名称 E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```java
{
    'orderId': '499890200602846976', 
    'clientOrderId': '157432755564968', 
    'symbol': 'BHTUSDT', 
    'price': '0.01', 
    'origQty': '50', 
    'executedQty': '0', 
    'avgPrice': '0', 
    'status': 'NEW', 
    'type': 'LIMIT', 
    'side': 'BUY', 
    'transactTime': '1574327555669'
}
```
{% endswagger-response %}
{% endswagger %}

#### **Response:**

| 名称              | 类型     | 例子                   | 描述                                                                                                     |
| --------------- | ------ | -------------------- | ------------------------------------------------------------------------------------------------------ |
| `orderId`       | long   | `150695552109032492` | 订单ID（系统生成）                                                                                             |
| `clientOrderId` | string | `213443`             | 订单ID（自己发送的）                                                                                            |
| `symbol`        | string | `BTCUSDT`            | 币对名称                                                                                                   |
| `price`         | float  | `4765.29`            | 订单价格                                                                                                   |
| `origQty`       | float  | `1.01`               | 订单数量                                                                                                   |
| `executedQty`   | float  | `1.01`               | 已经成交订单数量                                                                                               |
| `avgPrice`      | float  | `4754.24`            | 订单已经成交的平均价格                                                                                            |
| `type`          | string | `LIMIT`              | 订单类型。可能出现的值只能为:`LIMIT`(限价)和`MARKET`（市价）                                                                |
| `side`          | string | `BUY`                | 订单方向。可能出现的值只能为：`BUY`（买入做多） 和 `SELL`（卖出做空）                                                              |
| `status`        | string | `NEW`                | 订单状态。可能出现的值为：`NEW`(新订单，无成交)、`PARTIALLY_FILLED`（部分成交）、`FILLED`（全部成交）、`CANCELED`（已取消）和`REJECTED`（订单被拒绝）. |

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/cancel" method="post" summary=" 撤销订单" %}
{% swagger-description %}
**Demo:**\
`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/CancelOrder.java` \
\
**限速规则: 100次/2s**
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" required="true" %}
&#x20;签名
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" required="true" %}
&#x20;您的API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" required="true" %}
&#x20;时间戳
{% endswagger-parameter %}

{% swagger-parameter in="body" name="orderId" type="string" required="true" %}
&#x20;订单id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="newClientOrderId" type="string" %}
&#x20;客户端订单标识
{% endswagger-parameter %}

{% swagger-parameter in="body" name="symbol" type="string" required="true" %}
&#x20;币对名称 E.g. `BTCUSDT`&#x20;
{% endswagger-parameter %}

{% swagger-response status="200" description=" 撤销订单成功" %}
```java
{
    'symbol': 'BHTUSDT', 
    'clientOrderId': '0', 
    'orderId': '499890200602846976', 
    'status': 'CANCELED'
}

```
{% endswagger-response %}
{% endswagger %}

#### Response:

| 名称              | 类型     | 例子                   | 描述                                                                                                    |
| --------------- | ------ | -------------------- | ----------------------------------------------------------------------------------------------------- |
| `orderId`       | long   | `150695552109032492` | 订单ID（系统生成                                                                                             |
| `clientOrderId` | string | `213443`             | 订单ID（自己发送的）                                                                                           |
| `symbol`        | string | `BHTUSDT`            | 币对名称                                                                                                  |
| `status`        | string | `NEW`                | 订单状态。可能出现的值为：`NEW`(新订单，无成交)、`PARTIALLY_FILLED`（部分成交）、`FILLED`（全部成交）、`CANCELED`（已取消）和`REJECTED`（订单被拒绝） |

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/batchCancel" method="post" summary=" 批量撤销订单" %}
{% swagger-description %}
**Demo:**\
`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/BatchCancelOrders.java`\
\
**限速规则: 50次/2s 一次批量最多10个订单**
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" required="true" %}
&#x20;签名
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" required="true" %}
&#x20;您的API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" required="true" %}
&#x20;时间戳
{% endswagger-parameter %}

{% swagger-parameter in="body" name="symbol" type="string" required="true" %}
&#x20;币对名称 E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="orderIds" type="array" required="true" %}
&#x20;要取消的订单id集合 `[123,456]`
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```java
{
    "success": [
        165964665990709251,
        165964665990709252,
        165964665990709253
    ],
    "failed": [ //取消失败一般是因为订单不存在或订单状态已经到终态
        165964665990709250  
    ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/openOrders" method="get" summary=" 当前订单" %}
{% swagger-description %}
**Demo:**\
`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/CurrentOpenOrders.java` \
\
**限速规则: 20次/2s**
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" required="true" %}
&#x20;签名
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" required="true" %}
&#x20;您的API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" required="true" %}
&#x20;时间戳
{% endswagger-parameter %}

{% swagger-parameter in="query" name="symbol" type="string" required="true" %}
&#x20;币对名称 E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="integer" required="true" %}
&#x20;默认100; 最大1000
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```java
[
    {
        'orderId': '499902955766523648', 
        'symbol': 'BHTUSDT', 
        'price': '0.01', 
        'origQty': '50', 
        'executedQty': '0', 
        'avgPrice': '0', 
        'status': 'NEW', 
        'type': 'LIMIT', 
        'side': 'BUY', 
        'time': '1574329076202'
        },...
]
```
{% endswagger-response %}
{% endswagger %}

#### **Response:**

| 名称              | 类型     | 例子                   | 描述                                                                                                     |
| --------------- | ------ | -------------------- | ------------------------------------------------------------------------------------------------------ |
| `orderId`       | long   | `150695552109032492` | 订单ID（系统生成）                                                                                             |
| `clientOrderId` | string | `213443`             | 订单ID（自己发送的）                                                                                            |
| `symbol`        | string | `BTCUSDT`            | 币对名称                                                                                                   |
| `price`         | float  | `4765.29`            | 订单价格                                                                                                   |
| `origQty`       | float  | `1.01`               | 订单数量                                                                                                   |
| `executedQty`   | float  | `1.01`               | 已经成交订单数量                                                                                               |
| `avgPrice`      | float  | `4754.24`            | 订单已经成交的平均价格                                                                                            |
| `type`          | string | `LIMIT`              | 订单类型。可能出现的值只能为:`LIMIT`(限价)和`MARKET`（市价）                                                                |
| `side`          | string | `BUY`                | 订单方向。可能出现的值只能为：`BUY`（买入做多） 和 `SELL`（卖出做空）                                                              |
| `status`        | string | `NEW`                | 订单状态。可能出现的值为：`NEW`(新订单，无成交)、`PARTIALLY_FILLED`（部分成交）、`FILLED`（全部成交）、`CANCELED`（已取消）和`REJECTED`（订单被拒绝）. |

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/myTrades" method="get" summary=" 交易记录" %}
{% swagger-description %}
**Demo:**\
`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/Trades.java` \
\
**限速规则: 20次/2s**
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" required="true" %}
&#x20;签名
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" required="true" %}
&#x20;您的API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" required="true" %}
&#x20;时间戳
{% endswagger-parameter %}

{% swagger-parameter in="query" name="symbol" type="string" required="true" %}
&#x20;币对名称 E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="string" required="true" %}
&#x20;默认100; 最大1000
{% endswagger-parameter %}

{% swagger-parameter in="query" name="fromId" type="integer" required="true" %}
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
    "feeCoin": "ETH",
    "fee":"0.001"
  },...
]
```
{% endswagger-response %}
{% endswagger %}

#### **Response:**

| 名称        | 类型      | 例子                   | 描述                            |
| --------- | ------- | -------------------- | ----------------------------- |
| `symbol`  | string  | `ETHBTC`             | 币种名称(交易对)                     |
| `id`      | integer | `28457`              | 交易ID                          |
| `bidId`   | long    | `150695552109032492` | 买方订单ID                        |
| `askId`   | long    | `150695552109032493` | 卖方订单ID                        |
| `price`   | integer | `4.01`               | 交易时间戳                         |
| `qty`     | float   | `12`                 | 交易数量                          |
| `time`    | number  | `1499865549590`      | 交易时间戳                         |
| `isBuyer` | bool    | `true`               | `true`= Buyer `false`= Seller |
| `isMaker` | bool    | `false`              | `true`=Maker `false`=Taker    |
| `feeCoin` | string  | `ETH`                | 交易手续费币种                       |
| `fee`     | number  | `0.001`              | 交易手续费                         |

## 账户

### 安全类型:[ USER\_DATA](general-info.md#jie-kou-jian-quan-lei-xing)

账户下方的接口都需要[签名和API-key验证](general-info.md#xu-yao-qian-ming-de-jie-kou-trade-yu-userdata)

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/account" method="get" summary=" 账户信息" %}
{% swagger-description %}
**Demo:** \
`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/AccountInformation.java`\
\
**限速规则: 20次/2s**
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" required="true" %}
&#x20;签名
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" required="true" %}
&#x20;您的API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" required="true" %}
&#x20;时间戳
{% endswagger-parameter %}

{% swagger-response status="200" description=" 获取账户信息成功" %}
```java
{
    'balances': 
        [
            {
                'asset': 'BTC', 
                'free': '0', 
                'locked': '0'
                }, 
            {
                'asset': 'ETH', 
                'free': '0', 
                'locked': '0'
                },...
        ]
}
```
{% endswagger-response %}
{% endswagger %}

#### Response:

| 名称         | 类型   | 描述   |
| ---------- | ---- | ---- |
| `balances` | `[]` | 余额集合 |

`balances` field:

| 名称       | 类型     | 例子      | 描述   |
| -------- | ------ | ------- | ---- |
| `asset`  | string | `USDT`  | 币种名称 |
| `free`   | float  | 1000.30 | 可用   |
| `locked` | float  | 400     | 冻结   |
