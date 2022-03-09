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
