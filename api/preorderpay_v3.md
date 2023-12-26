<b style="font-size: 2em">主扫支付 v3</b>

---

# 主扫预下单v3

**应用场景**

用户通过微信公众号（支付宝服务窗、数字人民币）或扫描二维码，可以支付完成下单购买流程。

**注意事项**

【商户单号生成】

当同一业务订单需要进行多次支付（前几次失败或被撤销）时，需要保证每次调用接口传入的商户单号 out_trade_no 不重复，
因此不能直接将业务订单号作为商户单号使用，而是应该为每个支付请求生成独立的流水号，并在商户服务端维护业务订单号与流水号（商户单号）的关系。
建议商户单号规则为“业务订单号+请求序号”，例如对于业务订单号 A10001，第一次请求支付的商户单号为A100011，如果失败或未支付被撤销，再次发起的支付的商户单号为 A100012，以此类推。

提交下单请求后会同步返回交易状态。当出现网络异常、超时或交易状态为“NEED_QUERY”时，商户系统等待5秒后调用【[订单查询](/api/micropay.md#订单查询)】，查询支付实际交易结果；当返回结果为“NEED_QUERY”时，商户系统可设置间隔时间(建议5秒)重新查询支付结果，直到支付成功或超时(建议60~180秒)；

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td class="tb-head">接口地址</td>
        <td colspan="2">https://pay.storepos.cn/v3/UnifiedPay/Gateway</td>
    </tr>
    <tr>
        <td class="tb-head">提交方式</td>
        <td colspan="2">POST</td>
    </tr>
    <tr>
        <td class="tb-head">校验签名</td>
        <td colspan="2">是</td>
    </tr>
    <tr>
        <td class="tb-head">签名密钥</td>
        <td colspan="2">商户密钥</td>
    </tr>
</table>

**公共请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| method | 是 | PreOrder_WECHAT | 接口名称，PreOrder_WECHAT-微信，PreOrder_ALIPAY-支付宝，PreOrder_ECNY-数币 |
| pid | 是 | yunpos | 调用方产品名称 |
| version | 是 | 1.0 | 调用方版本号 |
| mch_id | 是 | 00000001 | 超赢商户号 |
| content | 是 | - | 请求参数（Json后加密） |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| sub_appid | 否 | wxaee08d155d9de0c5 | 微信公众号AppId或开放平台APP应用AppId。trade_type=JSPAY、APP时，此参数必传 |
| is_minipg | 否 | 1 | 是否微信小程序支付。1：小程序支付；0：表示公众号支付。 |
| buyer_id | 否 | oRA5quGvJc1wwvjMW-tnpLLqD-FM | 买家用户标识。trade_type=JSPAY，此参数必传 |
| device_info | 否 | 013467007045764 | 终端设备号，商户自定义。 |
| body | 是 | image形象店-深圳腾大- QQ公仔 | 商品描述 |
| attach | 否 | 说明 | 商户附加信息，可做扩展参数 |
| out_trade_no | 是 | 1497769914931 | 商户系统内部的订单号，5到32个字符、只能包含字母数字，区分大小写，确保在商户系统唯一 |
| total_fee | 是 | 1 | 总金额，以分为单位，只能为整数 |
| mch_create_ip | 否 | 114.114.114.114 | 调用支付API的机器IP |
| time_start | 否 | 20091225091010 | 交易起始时间，格式为yyyyMMddHHmmss，如2009年12月25日9点10分10秒表示为20091225091010。时区为GMT+8 Beijing |
| time_expire | 否 | 20091225091510 | 交易结束时间，格式为yyyyMMddHHmmss，如2009年12月25日9点15分10秒表示为20091225091510。时区为GMT+8 Beijing |
| notify_url | 否 | <http://baidu.com/notify> | 接收支付异步通知回调地址，通知url必须为直接可访问的url，**不能携带参数** |
| op_shop_id | 否 | 00000001 | 门店编号 |
| op_user_id | 否 | 00000001 | 操作员帐号，默认为商户号 |
| limit_pay | 否 | NO_CREDIT | no_credit指定不能使用信用卡支付 |
| trade_type | 是 | JSPAY | 交易类型；JSPAY-服务窗支付、NATIVE-原生扫码支付、APP-APP支付，APP_BANK-APP支付银行模式 |
| product_id | 否 | 1223541321407035645 | trade_type=NATIVE，此参数必传。此id为二维码中包含的商品ID，商户自行定义 |
| goods_tag | 否 | CY_PROMOTION_001 | 订单优惠标记，用于优惠券或者满减使用（数币该字段不传） |
| goods_detail | 否 | [{"goods_id":"CY000","goods_name":"促销单品","quantity":1,"price":1}] | 商品详情，JSON Array格式 |
| profit_sharing | 否 | N | 分账标识 |
| profit_sharing_receiver | 否 | - | 分账明细 |

goods_detail为JSON数组类型结构如下

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| goods_id | 是 | CY00000000001 | 商品编码，由半角的大小写字母、数字、中划线、下划线中的一种或几种组成 |
| pay_goods_id | 否 | 20010001 | 微信/支付宝的商品编码（没有可不传） |
| goods_name | 否 | 纸巾 | 商品名称 |
| quantity | 是 | 1 | 商品数量（整数） |
| price | 是 | 100 | 商品单价（整数），单位为：分 |

**请求参数示例**

> method=PreOrder_WECHAT&version=1.0&pid=yunpos&mch_id=00000001&content=u8PKPKxrgMTDmndycpwLmQ&sign=00000000000000000000000000000000

**响应结果**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| code | 否 | 状态码 ，详见参数规定 |
| msg | 否 | 返回信息 |
| trade_state | 否 | 交易状态，详见参数规定 |
| content | 否 | 响应报文 |
| sign | 否 | 响应结果的签名串(仅业务正确时返回签名) |

以下字段在state和trade_state都为SUCCESS的时候在content中返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| mch_id | 是 | 超赢商户号 |
| appid | 否 | 调用接口提交的微信APPID |
| sub_openid | 是 | 子商户appid下用户唯一标识，如需返回则请求时需要传sub_appid |
| out_trade_no | 是 | 商户系统内部的定单号，32个字符内、可包含字母 |
| pay_info | 否 | 支付信息，用以唤起微信支付；trade_type=JSPAY时，此参数有返回 |
| code_url | 否 | 商户可用此参数自定义去生成二维码后展示出来进行扫码支付；trade_type=NATIVE时，此参数有返回（使用该字段生成二维码供买家扫码付款） |
| wx_mch_id | 否 | 微信服务商商户号 |
| wx_sub_mch_id | 否 | 微信子商户号 |
| nonce_str | 是 | 随机字符串 |

**响应结果示例**

```json
{
    "state": "SUCCESS",
    "code": "10000",
    "trade_state": "SUCCESS",
    "msg": "SUCCESS",
    "content": "u8PKPKxrgMTDmndycpwLmQ",
    "sign": "00000000000000000000000000000000"
}

{// 微信JSPAY content
    "mch_id": "00000001",
    "appid": "wxc3d2e734ae326831",
    "out_trade_no": "1497769914931",
    "sub_openid": "o4he1jo7fA1rIWTOOA3h00000000",
    "buyer_id": "o4he1jo7fA1rIWTOOA3h00000000",
    "pay_info": "{\"appId\":\"wxc3d2e734ae326831\",\"timeStamp\":\"1511947589427\",\"signType\":\"MD5\",\"package\":\"prepay_id=wx2017112917262941a3a33e980001282756\",\"nonceStr\":\"1511947589427\",\"paySign\":\"CD871BCD09B3D0C6339B2D0DE72DE7EE\"}",
    "wx_mch_id": "1264300000",
    "wx_sub_mch_id": "1266500000",
    "nonce_str": ""
}

{// 微信NATIVE content
    "mch_id": "00000001",
    "out_trade_no": "1497769914931",
    "appid": "wxc3d2e734ae326831",
    "code_url": "weixin://wxpay/bizpayurl?pr=xxxxxxxxx",
    "wx_mch_id": "1264300000",
    "wx_sub_mch_id": "1266500000",
    "nonce_str": ""
}

{// 支付宝JSPAY content
    "mch_id": "00000001",
    "out_trade_no": "1497769914931",
    "sub_openid": "2088102705271184",
    "buyer_id": "2088102705271184",
    "pay_info": "{\"tradeNO\":\"2023053122001471181451960663\"}",
    "wx_mch_id": "1264300000",
    "wx_sub_mch_id": "1266500000",
    "nonce_str": "00000000000000000000000000000000",
}

{// 支付宝NATIVE content
    "mch_id": "00000001",
    "out_trade_no": "1497769914931",
    "sub_openid": "2088102705271184",
    "buyer_id": "2088102705271184",
    "code_url": "https://qr.alipay.com/bax08752cgfkhh5non0u304e",
    "wx_mch_id": "1264300000",
    "wx_sub_mch_id": "1266500000",
    "nonce_str": ""
}

{// 数币
    "mch_id": "00000001",
    "out_trade_no": "1523265111702",
    "code_url": "https://qr.pbcdci.cn/004043112022083115224300703035700000004",
    "nonce_str": ""
}
```

---

# 主扫付款通知v3

**应用场景**

通知 URL 是初始化请求接口中提交的参数 notify_url，支付完成后，平台会把相关支付和用户信息发送到该 URL，商户需要接收处理信息。

对后台通知交互时，如果平台收到商户的应答不是纯字符串**success**或超过3秒后返回时，平台认为通知失败，平台会通过一定的策略（**通知频率为 0/15s/15s/15s/30s/3m/3m/30m/30m/30m/30m/1h**）间接性重新发起通知，尽可能提高通知的成功率，但不保证通知最终能成功。

由于存在重新发送后台通知的情况， 因此同样的通知可能会**多次发送**给商户系统。商户系统必须能够正确处理重复的通知。

推荐的做法是， 当收到通知进行处理时， 首先检查对应业务数据的状态， 判断该通知是否已经处理过， 如果没有处理过再进行处理， 如果处理过直接返回结果成功。 在对业务数据进行状态检查和处理之前， 要采用数据锁进行并发控制， 以避免函数重入造成的数据混乱。

**特别注意：商户后台接收到通知参数后，一定要对接收到通知参数里的订单号out_trade_no和订单金额total_fee和自身业务系统的订单和金额做校验，校验一致后才更新数据库订单状态，防止数据泄漏导致出现“假通知”，造成资金损失。**

后台通知通过请求中的notify_url进行， POST方式给商户系统（通知参数内容为HASH的字符串）

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td class="tb-head">接口地址</td>
        <td>该链接是通过<a href="#主扫预下单v3">主扫预下单v3</a>接口中提交的参数notify_url设置，如果链接无法访问，商户将无法接收到通知。</td>
    </tr>
    <tr>
        <td class="tb-head">提交方式</td>
        <td>POST</td>
    </tr>
    <tr>
        <td class="tb-head">校验签名</td>
        <td>是</td>
    </tr>
    <tr>
        <td class="tb-head">签名密钥</td>
        <td>商户密钥</td>
    </tr>
</table>

**通知参数**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| result_code | 是 | 状态码 ，SUCCESS-成功，其他-失败 |
| sign | 是 | 通知的签名串 |

以下字段在state和result_code都为SUCCESS的时候有返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| mch_id | 是 | 超赢商户号 |
| pay_result | 是 | 支付结果：0—成功；其它—失败 |
| out_trade_no | 是 | 商户系统内部的订单号，32个字符内、可包含字母 |
| transaction_id | 是 | 平台交易号 |
| total_fee | 是 | 总金额，以分为单位，只能为整数 |
| time_end | 是 | 支付完成时间，格式为yyyyMMddHHmmss，如2009年12月25日9点10分10秒表示为20091225091010。时区为GMT+8 Beijing |
| trade_type | 是 | 交易类型；pay.alipay.native原生扫码支付，pay.alipay.jspay服务窗支付 |
| nonce_str | 是 | 随机字符串 |
| device_info | 否 | 终端设备号 |
| out_transaction_id | 否 | 第三方订单号 |
| fee_type | 否 | 货币类型，符合 ISO 4217 标准的三位字母代码，默认人民币：CNY |
| coupon_fee | 否 | 代金券金额，代金券金额&lt;=订单金额，订单金额 - 代金券金额 = 现金支付金额 |
| bank_type | 否 | 付款银行 |
| sub_appid | 否 | 调用接口提交的子商户公众账号ID |
| sub_openid | 否 | 子商户appid下用户唯一标识，用户关注时存在 |
| promotion_detail | 否 | 营销详情，返回值为Json格式 |
| wx_mch_id | 否 | 微信服务商商户号 |
| wx_sub_mch_id | 否 | 微信子商户号 |

**请求参数示例**

> bank_type=CFT&mch_id=f20170519135901860000&nonce_str=1523929649387&out_trade_no=1523929500000&out_transaction_id=2018041721001004870537670226&pay_result=0&result_code=SUCCESS&sign=00000000000000000000000000000000&state=SUCCESS&time_end=20180417094729&total_fee=1&trade_type=pay.weixin.native&transaction_id=199520439266201804177199552446

**后台通知结果反馈**

| 返回结果 | 结果说明 |
| :--- | :--- |
| success | 处理成功，平台收到此结果后不再进行后续通知 |
| fail或其它字符 | 处理不成功，平台收到此结果或者没有收到任何结果，系统通过补单机制再次通知 |
