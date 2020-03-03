<b style="font-size: 2em">刷卡支付</b>

---

# 提交支付

**应用场景**

收银员使用扫码设备读取微信（或支付宝等电子钱包）用户刷卡授权码以后，调用该接口发起支付对用户进行收款。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">接口地址</td>
        <td>https://{BaseURL}/UnifiedPay/Gateway</td>
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
| method | 是 | pay | 接口名称，pay |
| agent_id | 是 | 13000000000000000 | 代理商编号 |
| pid | 是 | yunpos | 调用方产品名称 |
| version | 是 | 1.0 | 调用方版本号 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| mch_id | 是 | 00000001 | 超赢商户号 |
| out_trade_no | 是 | 1497769914931 | 商户系统内部的订单号 ,5到32个字符、 只能包含字母数字或者下划线，区分大小写，确保在商户系统唯一 |
| device_info | 否 | 013467007045764 | 终端设备号，商户自定义。特别说明：对于QQ钱包支付，此参数必传，否则会报错。 |
| body | 是 | image形象店-深圳腾大- QQ公仔 | 商品描述 |
| attach | 否 | 说明 | 商户附加信息，可做扩展参数 |
| total_fee | 是 | 1 | 总金额，以分为单位，只能为整数 |
| mch_create_ip | 否 | 114.114.114.114 | 调用支付API的机器IP |
| auth_code | 是 | 120061098828009406 | 扫码支付授权码， 设备读取用户展示的条码信息 |
| op_user_id | 否 | 00000001 | 操作员帐号，默认为商户号 |
| op_shop_id | 否 | md_001 | 门店编号 |
| op_device_id | 否 | device_01 | 设备编号 |
| goods_tag | 否 | hot | 订单优惠标记，用于优惠券或者满减使用 |
| goods_detail | 否 | [{"goods_id":"CY000","goods_name":"促销单品","quantity":1,"price":1}] | 商品详情，JSON Array格式 |

goods_detail为JSON数组类型结构如下

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| goods_id | 是 | CY00000000001 | 商品编码，由半角的大小写字母、数字、中划线、下划线中的一种或几种组成 |
| pay_goods_id | 否 | 20010001 | 微信/支付宝的商品编码（没有可不传） |
| goods_name | 否 | 纸巾 | 商品名称 |
| quantity | 是 | 1 | 商品数量（整数） |
| price | 是 | 100 | 商品单价（整数），单位为：分 |

**请求参数示例**

> method=pay&agent_id=13000000000000000&mch_id=00000001&version=1.0&pid=yunpos&out_trade_no=1497769914931&auth_code=123123123&body=%E8%B6%85%E8%B5%A2%E6%94%AF%E4%BB%98&total_fee=4&goods_tag=CY_PROMOTION_001&goods_detail=[{"goods_id":"CY000000","goods_name":"促销单品-CY00000000000","quantity":1,"price":2},{"goods_id":"CY000001","goods_name":"促销单品-CY00000000001","quantity":1,"price":2}]&sign=00000000000000000000000000000000

**响应结果**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| code | 是 | 状态码 ，详见参数规定 |
| msg | 否 | 返回信息 |
| trade_state | 否 | 交易状态，详见参数规定 |
| sign | 是 | 响应结果的签名串 |

