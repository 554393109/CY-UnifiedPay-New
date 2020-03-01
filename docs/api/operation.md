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
| agent_id | 是 | 13000000000000000 | 代理商编号 |
| version | 是 | 1.0 | 调用方版本号 |
| pid | 是 | yunpos | 调用方产品名称 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| - | 是 | - | 具体参数，联调时请联系技术支持获取 |

**请求参数示例**

> agent_id=13000000000000000&version=1.0&pid=yunpos&key1=aaa&key2=bbb&sign=00000000000000000000000000000000

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
| agent_id | 是 | 13000000000000000 | 代理商编号 |
| version | 是 | 1.0 | 调用方版本号 |
| pid | 是 | yunpos | 调用方产品名称 |
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
| agent_id | 是 | 13000000000000000 | 代理商编号 |
| version | 是 | 1.0 | 调用方版本号 |
| pid | 是 | yunpos | 调用方产品名称 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| mobile | 否 | 13800000000 | 手机号。（手机号+验证码）或（用户名+用户密码）不能同时为空 |
| valid | 否 | 1234 | 验证码。（手机号+验证码）或（用户名+用户密码）不能同时为空 |
| username | 否 | 13800000000 | 用户名。（手机号+验证码）或（用户名+用户密码）不能同时为空 |
| password | 否 | 12345678 | 用户密码。（手机号+验证码）或（用户名+用户密码）不能同时为空 |

**请求参数示例**

> agent_id=13000000000000000&version=1.0&pid=yunpos&mobile=13800000000&valid=1234&sign=00000000000000000000000000000000

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

---

# 获取超赢商户微信子商户号

**应用场景**

该接口提供获取超赢商户微信子商户号功能。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">接口地址</td>
        <td>https://{BaseURL}/Open/GetPartnerId</td>
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
| agent_id | 是 | 13000000000000000 | 代理商编号 |
| version | 是 | 1.0 | 调用方版本号 |
| pid | 是 | yunpos | 调用方产品名称 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| mch_id | 是 | 00000001 | 超赢商户号 |

**请求参数示例**

> agent_id=13000000000000000&version=1.0&pid=yunpos&mch_id=00000001&sign=00000000000000000000000000000000

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
| partner_list | 是 | 超赢商户微信子商户信息列表 |

以下字段在partner_list中返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| pay_channel | 是 | 所属支付通道编码 |
| appid | 否 | 公众号AppId |
| partner_id | 否 | 微信子商户号，在微信方未报备通过则为空 |

**响应结果示例**

```json
{
    "state": "SUCCESS",
    "code": "10000",
    "msg": "SUCCESS",
    "mch_id": "00000001",
    "partner_list": "[{\"pay_channel\":\"CEB\",\"partner_id\":\"257012345\",\"appid\":\"wx2a8d87e234100000\"},{\"pay_channel\":\"CCB\",\"partner_id\":\"257012346\",\"appid\":\"wx2a8d87e234100000\"}]",
    "sign": "00000000000000000000000000000000"
}
```

---

# 获取超赢商户基础信息

**应用场景**

该接口提供获取超赢商户基础信息功能。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">接口地址</td>
        <td>https://{BaseURL}/Open/GetMchInfo</td>
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
| agent_id | 是 | 13000000000000000 | 代理商编号 |
| version | 是 | 1.0 | 调用方版本号 |
| pid | 是 | yunpos | 调用方产品名称 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| mch_id | 是 | 00000001 | 超赢商户号 |

**请求参数示例**

> agent_id=13000000000000000&version=1.0&pid=yunpos&mch_id=00000001&sign=00000000000000000000000000000000

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
| FullName | 是 | 商户全称 |
| ShortName | 是 | 商户简称 |

**响应结果示例**

