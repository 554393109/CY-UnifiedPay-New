# 微信预下单

**应用场景**

用户通过微信公众号或扫描二维码，可以支付完成下单购买流程。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">接口地址</td>
        <td>https://{BaseURL}/Open/WECHAT_PreOrder</td>
    </tr>
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">提交方式</td>
        <td>POST</td>
    </tr>
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">校验签名</td>
        <td>是</td>
    </tr>
</table>

**公共请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| agent_id | 是 | 13000000000000001 | 代理商编号 |
| nonce_str | 否 | 00000000000000000000000000000000 | 随机字符串 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| mch_id | 是 | 00000001 | 超赢商户号 |
| sub_appid | 是 | wxaee08d155d9de0c5 | 公众号AppId。trade_type=JSPAY、APP、APP_BANK时，此参数必传 |
| is_minipg | 否 | 1 | 是否小程序支付。1：小程序支付；0：表示公众号支付 |
| buyer_id | 否 | oRA5quGvJc1wwvjMW-tnpLLqD-FM | 在sub_appid下通过微信授权取得的买家sub_openid。trade_type=JSPAY，此参数必传 |
| device_info | 否 | 013467007045764 | 终端设备号，商户自定义。 |
| body | 是 | image形象店-深圳腾大- QQ公仔 | 商品描述 |
| attach | 否 | 说明 | 商户附加信息，可做扩展参数 |
| out_trade_no | 是 | 1497769914931 | 商户系统内部的订单号 ,5到32个字符、 只能包含字母数字，区分大小写，确保在商户系统唯一 |
| total_fee | 是 | 1 | 总金额，以分为单位，只能为整数 |
| mch_create_ip | 否 | 114.114.114.114 | 调用支付API的机器IP |
| time_start | 否 | 20091225091010 | 交易起始时间，格式为yyyyMMddHHmmss，如2009年12月25日9点10分10秒表示为20091225091010。时区为GMT+8 Beijing |
| time_expire | 否 | 20091225091510 | 交易结束时间，格式为yyyyMMddHHmmss，如2009年12月25日9点15分10秒表示为20091225091510。时区为GMT+8 Beijing |
| goods_tag | 否 | WXG | 订单优惠标记，用于优惠券或者满减使用 |
| notify_url | 否 | <http://baidu.com/notify> | 接收支付异步通知回调地址，通知url必须为直接可访问的url，**不能携带参数** |
| op_user_id | 否 | 00000001 | 操作员帐号，默认为商户号 |
| limit_pay | 否 | NO_CREDIT | no_credit指定不能使用信用卡支付 |
| trade_type | 是 | JSPAY | 交易类型；JSPAY-服务窗支付、NATIVE-原生扫码支付、APP-APP支付，APP_BANK-APP支付银行模式 |
| product_id | 否 | 1223541321407035645 | trade_type=NATIVE，此参数必传。此id为二维码中包含的商品ID，商户自行定义 |

**请求参数示例**

> agent_id=13000000000000001&mch_id=00000001™_type=NATIVE&body=超赢支付聚合支付&out_trade_no=1497769914931&total_fee=1&sign=00000000000000000000000000000000

**响应结果**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| code | 是 | 状态码 ，详见参数规定 |
| msg | 否 | 返回信息 |
| trade_state | 否 | 交易状态，详见参数规定 |

以下字段在state和trade_state都为SUCCESS的时候有返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| mch_id | 是 | 超赢商户号 |
| appid | 是 | 调用接口提交的公众账号ID |
| sub_openid | 是 | 子商户appid下用户唯一标识，如需返回则请求时需要传sub_appid |
| out_trade_no | 是 | 商户系统内部的定单号，32个字符内、可包含字母 |
| token_id | 是 | 动态口令 |
| pay_info | 是 | 支付信息，用以唤起微信支付 |
| services | 否 | 支持的交易类型，多个以竖线分割 |
| nonce_str | 是 | 随机字符串 |

**响应结果示例**

```json
{
    "state": "SUCCESS",
    "code": "10000",
    "trade_state": "SUCCESS",
    "msg": "SUCCESS",
    "mch_id": "3338102513618944",
    "out_trade_no": "1497769914931",
    "token_id": "16c5f40274e084b123a08f1313d53da57",
    "pay_info": "{\"appId\":\"wxc3d2e734ae326831\",\"timeStamp\":\"1511947589427\",\"status\":\"0\",\"signType\":\"MD5\",\"package\":\"prepay_id=wx2017112917262941a3a33e980001282756\",\"callback_url\":\"\",\"nonceStr\":\"1511947589427\",\"paySign\":\"CD871BCD09B3D0C6339B2D0DE72DE7EE\"}",
    "nonce_str": "14a9edad51c2403f9318c6d699152168"
}
```