以下字段在state和trade_state都为SUCCESS的时候有返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| mch_id | 是 | 超赢商户号 |
| appid | 是 | 调用接口提交的公众账号ID |
| is_subscribe | 是 | 用户是否关注公众账号，仅在公众账号类型支付有效，取值范围：Y或N；Y-关注；N-未关注 |
| openid | 是 | 用户在商户 appid 下的唯一标识 |
| sub_appid | 是 | 调用接口提交的子商户公众账号ID |
| sub_is_subscribe | 是 | 用户是否关注子公众账号，仅在公众账号类型支付有效，取值范围：Y或N;Y-关注;N-未关注 |
| sub_openid | 是 | 子商户appid下用户唯一标识，如需返回则请求时需要传sub_appid |
| transaction_id | 是 | 平台交易号 |
| out_transaction_id | 是 | 第三方订单号 |
| out_trade_no | 是 | 商户系统内部的定单号，32个字符内、可包含字母 |
| base_fee | 是 | 订单应付金额，单位为分 |
| total_fee | 是 | 订单实付金额，单位为分 |
| coupon_fee | 否 | 代金券金额，代金券金额&lt;=订单金额，订单金额 - 代金券金额 = 现金支付金额 |
| fee_type | 否 | 货币类型，符合 ISO 4217 标准的三位字母代码，默认人民币：CNY |
| attach | 否 | 商家数据包，原样返回 |
| bank_type | 否 | 付款银行 |
| bank_billno | 否 | 银行订单号，若为第三方支付则为空 |
| time_end | 是 | 支付完成时间，格式为yyyyMMddHHmmss，如2009年12月25日9点10分10秒表示为20091225091010。时区为GMT+8 Beijing |
| nonce_str | 是 | 随机字符串 |
| promotion_detail | 否 | 营销详情，返回值为Json格式 |
| wx_mch_id | 否 | 微信服务商商户号 |
| wx_sub_mch_id | 否 | 微信子商户号 |

**响应结果示例**

```json
{
    "state": "SUCCESS",
    "code": "10000",
    "trade_state": "SUCCESS",
    "msg": "SUCCESS",
    "mch_id": "00000001",
    "appid": "wx1f87d44db95cba7a",
    "is_subscribe": "N",
    "openid": "oywgtuCJFeGzT-QtF-8U7FHb1z3Q",
    "sub_appid": "wxce38685bc050ef82",
    "sub_is_subscribe": "N",
    "sub_openid": "oHmbktxFlpoEPo2Ol5GOJniV2q-A",
    "transaction_id": "7551000001201706196281085687",
    "out_transaction_id": "4005572001201706196460269701",
    "out_trade_no": "1497862554883",
    "base_fee": "1",
    "total_fee": "1",
    "fee_type": "CNY",
    "bank_type": "CFT",
    "time_end": "20170619165616",
    "nonce_str": "a849df6660cb4354b6fe5b23120a73ce",
    "promotion_detail": "{\"promotion_detail\":[{\"promotion_id\":\"6348962444\",\"name\":\"维他减2分\",\"scope\":\"SINGLE\",\"type\":\"DISCOUNT\",\"amount\":2,\"activity_id\":\"9447213\",\"wxpay_contribute\":0,\"merchant_contribute\":2,\"other_contribute\":0,\"goods_detail\":[{\"goods_id\":\"CY00000000000\",\"quantity\":1,\"price\":2,\"discount_amount\":1,\"goods_remark\":\"单品券活动No.002\"},{\"goods_id\":\"CY00000000001\",\"quantity\":1,\"price\":2,\"discount_amount\":1,\"goods_remark\":\"单品券活动No.002\"}]}]}",
    "wx_mch_id": "1264300000",
    "wx_sub_mch_id": "1266500000",
    "sign": "00000000000000000000000000000000"
}
```

---

# 订单查询

**应用场景**

根据商户订单号或者平台订单号查询平台的具体订单信息。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">接口地址</td>
        <td>https://{BaseURL}/UnifiedPay/Gateway</td>
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
| method | 是 | orderquery | 接口名称，orderquery |
| agent_id | 是 | 13000000000000000 | 代理商编号 |
| pid | 是 | yunpos | 调用方产品名称 |
| version | 是 | 1.0 | 调用方版本号 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| paytype | 是 | WECHAT | 支付方式，详见参数规定 |
| mch_id | 是 | 00000001 | 超赢商户号 |
| out_trade_no | 否 | 1497769914931 | 商户系统内部的订单号，out_trade_no和transaction_id至少一个必填，同时存在时out_trade_no优先 |
| transaction_id | 否 | 7551000001201706166172780576 | 平台交易号，out_trade_no和transaction_id至少一个必填，同时存在时out_trade_no优先。 |

**请求参数示例**

> method=orderquery&agent_id=13000000000000000&version=1.0&pid=yunpos&paytype=WECHAT&mch_id=00000001&out_trade_no=1497769914931&sign=00000000000000000000000000000000

**响应结果**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| code | 是 | 状态码 ，详见参数规定 |
| msg | 否 | 返回信息 |
| trade_state | 否 | 交易状态，详见参数规定 |
| sign | 是 | 响应结果的签名串 |

