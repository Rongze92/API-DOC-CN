---
description: 错误码解释说明
---

# 错误码

返回报错一般由两个部分组成：错误码和错误信息。错误码是通用的，但是错误信息会有所不同。如下是一个报错JSON Payload示例：

```java
{
  "code":-1121,
  "msg":"Invalid symbol."
}
```

## 10xx - 通用服务器和网络错误

### -1000 UNKNOWN

* 处理请求时发生未知错误

### -1001 DISCONNECTED

* 内部错误, 无法处理您的请求, 请再试一次

### -1002 UNAUTHORIZED

* 您无权执行此请求. 请求需要发送API key,  我们建议在所有的请求头附加API key

### -1003 TOO\_MANY\_REQUESTS

* 请求过于频繁超过限制.

### -1004 NO\_THIS\_COMPANY

* 您无权执行此请求, User not exit Company

### -1006 UNEXPECTED\_RESP

* 接收到了不符合预设格式的消息，下单状态未知

### -1007 TIMEOUT

* 等待后端服务器响应超时。 发送状态未知； 执行状态未知

### -1014 UNKNOWN\_ORDER\_COMPOSITION

* 不支持的订单组合

### -1015 TOO\_MANY\_ORDERS

* 新订单太多。请减少你的请求频率

### -1016 SERVICE\_SHUTTING\_DOWN

* 服务器下线

### -1017 ILLEGAL\_CONTENT\_TYPE

* 我们建议在所有的请求头附加Content-Type, 并设置成application/json

### -1020 UNSUPPORTED\_OPERATION

* 不支持此操作

### -1021 INVALID\_TIMESTAMP

* 时延过大，服务器根据接请求中的时间戳判定耗时已经超出了recevWindow。请改善网络条件或者增大recevWindow.
* 时间偏移过大，服务器根据请求中的时间戳判定客户端时间比服务器时间提前了1秒钟以上.

### -1022 INVALID\_SIGNATURE

* 此请求的签名无效。

### -1023 UNTIMESTAMP

* 您无权执行此请求, 我们建议您在所有的请求头附加X-CH-TS

### -1024 UNSIGNATURE

* 您无权执行此请求, 我们建议您在请求头附加X-CH-SIGN

## 11xx - 请求内容中的问题

### -1100 ILLEGAL\_CHARS

* 在参数中发现非法字符。&#x20;

### -1101 TOO\_MANY\_PARAMETERS

* 发送的参数太多。 &#x20;
* 检测到的参数值重复

### -1102 MANDATORY\_PARAM\_EMPTY\_OR\_MALFORMED

* 未发送强制性参数，该参数为空/空或格式错误。 &#x20;
* 强制参数'％s'未发送，为空/空或格式错误。 &#x20;
* 必须发送参数'％s'或'％s'，但两者均为空！

### -1103 UNKNOWN\_PARAM

* 发送了未知参数。
* 每条请求需要至少一个参数{Timestamp}.

### -1104 UNREAD\_PARAMETERS

* 并非所有发送的参数都被读取。
* 并非所有发送的参数都被读取； 读取了'％s'参数，但被发送了'％s'。

### -1105 PARAM\_EMPTY

* 参数为空。
* 参数'％s'为空。

### -1106 PARAM\_NOT\_REQUIRED

* 不需要时已发送参数。
* 不需要时发送参数'％s'。

### -1111 BAD\_PRECISION

* 精度超过为此资产定义的最大值。

### -1112 NO\_DEPTH

* 交易对没有挂单

### -1116 INVALID\_ORDER\_TYPE

* 无效订单类型。

### -1117 INVALID\_SIDE

* 无效买卖方向。

### -1118 EMPTY\_NEW\_CL\_ORD\_ID

* 新的客户订单ID为空。

### -1121 BAD\_SYMBOL

* 无效的symbol

### -1136 ORDER\_QUANTITY\_TOO\_SMALL

* 订单quantity小于最小值

### -1138 ORDER\_PRICE\_WAVE\_EXCEED

* 订单价格超出允许范围

### -1139 ORDER\_NOT\_SUPPORT\_MARKET

* 该交易对不支持市价交易

### -1145 ORDER\_NOT\_SUPPORT\_CANCELLATION

* 该订单类型不支持撤销

### -1147  PRICE\_VOLUME\_PRESION\_ERROR

* 订单价格或数量超过最大限制

### -2013 NO\_SUCH\_ORDER

* Order不存在

### -2015 REJECTED\_CH\_KEY

* 无效的API密钥，IP或操作权限.

### -2016 EXCHANGE\_LOCK

* 交易被冻结

### -2017 BALANCE\_NOT\_ENOUGH

* 余额不足
