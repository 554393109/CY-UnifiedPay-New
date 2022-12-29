<b style="font-size: 2em">运维管理</b>

---

# 下发获取超赢商户号验证短信

**应用场景**

该接口提供使用手机号获取短信验证码功能。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td class="tb-head">接口地址</td>
        <td>https://api.storepos.cn/Mch/GetMchSMSValid</td>
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
        <td>代理商密钥</td>
    </tr>
</table>

**公共请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| agent_id | 是 | 13000000000000000 | 代理商编号 |
| pid | 是 | yunpos | 调用方产品名称 |
| version | 是 | 1.0 | 调用方版本号 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :---- | :--- |
| mobile | 是 | 13800000000 | 手机号 |

**请求参数示例**

> agent_id=13000000000000000&version=1.0&pid=yunpos&mobile=13800000000&sign=00000000000000000000000000000000

**响应结果**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| code | 否 | 验证码有效时长 单位：分钟 |
| msg | 否 | 返回信息 |
| sign | 是 | 响应结果的签名串 |

**响应结果示例**

```json
{
    "state": "SUCCESS",
    "code": "20",
    "msg": "短信验证码已发送",
    "sign": "00000000000000000000000000000000"
}
```

---

# 小程序用户code登录

**应用场景**

该接口提供获取超赢商户基础信息功能。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td class="tb-head">接口地址</td>
        <td>https://api.storepos.cn/Open/WXA_Code2Session</td>
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
        <td>代理商密钥</td>
    </tr>
</table>

**公共请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| agent_id | 是 | 13000000000000000 | 代理商编号 |
| pid | 是 | yunpos | 调用方产品名称 |
| version | 是 | 1.0 | 调用方版本号 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| appid | 是 | wx4da448cd29920000 | 小程序appId |
| js_code | 是 | 023jh17A0TIixd1ql75A0aLc7A0jabcd | 登录时获取的code |

**请求参数示例**

> agent_id=13000000000000000&version=1.0&pid=yunpos&appid=wx4da448cd29920000&js_code=023jh17A0TIixd1ql75A0aLc7A0jabcd&sign=00000000000000000000000000000000

**响应结果**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| code | 否 | 状态码 ，详见参数规定 |
| msg | 否 | 返回信息 |
| sign | 是 | 响应结果的签名串 |

以下字段在state为SUCCESS，code为10000的时候有返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| openid | 是 | 用户唯一标识 |
| session_key | 是 | 会话密钥 |
| expires_in | 是 | 有效期 |
| unionid | 否 | 用户在开放平台的唯一标识符，在满足UnionID下发条件的情况下会返回 |

**响应结果示例**

```json
{
    "state": "SUCCESS",
    "code": "10000",
    "msg": "SUCCESS",
    "openid": "oDY_z0OgEhAdLJ8cLTVd8nGCj-_M",
    "session_key": "+rL9Uq02dbP85itLOdz94w==",
    "expires_in": 7200
}
```

---

# 微信APIv3请求代签名

**应用场景**

该接口提供使用商户所属通道微信服务商证书进行请求代签名，返回该请求的Header["Authorization"]供业务方调用微信接口功能。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td class="tb-head">接口地址v1</td>
        <td colspan="2">https://api.storepos.cn/Open/GetWechatV3AuthInfo</td>
    </tr>
    <tr>
        <td class="tb-head">接口地址v2</td>
        <td colspan="2">https://api.storepos.cn/v2/Open/GetWechatV3AuthInfo</td>
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
        <td>v1 - 代理商密钥</td>
        <td>v2 - 商户密钥</td>
    </tr>
</table>

**公共请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| agent_id | 是 | 13000000000000000 | 代理商编号 |
| pid | 是 | yunpos | 调用方产品名称 |
| version | 是 | 1.0 | 调用方版本号 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| mch_id | 是 | 00000001 | 超赢商户号 |
| method | 是 | POST | 请求方法 |
| path | 是 | /v3/marketing/shopping-receipt/shoppingreceipts | 请求URL |
| body | 否 | {"transaction_id":"42000000000001"} | 请求报文主体（请求方法为GET时，报文主体为空） |

