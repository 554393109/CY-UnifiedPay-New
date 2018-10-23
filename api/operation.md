<b style="font-size: 2em">运维管理</b>

---

# 注册超赢虚拟商户

**应用场景**

该接口提供第三方接入使用我方聚合支付业务时注册成超赢虚拟商户功能。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">接口地址</td>
        <td>https://{BaseURL}/UnifiedPay/Mch_Reg</td>
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
| version | 否 | 1.0 | 调用方版本号 |
| pid | 否 | yunpos | 调用方产品名称 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| url_path | 否 | <https://api.domain.com/> | 接口地址，以**斜杠结尾** |
| - | 是 | - | 具体参数，联调时请联系技术支持获取 |

**请求参数示例**

> agent_id=13000000000000001key1=aaa&key2=bbb&sign=00000000000000000000000000000000

**响应结果**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| code | 是 | 状态码 ，详见参数规定 |
| msg | 否 | 返回信息 |
| sign | 是 | 响应结果的签名串 |

以下字段在state为SUCCESS，code为10000的时候有返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| mch_id | 是 | 超赢商户号 |

**响应结果示例**

```json
{
    "state": "SUCCESS",
    "code": "10000",
    "msg": "SUCCESS",
    "mch_id": "00000001",
    "nonce_str": "f1625e94362d4d82aafcc5fc9d1f9325",
    "sign": "00000000000000000000000000000000"
}
```

---

# 下发获取超赢商户号验证短信

**应用场景**

该接口提供使用手机号获取短信验证码功能。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">接口地址</td>
        <td>https://{BaseURL}/Mch/GetMchSMSValid</td>
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
| version | 否 | 1.0 | 调用方版本号 |
| pid | 否 | yunpos | 调用方产品名称 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :---- | :--- |
| mobile | 是 | 13800000000 | 手机号 |

**请求参数示例**

> agent_id=13000000000000001&mobile=13800000000&sign=00000000000000000000000000000000

**响应结果**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| code | 是 | 验证码有效时长 单位：分钟 |
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

# 获取超赢商户号

**应用场景**

该接口提供获取超赢商户号功能。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">接口地址</td>
        <td>https://{BaseURL}/Mch/GetMchId</td>
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
| version | 否 | 1.0 | 调用方版本号 |
| pid | 否 | yunpos | 调用方产品名称 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| mobile | 否 | 13800000000 | 手机号。（手机号+验证码）或（用户名+用户密码）不能同时为空 |
| valid | 否 | 1234 | 验证码。（手机号+验证码）或（用户名+用户密码）不能同时为空 |
| username | 否 | 13800000000 | 用户名。（手机号+验证码）或（用户名+用户密码）不能同时为空 |
| password | 否 | 12345678 | 用户密码。（手机号+验证码）或（用户名+用户密码）不能同时为空 |

**请求参数示例**

> agent_id=13000000000000001&mobile=13800000000&valid=1234&sign=00000000000000000000000000000000

**响应结果**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| code | 是 | 状态码 ，详见参数规定 |
| msg | 否 | 返回信息 |
| sign | 是 | 响应结果的签名串 |

以下字段在state为SUCCESS，code为10000的时候有返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| mch_id | 是 | 超赢商户号 |
| mch_trade_code | 是 | 商户交易码，大小写敏感 |
| mch_full_name | 是 | 商户全称 |
| mch_short_name | 是 | 商户简称 |
| mch_state | 是 | 商户状态。0-待审核、20-启用、30-停用 |

**响应结果示例**

```json
{
    "state": "SUCCESS",
    "code": "10000",
    "msg": "SUCCESS",
    "mch_id": "f0000000000000001",
    "mch_trade_code": "f6742168cc",
    "mch_full_name": "广州市超赢信息科技有限公司",
    "mch_short_name": "超赢科技",
    "mch_state": "20",
    "sign": "00000000000000000000000000000000"
}
```