---

# 支付宝预下单

**应用场景**

用户通过支付宝服务窗或扫描二维码，可以支付完成下单购买流程。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">接口地址</td>
        <td>https://{BaseURL}/Open/ALIPAY_PreOrder</td>
    </tr>
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">提交方式</td>
        <td>POST</td>
    </tr>
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">校验签名</td>
        <td>是</td>
    </tr>
</table>

**公共请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| agent_id | 是 | 13000000000000001 | 代理商编号 |
| nonce_str | 否 | 00000000000000000000000000000000 | 随机字符串 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| mch_id | 是 | 00000001 | 超赢商户号 |
| device_info | 否 | 013467007045764 | 终端设备号，商户自定义。 |
| body | 是 | image形象店-深圳腾大- QQ公仔 | 商品描述 |
| attach | 否 | 说明 | 商户附加信息，可做扩展参数 |
| out_trade_no | 是 | 1497769914931 | 商户系统内部的订单号 ,5到32个字符、 只能包含字母数字，区分大小写，确保在商户系统唯一 |
| total_fee | 是 | 1 | 总金额，以分为单位，只能为整数 |
| mch_create_ip | 否 | 114.114.114.114 | 调用支付API的机器IP |
| time_start | 否 | 20091225091010 | 交易起始时间，格式为yyyyMMddHHmmss，如2009年12月25日9点10分10秒表示为20091225091010。时区为GMT+8 Beijing。注：交易起始时间与交易结束时间需要同时传入才会生效。 |
| time_expire | 否 | 20091225091510 | 交易结束时间，格式为yyyyMMddHHmmss，如2009年12月25日9点15分10秒表示为20091225091510。时区为GMT+8 Beijing。注：交易起始时间与交易结束时间需要同时传入才会生效。 |
| goods_tag | 否 | WXG | 订单优惠标记，用于优惠券或者满减使用 |
| notify_url | 否 | <http://baidu.com/notify> | 接收支付异步通知回调地址，通知url必须为直接可访问的url，**不能携带参数** |
| op_user_id | 否 | 00000001 | 操作员帐号，默认为商户号 |
| limit_pay | 否 | NO_CREDIT | no_credit指定不能使用信用卡支付 |
| trade_type | 是 | NATIVE | 交易类型；JSPAY-服务窗支付、NATIVE-原生扫码支付、APP-APP支付，APP_BANK-APP支付银行模式 |
| product_id | 否 | 1223541321407035645 | trade_type=JSPAY时，此参数必传。此id为二维码中包含的商品ID，商户自行定义 |
| buyer_logon_id | 否 | 13800000000 | 买家支付宝账号。trade_type=JSPAY时，和buger_id不能同时为空 |
| buyer_id | 否 | 2088822494428872 | 买家支付宝用户ID。trade_type=JSPAY时，和buyer_logon_id不能同时为空 |

**请求参数示例**

> agent_id=13000000000000001&mch_id=00000001&body=超赢支付聚合支付&out_trade_no=1497769914931&total_fee=1™_type=NATIVE&sign=00000000000000000000000000000000

**响应结果**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| code | 是 | 状态码 ，详见参数规定 |
| msg | 否 | 返回信息 |
| trade_state | 否 | 交易状态，详见参数规定 |

以下字段在state和trade_state都为SUCCESS的时候有返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| mch_id | 是 | 超赢商户号 |
| out_trade_no | 是 | 商户系统内部的定单号，32个字符内、可包含字母 |
| pay_info | 是 | JSON字符串，自行唤起支付宝钱包支付；trade_type=JSPAY时，此参数有返回 |
| pay_url | 是 | 仅作为参考使用，商户需自己实现该支付页面；trade_type=JSPAY时，此参数有返回 |
| code_img_url | 是 | 此参数的值即是根据code_url生成的可以扫码支付的二维码图片地址；trade_type=NATIVE时，此参数有返回 |
| code_url | 是 | 商户可用此参数自定义去生成二维码后展示出来进行扫码支付；trade_type=NATIVE时，此参数有返回 |
| nonce_str | 是 | 随机字符串 |

**响应结果示例**