**请求参数示例**

> agent_id=13000000000000000&version=1.0&pid=yunpos&mch_id=00000001&method=POST&path=/v3/marketing/shopping-receipt/shoppingreceipts&body={"transaction_id":"42000000000001"}&sign=00000000000000000000000000000000

**响应结果**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| code | 否 | 状态码 ，详见参数规定 |
| msg | 否 | 返回信息 |
| sign | 是 | 响应结果的签名串 |

以下字段在state为SUCCESS，code为10000的时候有返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| AuthInfo | 是 | 认证信息 |

认证信息AuthInfo包含字段

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| method | 是 | 请求方法（原样返回） |
| path | 是 | 请求URL（原样返回） |
| body | 是 | 请求报文主体（原样返回） |
| mchid | 是 | 微信服务商商户号 |
| timestamp | 是 | 签名时间戳 |
| nonce | 是 | 签名随机串 |
| sign_data | 是 | 签名原文 |
| authorization | 是 | 认证信息字串 |
| serial_no | 是 | 服务商证书序列号 |
| wechat_serial_no | 否 | 微信平台证书序列号 |

**响应结果示例**

```json
{
    "state": "SUCCESS",
    "code": "10000",
    "msg": "SUCCESS",
    "ReqId": "zkcdmszqfeahpyatylnejj2i",
    "AuthInfo": {
        "method": "POST",
        "path": "/v3/marketing/shopping-receipt/shoppingreceipts",
        "body": "{\"transaction_id\":\"4200001691202212164552827236\",\"transaction_sub_mchid\":\"463913005\",\"openid\":\"o4he1jo7fA1rIWTOOA3hDbGWc29w\",\"sha256\":\"A08B06FAB9215872BAD51EA1862B4ED44DAD42D26815C38DC77EFFB98295C305\"}",
        "mchid": "438457393",
        "timestamp": "1672297950",
        "nonce": "8314668a545a4d73bc5919a5c6aa7f31",
        "sign_data": "POST\n/v3/marketing/shopping-receipt/shoppingreceipts\n1672297950\n8314668a545a4d73bc5919a5c6aa7f31\n{\"transaction_id\":\"4200001691202212164552827236\",\"transaction_sub_mchid\":\"463913005\",\"openid\":\"o4he1jo7fA1rIWTOOA3hDbGWc29w\",\"sha256\":\"A08B06FAB9215872BAD51EA1862B4ED44DAD42D26815C38DC77EFFB98295C305\"}\n",
        "authorization": "WECHATPAY2-SHA256-RSA2048 mchid=\"438457393\",nonce_str=\"8314668a545a4d73bc5919a5c6aa7f31\",timestamp=\"1672297950\",serial_no=\"75213FA443604051FB64C089B785206D47F2CCB7\",signature=\"DSQn5V++CTDm/MMLVOVcz4M4Pkp7lvs0dcL57FODcSPwA7Td/XzfmcYlQc8Cpv/Avmpc8WKU//+iU3ifQDU4rc6u7HcVL9bhVPSnXvFQRS+p9uYZ0cE4Oj/+Z5GXeAt0tmtCzF34PsRUN7cRkYzY5PEujSOjZdGMxfmmyGl4UBiHsTxBo9lOKq4qNIZYfSibbAiKxD7hC7uW4rZ271PZXrEv1sd2R8GjGtzO3m3lBwSElGUwdVUvb/ZMeb/ytpo37Fx50Oz0KUIOxuc3tzohjaDAzN2rzZtLWIBoHAyuvjGK7UnEXizgZM2xRBlMIYiEOneihdacYA/TIwoCJl2oGQ==\"",
        "serial_no": "75213FA443604051FB64C089B785206D47F2CCB7",
        "wechat_serial_no": "29FAD77ADF7D06360EC340ED8117C6C6BC368C17"
    }
}
```

---