```json
{
    "state": "SUCCESS",
    "code": "10000",
    "msg": "SUCCESS",
    "mch_id": "00000001",
    "FullName": "测试商户全称",
    "ShortName": "测试商户简称",
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
        <td style="width: 100px; text-align: center; font-weight: 700;">接口地址</td>
        <td>https://{BaseURL}/Open/WXA_Code2Session</td>
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
| agent_id | 是 | 13000000000000000 | 代理商编号 |
| version | 是 | 1.0 | 调用方版本号 |
| pid | 是 | yunpos | 调用方产品名称 |
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
| code | 是 | 状态码 ，详见参数规定 |
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

# 超赢商户微信支付配置新增

**应用场景**

该接口为超赢商户配置公众号功能。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">接口地址</td>
        <td>https://{BaseURL}/open/wx_addsubdevconfig</td>
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
| agent_id | 是 | 13000000000000000 | 代理商编号 |
| version | 是 | 1.0 | 调用方版本号 |
| pid | 是 | yunpos | 调用方产品名称 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| appid | 否 | wx4da448cd29920000 | 支付的公众号APPID，可以绑定商户或服务商公众号、小程序、APP支付等对应的APPID；该字段视支付接口中是否传sub_appid而定，如有疑惑请联系超赢运营人员；该字段每次调用仅支持传送1个APPID |
| jsapi_path | 否 | http:/a.com/pay/ | 商户公众号JS API支付授权目录，要求符合URI格式规范；多个目录间请以英标分号【;】分割 |
| subscribe_appid | 否 | wx4da448cd29920000 | 推荐关注的公众号APPID，该字段每次调用仅支持传送1个APPID；subscribe_appid和receipt_appid二选一 |
| receipt_appid | 否 | wx4da448cd29920000 | 支付凭证推荐小程序APPID，该字段每次调用仅支持传送1个APPID；subscribe_appid和receipt_appid二选一 |

**请求参数示例**

> agent_id=13000000000000000&version=1.0&pid=yunpos&appid=wx4da448cd29920000&jsapi_path=http:/a.com/pay/;http:/b.com/pay/&subscribe_appid=wx4da448cd29920000&sign=00000000000000000000000000000000

**响应结果**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| code | 是 | 状态码 ，详见参数规定 |
| msg | 否 | 返回信息 |
| sign | 是 | 响应结果的签名串 |

**响应结果示例**

```json
{
    "state": "SUCCESS",
    "code": "10000",
    "msg": "SUCCESS",
    "sign": "00000000000000000000000000000000",
}
```

**配置规则重要说明**

* API只支持新增配置，不支持修改，如需要修改请联系超赢运营人员手工删除后重新配置。
* 可以绑定特约商户或渠道公司主体一致的公众号、小程序、开放平台应用的APPID。
* 每个商户最多自定义配置2个支付目录，2个支付公众号和推荐关注。
* 每个商户APPID可以配置相同或不同的推荐关注公众号（前提主体需一致）。
* 每个商户只允许APPID（A）关注一个公众号，不允许同时关注多个不同公众号。
* 不同商户APPID（A、B）允许关注同一个公众号。
* 配置关注后隔30天才能重新修改。
* 微信支持配置【商户主体】公众号或【服务商主体】公众号，可以使用服务商主体（或商户主体）公众号来支付时，实现关注商户主体（或服务商主体）公众号。注：现仅支持关注商户主体公众号。

**应用示例（A和B可代表服务商主体或商户主体的公众号）**

> **示例1：商户交易时实现用A支付关注A**  
> ①一次请求appid和subscribe_appid两个参数同时配置特约商户APPID（A）
>
> **示例2：商户交易时实现用A支付关注B**  
> ①一次请求appid和subscribe_appid两个参数分别对应配置APPID（B）和APPID（A）
>
> **示例3：商户交易时实现用A支付时关注A，同时实现用B支付时关注A**  
> ①一次请求appid和subscribe_appid两个参数同时配置特约商户APPID（A）  
> ②一次请求appid和subscribe_appid两个参数分别对应配置APPID（B）和APPID（A）
