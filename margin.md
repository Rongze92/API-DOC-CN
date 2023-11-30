# 杠杆交易

## 交易

### 安全类型: [TRADE](general-info.md#jie-kou-jian-quan-lei-xing)

交易下方的接口都需要[签名和API-key验证](general-info.md#xu-yao-qian-ming-de-jie-kou-trade-yu-userdata)

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/margin/order" method="post" summary=" 创建杠杆订单" %}
{% swagger-description %}
**Demo:**\
`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/margin/NewOrder.java` \
\
**限速规则：10次/s**
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

{% swagger-parameter in="body" name="symbol" type="string" %}
&#x20;币对名称 E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="volume" type="number" %}
&#x20;订单数量
{% endswagger-parameter %}

{% swagger-parameter in="body" name="side" type="string" %}
&#x20;订单方向, `BUY/SELL`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="string" %}
&#x20;订单类型, `LIMIT/MARKET`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="price" type="number" %}
&#x20;订单价格, 对于`LIMIT`订单必须发送
{% endswagger-parameter %}

{% swagger-parameter in="body" name="newClientOrderId" type="string" %}
&#x20;客户端订单标识
{% endswagger-parameter %}

{% swagger-parameter in="body" name="recvWindow" type="string" %}
&#x20;时间窗口
{% endswagger-parameter %}

{% swagger-response status="200" description=" 发送杠杆订单成功" %}
```java
{
    'symbol': 'LXTUSDT', 
    'orderId': '494736827050147840', 
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

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/margin/order" method="get" summary=" 杠杆订单查询" %}
{% swagger-description %}
**Demo:**\
`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/margin/QueryOrder.java`\

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

{% swagger-parameter in="query" name="orderId" type="string" %}
&#x20;订单ID
{% endswagger-parameter %}

{% swagger-parameter in="query" name="newClientOrderId" type="string" %}
&#x20;客户端订单标识
{% endswagger-parameter %}

{% swagger-parameter in="query" name="symbol" type="string" %}
&#x20;币对名称E.g. `BTCUSDT`
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

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/margin/cancel" method="post" summary=" 撤销杠杆订单" %}
{% swagger-description %}
**Demo:**\
`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/margin/CancelOrder.java`\

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

{% swagger-parameter in="body" name="orderId" type="string" %}
&#x20;订单id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="newClientOrderId" type="string" %}
&#x20;客户端订单标识
{% endswagger-parameter %}

{% swagger-parameter in="body" name="symbol" type="string" %}
&#x20;币对名称E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
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

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/margin/openOrders" method="get" summary=" 杠杆当前委托" %}
{% swagger-description %}
**Demo:**\
`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/margin/CurrentOpenOrders.java`\

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

{% swagger-parameter in="query" name="symbol" type="string" %}
&#x20;币对名称 E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="integer" %}
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

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/margin/myTrades" method="get" summary=" 杠杆交易记录" %}
{% swagger-description %}
**Demo:**\
`https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/margin/Trades.java`\

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

{% swagger-parameter in="query" name="symbol" type="string" %}
&#x20;币对名称 E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="integer" %}
&#x20;默认100; 最大1000
{% endswagger-parameter %}

{% swagger-parameter in="query" name="fromId" type="integer" %}
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