以下字段在state和trade_state都为SUCCESS的时候有返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| mch_id | 是 | 超赢商户号 |
| appid | 是 | 调用接口提交的公众账号ID |
| is_subscribe | 是 | 用户是否关注公众账号，仅在公众账号类型支付有效，取值范围：Y或N;Y-关注;N-未关注 |
| openid | 是 | 用户在商户 appid 下的唯一标识 |
| sub_appid | 是 | 调用接口提交的子商户公众账号ID |
| sub_is_subscribe | 是 | 用户是否关注子公众账号，仅在公众账号类型支付有效，取值范围：Y或N；Y-关注；N-未关注 |
| sub_openid | 是 | 子商户appid下用户唯一标识，如需返回则请求时需要传sub_appid |
| transaction_id | 是 | 平台交易号 |
| out_transaction_id | 是 | 第三方订单号 |
| out_trade_no | 是 | 商户系统内部的定单号，32个字符内、可包含字母 |
| base_fee | 是 | 应付金额、订单金额，以分为单位，只能为整数 |
| total_fee | 是 | 实付金额，以分为单位，只能为整数 |
| coupon_fee | 否 | 代金券金额，代金券金额&lt;=订单金额，订单金额 - 代金券金额 = 现金支付金额 |
| fee_type | 否 | 货币类型，符合 ISO 4217 标准的三位字母代码，默认人民币：CNY |
| attach | 否 | 商家数据包，原样返回 |
| bank_type | 否 | 付款银行 |
| bank_billno | 否 | 银行订单号，若为第三方支付则为空 |
| time_end | 是 | 支付完成时间，格式为yyyyMMddHHmmss，如2009年12月25日9点10分10秒表示为20091225091010。时区为GMT+8 Beijing |
| nonce_str | 是 | 随机字符串 |
| trade_type | 是 | 交易类型 |
| promotion_detail | 否 | 营销详情，返回值为Json格式 |

**响应结果示例**

```json
{
    "state": "SUCCESS",
    "code": "10000",
    "trade_state": "SUCCESS",
    "msg": "SUCCESS",
    "mch_id": "00000001",
    "appid": "wx4da448cd29920000",
    "is_subscribe": "Y",
    "openid": "o4he1jo7fA1rIWTOOA3hDbGWc29w",
    "sub_appid": "wx4da448cd29920000",
    "sub_is_subscribe": "Y",
    "sub_openid": "o4he1jo7fA1rIWTOOA3hDbGWc29w",
    "transaction_id": "4200000334201905246610520000",
    "out_transaction_id": "4200000334201905246610520000",
    "out_trade_no": "T0020190524102840000",
    "base_fee": "4",
    "total_fee": "2",
    "coupon_fee": "2",
    "fee_type": "CNY",
    "bank_type": "CFT",
    "time_end": "20190524103044",
    "nonce_str": "1CQmxHpi2H62HsGg",
    "trade_type": "MICROPAY",
    "promotion_detail": "{\"promotion_detail\":[{\"promotion_id\":\"6348962444\",\"name\":\"维他减2分\",\"scope\":\"SINGLE\",\"type\":\"DISCOUNT\",\"amount\":2,\"activity_id\":\"9447213\",\"wxpay_contribute\":0,\"merchant_contribute\":2,\"other_contribute\":0,\"goods_detail\":[{\"goods_id\":\"CY00000000000\",\"quantity\":1,\"price\":2,\"discount_amount\":1,\"goods_remark\":\"单品券活动No.002\"},{\"goods_id\":\"CY00000000001\",\"quantity\":1,\"price\":2,\"discount_amount\":1,\"goods_remark\":\"单品券活动No.002\"}]}]}",
    "wx_mch_id": "1264300000",
    "wx_sub_mch_id": "1266500000",
    "sign": "00000000000000000000000000000000"
}
```

---

# 交易退款

**应用场景**

商户针对某一个已经成功支付的订单发起退款，操作结果在同一会话中同步返回。

**退款方式**

目前只支持原路返回退款

说明：退到银行卡则是非实时的，每个银行的处理速度不同，一般发起退款后1-3个工作日内到账。