```json
{
    "state": "SUCCESS",
    "code": "10000",
    "trade_state": "SUCCESS",
    "msg": "SUCCESS",
    "mch_id": "3338102513618944",
    "out_trade_no": "1523265111702",
    "code_img_url": "https://pay.swiftpass.cn/pay/qrcode?uuid=https%3A%2F%2Fqr.alipay.com%2Fbax04486r0vgbxds3h55805a",
    "code_url": "https://qr.alipay.com/bax04486r0vgbxds3h55805a",
    "nonce_str": "f032dd959bb0428ba01d58dad8a70ffa"
}
```

---

# 微信预下单结果通知

**应用场景**

通知 URL 是初始化请求接口中提交的参数 notify_url，支付完成后，平台会把相关支付和用户信息发送到该 URL，商户需要接收处理信息。

对后台通知交互时，如果平台收到商户的应答不是纯字符串**success**或超过3秒后返回时，平台认为通知失败，平台会通过一定的策略（**通知频率为0/15/15/30/180/1800/1800/1800/1800/3600，单位：秒**）间接性重新发起通知，尽可能提高通知的成功率，但不保证通知最终能成功。

由于存在重新发送后台通知的情况， 因此同样的通知可能会**多次发送**给商户系统。商户系统必须能够正确处理重复的通知。

推荐的做法是， 当收到通知进行处理时， 首先检查对应业务数据的状态， 判断该通知是否已经处理过， 如果没有处理过再进行处理， 如果处理过直接返回结果成功。 在对业务数据进行状态检查和处理之前， 要采用数据锁进行并发控制， 以避免函数重入造成的数据混乱。

**特别注意：商户后台接收到通知参数后，一定要对接收到通知参数里的订单号out_trade_no和订单金额total_fee和自身业务系统的订单和金额做校验，校验一致后才更新数据库订单状态，防止数据泄漏导致出现“假通知”，造成资金损失。**

后台通知通过请求中的notify_url进行， POST方式给商户系统（通知参数内容为HASH的字符串）

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">接口地址</td>
        <td>该链接是通过<a href="#微信预下单">微信预下单</a>接口中提交的参数notify_url设置，如果链接无法访问，商户将无法接收到通知。</td>
    </tr>
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">提交方式</td>
        <td>POST</td>
    </tr>
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">校验签名</td>
        <td>是</td>
    </tr>
</table>

**通知参数**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| result_code | 是 | 状态码 ，0-成功，其他-失败 |
| sign | 是 | 通知的签名串 |

以下字段在state和trade_state都为0的时候有返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| mch_id | 是 | 超赢商户号 |
| device_info | 否 | 终端设备号 |
| pay_result | 是 | 支付结果：0—成功；其它—失败 |
| out_trade_no | 是 | 商户系统内部的订单号，32个字符内、可包含字母 |
| out_transaction_id | 是 | 第三方订单号 |
| transaction_id | 是 | 平台交易号 |
| fee_type | 否 | 货币类型，符合 ISO 4217 标准的三位字母代码，默认人民币：CNY |
| total_fee | 是 | 总金额，以分为单位，只能为整数 |
| coupon_fee | 否 | 代金券金额，代金券金额&lt;=订单金额，订单金额 - 代金券金额 = 现金支付金额 |
| time_end | 是 | 支付完成时间，格式为yyyyMMddHHmmss，如2009年12月25日9点10分10秒表示为20091225091010。时区为GMT+8 Beijing |
| bank_type | 否 | 付款银行 |
| trade_type | 是 | 交易类型；pay.alipay.native原生扫码支付，pay.alipay.jspay服务窗支付 |
| sub_appid | 否 | 调用接口提交的子商户公众账号ID |
| sub_openid | 否 | 子商户appid下用户唯一标识，用户关注时存在 |
| nonce_str | 是 | 随机字符串 |

**请求参数示例**

> bank_type=CFT&mch_id=f20170519135901860000&nonce_str=1523929649387&out_trade_no=1523929500000&out_transaction_id=2018041721001004870537670226&pay_result=0&result_code=SUCCESS&sign=00000000000000000000000000000000&state=SUCCESS&time_end=20180417094729&total_fee=1&trade_type=pay.weixin.native&transaction_id=199520439266201804177199552446

**后台通知结果反馈**

| 返回结果 | 结果说明 |
| :--- | :--- |
| success | 处理成功，平台收到此结果后不再进行后续通知 |
| fail或其它字符 | 处理不成功，平台收到此结果或者没有收到任何结果，系统通过补单机制再次通知 |

