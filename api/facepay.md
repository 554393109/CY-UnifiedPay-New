<b style="font-size: 2em">刷脸支付</b>

---

# 获取SDK调用凭证

**应用场景**

获取SDK调用凭证。

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
| method | 是 | getfaceauth | 接口名称，getfaceauth |
| agent_id | 是 | 13000000000000000 | 代理商编号 |
| pid | 是 | yunpos | 调用方产品名称 |
| version | 是 | 1.0 | 调用方版本号 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| paytype | 是 | WECHAT | 支付方式，详见参数规定 |
| mch_id | 是 | 00000001 | 超赢商户号 |
| store_id | 是 | test_store_01 | 门店编号 |
| store_name | 是 | 测试门店01 | 门店名称 |
| device_id | 是 | 00000001 | 终端设备编号 |
| rawdata | 是 | 00000001 | 初始化数据 |

**请求参数示例**

> method=getfaceauth&agent_id=13000000000000000&paytype=WECHAT&mch_id=00000001&version=1.0&pid=yunpos&store_id=test_store_01&store_name=%E6%B5%8B%E8%AF%95%E9%97%A8%E5%BA%9701&device_id=CYW00000000000000000000&rawdata=eNPJNgR26U88XXXXXXXXX&sign=00000000000000000000000000000000

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
| appid | 是 | 服务商appid |
| sub_appid | 否 | 子商户sub_appid(服务商模式) |
| channel_mch_id | 是 | 服务商商户号 |
| sub_mch_id | 否 | 子商户号(服务商模式) |
| authinfo | 是 | SDK调用凭证 |
| expires_in | 是 | authinfo的有效时间，单位秒。例如：3600。在有效时间内, 对于同一台终端设备，相同的参数的前提下(如：相同的公众号、商户号、 门店编号等），可以用同一个authinfo，多次调用SDK的getWxpayfaceCode接口。 |
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
    "appid": "wx2b029c08a6232582",
    "channel_mch_id": "1900007071",
    "authinfo": "IGJSUOkyjSthQ0nWkI49U6LGhiJbTpr2KkMOiD2kb16DRmyySXXXXXX",
    "expires_in": "3600",
    "nonce_str": "k1MErGrCODf06uiv",
    "wx_mch_id": "1264300000",
    "wx_sub_mch_id": "1266500000",
    "sign": "00000000000000000000000000000000"
}
```

---

# 提交支付

**应用场景**

刷脸支付可用于线下各个场景，尤其对于不方便拿出手机支付等场景尤为方便。在支持刷脸支付的机具上选择使用微信刷脸支付付款，只需刷一下脸然后输入本人微信绑定的手机号即可完成付款，方便快捷又安全。

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
| method | 是 | facepay | 接口名称，facepay |
| agent_id | 是 | 13000000000000000 | 代理商编号 |
| pid | 是 | yunpos | 调用方产品名称 |
| version | 是 | 1.0 | 调用方版本号 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| paytype | 是 | WECHAT | 支付方式，详见参数规定 |
| mch_id | 是 | 00000001 | 超赢商户号 |
| openid | 是 | 00000001 | 用户标识 |
| out_trade_no | 是 | 1497769914931 | 商户系统内部的订单号 ,5到32个字符、 只能包含字母数字或者下划线，区分大小写，确保在商户系统唯一 |
| device_info | 否 | 013467007045764 | 终端设备号，商户自定义。特别说明：对于QQ钱包支付，此参数必传，否则会报错。 |
| body | 是 | image形象店-深圳腾大- QQ公仔 | 商品描述 |
| attach | 否 | 说明 | 商户附加信息，可做扩展参数 |
| total_fee | 是 | 1 | 总金额，以分为单位，只能为整数 |
| mch_create_ip | 否 | 114.114.114.114 | 调用支付API的机器IP |
| face_code | 是 | 120061098828009406 | 人脸凭证 |
| op_user_id | 否 | 00000001 | 操作员帐号，默认为商户号 |
| op_shop_id | 否 | md_001 | 门店编号 |
| op_device_id | 否 | device_01 | 设备编号 |
| goods_tag | 否 | CY_PROMOTION_001 | 订单优惠标记，用于优惠券或者满减使用 |
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

> method=facepay&agent_id=13000000000000000&paytype=WECHAT&mch_id=00000001&version=1.0&pid=yunpos&out_trade_no=1497769914931&face_code=123123123&body=%E8%B6%85%E8%B5%A2%E6%94%AF%E4%BB%98&total_fee=4&goods_tag=CY_PROMOTION_001&goods_detail=[{"goods_id":"CY000000","goods_name":"促销单品-CY00000000000","quantity":1,"price":2},{"goods_id":"CY000001","goods_name":"促销单品-CY00000000001","quantity":1,"price":2}]&sign=00000000000000000000000000000000

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
| base_fee | 是 | 应付金额，以分为单位，只能为整数 |
| total_fee | 是 | 实付金额，以分为单位，只能为整数 |
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
    "appid": "wx2b029c08a6232582",
    "is_subscribe": "N",
    "openid": "oBmIts3wbluEIYfp6zDgBWsC9Evs",
    "transaction_id": "4200000233201812272744871942",
    "out_transaction_id": "4200000233201812272744871942",
    "out_trade_no": "1545890307",
    "base_fee": "4",
    "total_fee": "2",
    "fee_type": "CNY",
    "bank_type": "CFT",
    "time_end": "20181227140034",
    "nonce_str": "k1MErGrCODf06uiv",
    "promotion_detail": "{\"promotion_detail\":[{\"promotion_id\":\"6348962444\",\"name\":\"维他减2分\",\"scope\":\"SINGLE\",\"type\":\"DISCOUNT\",\"amount\":2,\"activity_id\":\"9447213\",\"wxpay_contribute\":0,\"merchant_contribute\":2,\"other_contribute\":0,\"goods_detail\":[{\"goods_id\":\"CY00000000000\",\"quantity\":1,\"price\":2,\"discount_amount\":1,\"goods_remark\":\"单品券活动No.002\"},{\"goods_id\":\"CY00000000001\",\"quantity\":1,\"price\":2,\"discount_amount\":1,\"goods_remark\":\"单品券活动No.002\"}]}]}",
    "wx_mch_id": "1264300000",
    "wx_sub_mch_id": "1266500000",
    "sign": "00000000000000000000000000000000"
}
```