同一笔单的部分退款需要设置相同的订单号和不同的 out_refund_no 。一笔退款失败后重新提交，要采用原来 的out_refund_no。总退款金额不能超过用户实际支付金额\(代金券金额不能退款\)

**退款限制**

商户在退款操作时应该注意退款限制，避免发起不会成功的退款请求，下面是主要的退款限制：

1. 在平台系统中，只要退款累计金额不超过交易单支付总额，一笔交易单可以多次退款，退款申请单号（退款接口中有此参数）唯一确定一次退款，而      不是交易单号确定一次退款。退款申请单号由商户生成，所以商户一定要保证退款申请单的唯一性。商家在退款过程中要特别注意，只有在能确定退      款失败的情况下，才能重新发起另一笔退款。
2. 目前大多数银行都支持全额退款和部分退款，但是也有少数银行不支持全额退款或部分退款，或者不支持退款。在这种情况下，商户可以与买家协调， 线下直接退款给买家。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">接口地址</td>
        <td>https://{BaseURL}/UnifiedPay/Gateway</td>
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
| method | 是 | refund | 接口名称，refund |
| agent_id | 是 | 13000000000000000 | 代理商编号 |
| pid | 是 | yunpos | 调用方产品名称 |
| version | 是 | 1.0 | 调用方版本号 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| paytype | 是 | WECHAT | 支付方式，详见参数规定 |
| mch_id | 是 | 00000001 | 超赢商户号 |
| out_trade_no | 否 | 1497769914931 | 商户系统内部的订单号，out_trade_no和transaction_id至少一个必填，同时存在时transaction_id优先 |
| transaction_id | 否 | 7551000001201706166172780576 | 平台单号, out_trade_no和transaction_id至少一个必填，同时存在时transaction_id优先 |
| out_refund_no | 是 | TK-1497769914931-01 | 商户退款单号，32个字符内、可包含字母，确保在商户系统唯一。同个退款单号多次请求，平台当一个单处理，只会退一次款。如果出现退款不成功，请采用原退款单号重新发起，避免出现重复退款。 |
| total_fee | 是 | 1 | 订单应付金额，单位为分 |
| refund_fee | 是 | 1 | 申请退款金额，单位为分 |
| op_user_id | 是 | 00000001 | 操作员帐号，默认为商户号 |

**请求参数示例**

> method=refund&agent_id=13000000000000000&version=1.0&pid=yunpos&paytype=WECHAT&mch_id=00000001&out_trade_no=1497769914931&out_refund_no=TK-1497769914931-01&sign=00000000000000000000000000000000

**响应结果**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| code | 是 | 状态码 ，详见参数规定 |
| msg | 否 | 返回信息 |
| trade_state | 否 | 交易状态，详见参数规定 |
| sign | 是 | 响应结果的签名串 |

以下字段在state和trade_state都为SUCCESS的时候有返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| mch_id | 是 | 超赢商户号 |
| out_trade_no | 是 | 商户系统内部的定单号，32个字符内、可包含字母 |
| transaction_id | 是 | 平台交易号 |
| out_transaction_id | 是 | 第三方退款单号 |
| out_refund_no | 是 | 商户退款单号 |
| refund_id | 是 | 平台退款单号 |
| refund_channel | 否 | 退款渠道，ORIGINAL—原路退款，默认 |
| base_fee | 是 | 订单应付金额，单位为分 |
| total_fee | 是 | 订单实付金额，单位为分 |
| base_refund_fee | 是 | 申请退款金额，单位为分 |
| refund_fee | 是 | 实际退款金额，单位为分 |
| coupon_refund_fee | 是 | 代金券退款金额 &lt;= 退款金额， 退款金额-代金券退款金额为现金 |
| nonce_str | 是 | 随机字符串 |

**响应结果示例**

```json
{
    "state": "SUCCESS",
    "code": "10000",
    "trade_state": "SUCCESS",
    "msg": "SUCCESS",
    "mch_id": "00000001",
    "out_trade_no": "T0020190517145341153",
    "transaction_id": "4200000330201905173095298659",
    "out_transaction_id": "4200000330201905173095298659",
    "out_refund_no": "TKT0020190517145341153-B",
    "refund_id": "50000300412019051709584177333",
    "base_fee": "8",
    "total_fee": "6",
    "base_refund_fee": "2",
    "refund_fee": "1",
    "coupon_refund_fee": "1",
    "nonce_str": "78GTQmdylSxwFXxE",
    "sign": "00000000000000000000000000000000"
}
```