---

# 支付宝预下单结果通知

**应用场景**

通知 URL 是初始化请求接口中提交的参数 notify_url，支付完成后，平台会把相关支付和用户信息发送到该 URL，商户需要接收处理信息。

对后台通知交互时，如果平台收到商户的应答不是纯字符串**success**或超过3秒后返回时，平台认为通知失败，平台会通过一定的策略（**通知频率为0/15/15/30/180/1800/1800/1800/1800/3600，单位：秒**）间接性重新发起通知，尽可能提高通知的成功率，但不保证通知最终能成功。

由于存在重新发送后台通知的情况， 因此同样的通知可能会**多次发送**给商户系统。商户系统必须能够正确处理重复的通知。

推荐的做法是， 当收到通知进行处理时， 首先检查对应业务数据的状态， 判断该通知是否已经处理过， 如果没有处理过再进行处理， 如果处理过直接返回结果成功。 在对业务数据进行状态检查和处理之前， 要采用数据锁进行并发控制， 以避免函数重入造成的数据混乱。

**特别注意：商户后台接收到通知参数后，一定要对接收到通知参数里的订单号out_trade_no和订单金额total_fee和自身业务系统的订单和金额做校验，校验一致后才更新数据库订单状态，防止数据泄漏导致出现“假通知”，造成资金损失。**

后台通知通过请求中的notify_url进行， POST方式给商户系统（通知参数内容为HASH的字符串）

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">接口地址</td>
        <td>该链接是通过<a href="#支付宝预下单">支付宝预下单</a>接口中提交的参数notify_url设置，如果链接无法访问，商户将无法接收到通知。</td>
    </tr>
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">提交方式</td>
        <td>POST</td>
    </tr>
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">校验签名</td>
        <td>是</td>
    </tr>
</table>

**通知参数**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| result_code | 是 | 状态码 ，0-成功，其他-失败 |
| sign | 是 | 通知的签名串 |

以下字段在state和trade_state都为0的时候有返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| mch_id | 是 | 超赢商户号 |
| device_info | 否 | 终端设备号 |
| pay_result | 是 | 支付结果：0—成功；其它—失败 |
| out_trade_no | 是 | 商户系统内部的订单号，32个字符内、可包含字母 |
| out_transaction_id | 是 | 第三方订单号 |
| transaction_id | 是 | 平台交易号 |
| fee_type | 否 | 货币类型，符合 ISO 4217 标准的三位字母代码，默认人民币：CNY |
| total_fee | 是 | 总金额，以分为单位，只能为整数 |
| invoice_amount | 否 | 用户在交易中支付的可开发票的金额 |
| time_end | 是 | 支付完成时间，格式为yyyyMMddHHmmss，如2009年12月25日9点10分10秒表示为20091225091010。时区为GMT+8 Beijing |
| bank_type | 否 | 付款银行 |
| trade_type | 是 | 交易类型；pay.alipay.native原生扫码支付，pay.alipay.jspay服务窗支付 |
| buyer_user_id | 是 | 买家支付宝用户ID |
| buyer_logon_id | 是 | 买家支付宝账号 |
| fund_bill_list | 否 | 交易支付使用的资金渠道 |
| nonce_str | 是 | 随机字符串 |

**请求参数示例**

> bank_type=ALIPAYACCOUNT&buyer_logon_id=13800000000%40qq.com&buyer_user_id=2088822494428000&device_info=device_info_yzq_01&fee_type=CNY&fund_bill_list=%5b%7b%22amount%22%3a%220.01%22%2c%22fundChannel%22%3a%22ALIPAYACCOUNT%22%7d%5d&gmt_create=20180417094613&invoice_amount=1&mch_id=f20170519135901860000&nonce_str=1523929649387&out_trade_no=1523929500000&out_transaction_id=2018041721001004870537670226&pay_result=0&result_code=SUCCESS&sign=00000000000000000000000000000000&state=SUCCESS&time_end=20180417094729&total_fee=1&trade_type=pay.alipay.native&transaction_id=199520439266201804177199552446

**后台通知结果反馈**

| 返回结果 | 结果说明 |
| :--- | :--- |
| success | 处理成功，平台收到此结果后不再进行后续通知 |
| fail或其它字符 | 处理不成功，平台收到此结果或者没有收到任何结果，系统通过补单机制再次通知 |