---

# 退款查询

**应用场景**

提交退款申请后， 通过调用该接口查询退款状态。 银行卡支付的退款有一定延时， 请在 3 个工作日后重新查询退款状态。

**注意**

1. 如果单个支付订单部分退款次数超过20次请使用平台退款单号查询
2. 若存在多条退款单时，退款状态请以refund_list中refund_status字段为准

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">接口地址</td>
        <td>https://{BaseURL}/UnifiedPay/Gateway</td>
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
| method | 是 | refundquery | 接口名称，refundquery |
| agent_id | 是 | 13000000000000000 | 代理商编号 |
| pid | 是 | yunpos | 调用方产品名称 |
| version | 是 | 1.0 | 调用方版本号 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| paytype | 是 | WECHAT | 支付方式，详见参数规定 |
| mch_id | 是 | 00000001 | 超赢商户号 |
| out_refund_no | 否 | TK-1497769914931-01 | 商户退款单号，32个字符内、可包含字母,确保在商户系统唯一。 |
| refund_id | 否 | 7551000001201706215157548269 | 平台退款单号关于refund_id、out_refund_no必填一个， 如果同时存在优先级为：refund_id &gt; out_refund_no；特殊说明：如果是支付宝，refund_id、out_refund_no必填其中一个。 |

**请求参数示例**

> method=refundquery&agent_id=13000000000000000&version=1.0&pid=yunpos&paytype=WECHAT&mch_id=00000001&out_refund_no=TKT0020190524102840000&sign=00000000000000000000000000000000

**响应结果**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| code | 是 | 状态码 ，详见参数规定 |
| msg | 否 | 返回信息 |
| trade_state | 否 | 交易状态，详见参数规定 |
| sign | 是 | 响应结果的签名串 |

以下字段在state和trade_state都为SUCCESS的时候有返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| mch_id | 是 | 超赢商户号 |
| appid | 否 | 调用接口提交的公众账号ID |
| is_subscribe | 否 | 用户是否关注公众账号，仅在公众账号类型支付有效，取值范围：Y或N;Y-关注;N-未关注 |
| openid | 否 | 用户在商户 appid 下的唯一标识 |
| sub_appid | 否 | 调用接口提交的子商户公众账号ID |
| sub_is_subscribe | 否 | 用户是否关注子公众账号，仅在公众账号类型支付有效，取值范围：Y或N;Y-关注;N-未关注 |
| sub_openid | 否 | 子商户appid下用户唯一标识，如需返回则请求时需要传sub_appid |
| transaction_id | 是 | 平台交易号 |
| out_transaction_id | 是 | 第三方订单号 |
| out_trade_no | 是 | 商户系统内部的定单号，32个字符内、可包含字母 |
| refund_count | 是 | 退款笔数 |
| base_refund_fee_summary | 是 | 申请退款汇总金额，以分为单位，只能为整数 |
| refund_fee_summary | 是 | 实际退款汇总金额，以分为单位，只能为整数 |
| refund_list | 是 | 退款单集合 |
| nonce_str | 是 | 随机字符串 |
| wx_mch_id | 否 | 微信服务商商户号 |
| wx_sub_mch_id | 否 | 微信子商户号 |

以下字段在refund_list中返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| serial_no | 是 | 退款序号，按退款申请时间升序排列 |
| refund_id | 是 | 平台退款单号 |
| out_refund_id | 是 | 第三方退款单号 |
| out_refund_no | 是 | 商户退款单号 |
| refund_channel | 否 | 退款渠道，ORIGINAL—原路退款，默认 |
| base_refund_fee | 是 | 当次退款申请金额，以分为单位，只能为整数 |
| refund_fee | 是 | 当次实际退款金额，以分为单位，只能为整数 |
| coupon_refund_fee | 否 | 代金券退款金额 &lt;= 退款金额， 退款金额 - 代金券退款金额为现金 |
| refund_status | 是 | 退款状态：SUCCESS—退款成功；FAIL—退款失败；PROCESSING—退款处理中；NOTSURE—未确定， 需要商户原退款单号重新发起；CHANGE—转入代发，退款到银行发现用户的卡作废或者冻结了，导致原路退款银行卡失败，资金回流到商户的现金帐号，需要商户人工干预，通过线下或者平台转账的方式进行退款。 |
| refund_time | 否 | 退款时间，格式为yyyyMMddHHmmss，如2009年12月25日9点10分10秒表示为20091225091010。时区为GMT+8 Beijing |

**响应结果示例**

```json
{
    "state": "SUCCESS",
    "code": "10000",
    "trade_state": "SUCCESS",
    "msg": "SUCCESS",
    "mch_id": "00000001",
    "appid": "wx4da448cd29920000",
    "transaction_id": "4200000334201905246610520000",
    "out_transaction_id": "4200000334201905246610520000",
    "out_trade_no": "T0020190524102840000",
    "base_refund_fee_summary": "4",
    "refund_fee_summary": "2",
    "refund_count": "1",
    "refund_list": "[{\"serial_no\":\"0\",\"refund_id\":\"50000000482019052409653860000\",\"out_refund_id\":\"50000000482019052409653860000\",\"out_refund_no\":\"TKT0020190524102840000\",\"base_refund_fee\":\"4\",\"refund_fee\":\"2\",\"coupon_refund_fee\":\"2\",\"refund_status\":\"SUCCESS\",\"refund_channel\":\"ORIGINAL\",\"refund_time\":\"2019-05-24 11:11:33\"}]",
    "nonce_str": "DjRzpkdtpM0Sl6HW",
    "wx_mch_id": "1264300000",
    "wx_sub_mch_id": "1266500000",
    "sign": "00000000000000000000000000000000"
}
```

---

# 交易撤销

**应用场景**

当支付返回失败，或收银系统超时需要取消交易，可以调用该接口。接口逻辑 ： 支付失败的关单，支付成功的撤销支付。注意：5分钟的订单才可以撤销，其他正常支付的单如需实现相同功能请调用退款接口。

调用支付接口后请勿立即调用撤销订单接口，建议支付后至少15s后再调用撤销订单接口。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">接口地址</td>
        <td>https://{BaseURL}/UnifiedPay/Gateway</td>
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
| method | 是 | cancel | 接口名称 |
| agent_id | 是 | 13000000000000000 | 代理商编号 |
| pid | 是 | yunpos | 调用方产品名称 |
| version | 是 | 1.0 | 调用方版本号 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| paytype | 是 | WECHAT | 支付方式，详见参数规定 |
| mch_id | 是 | 00000001 | 超赢商户号 |
| out_trade_no | 是 | 1497769914931 | 商户系统内部的订单号 ,5到32个字符、 只能包含字母数字或者下划线，区分大小写，确保在商户系统唯一 |
| op_user_id | 是 | 00000001 | 操作员帐号 |

**请求参数示例**

> method=cancel&agent_id=13000000000000000&version=1.0&pid=yunpos&paytype=WECHAT&mch_id=00000001&out_trade_no=1497769914931&op_user_id=yzq&sign=00000000000000000000000000000000

**响应结果**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| code | 是 | 状态码 ，详见参数规定 |
| msg | 否 | 返回信息 |
| trade_state | 否 | 交易状态，详见参数规定 |
| sign | 是 | 响应结果的签名串 |

以下字段在state和trade_state都为SUCCESS的时候有返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| mch_id | 是 | 超赢商户号 |
| nonce_str | 是 | 随机字符串 |
| wx_mch_id | 否 | 微信服务商商户号 |
| wx_sub_mch_id | 否 | 微信子商户号 |

**响应结果示例**

```json
{
    "state": "SUCCESS",
    "code": "10000",
    "trade_state": "SUCCESS",
    "msg": "SUCCESS",
    "mch_id": "00000001",
    "nonce_str": "f1625e94362d4d82aafcc5fc9d1f9325",
    "wx_mch_id": "1264300000",
    "wx_sub_mch_id": "1266500000",
    "sign": "00000000000000000000000000000000"
}
```
