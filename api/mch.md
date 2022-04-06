<b style="font-size: 2em">商户</b>

---

# 注册超赢虚拟商户

**应用场景**

该接口提供第三方接入使用我方聚合支付业务时注册成超赢虚拟商户功能。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td class="tb-head">接口地址</td>
        <td>https://api.storepos.cn/UnifiedPay/Mch_Reg</td>
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
| - | 是 | - | 具体参数，联调时请联系技术支持获取 |

**请求参数示例**

> agent_id=13000000000000000&version=1.0&pid=yunpos&key1=aaa&key2=bbb&sign=00000000000000000000000000000000

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

# 获取超赢商户号

**应用场景**

该接口提供获取超赢商户号功能。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td class="tb-head">接口地址</td>
        <td>https://api.storepos.cn/Mch/GetMchId</td>
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
| code | 否 | 状态码 ，详见参数规定 |
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
        <td class="tb-head">接口地址v1</td>
        <td colspan="2">https://api.storepos.cn/Open/GetPartnerId</td>
    </tr>
    <tr>
        <td class="tb-head">接口地址v2</td>
        <td colspan="2">https://api.storepos.cn/v2/Open/GetPartnerId</td>
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

**请求参数示例**

> agent_id=13000000000000000&version=1.0&pid=yunpos&mch_id=00000001&sign=00000000000000000000000000000000

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

# 超赢商户微信支付配置新增

**应用场景**

该接口为超赢商户配置公众号功能。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td class="tb-head">接口地址v1</td>
        <td colspan="2">https://api.storepos.cn/open/wx_addsubdevconfig</td>
    </tr>
    <tr>
        <td class="tb-head">接口地址v2</td>
        <td colspan="2">https://api.storepos.cn/v2/open/wx_addsubdevconfig</td>
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
| code | 否 | 状态码 ，详见参数规定 |
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
> **示例3：商户交易时实现用A支付关注A，同时实现用A支付关注B**  
> ①一次请求appid和subscribe_appid两个参数同时配置特约商户APPID（A）  
> ②一次请求appid和subscribe_appid两个参数分别对应配置APPID（B）和APPID（A）

---

# 支付终端轮询商户配置

**应用场景**

该接口提供支付终端获取轮询商户配置功能（间隔5秒）。若返回配置地址，则将配置地址生成二维码供商户扫码进行配置。

**注意事项**

请求头User-Agent参数须携带固定值“CySoftPayBox”。

当state=FAIL，终止轮询并展示msg信息；

当state=SUCCESS，但无商户信息返回，且返回了配置地址，则将配置地址生成二维码并展示（当配置地址发生变更，需重新生成二维码），并间隔5秒继续轮询。

当state=SUCCESS，且商户信息非空，则保存并终止配置轮询。

**配置流程**

![配置流程](/assets/支付终端配置流程-20220406.png)

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td class="tb-head">接口地址</td>
        <td>https://api.storepos.cn/Mch/PayBoxConfGet</td>
    </tr>
    <tr>
        <td class="tb-head">提交方式</td>
        <td>GET</td>
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
| pid | 是 | CySoftPayBox | 调用方产品名称 |
| version | 是 | 1.0 | 调用方版本号 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| device_info | 是 | CySoftPayBox | 设备信息 |
| op_device_id | 是 | 000063066004189990000194 | 设备唯一编号 |

**请求参数示例**

> agent_id=13000000000000000&version=1.0&pid=CySoftPayBox&device_info=CySoftPayBox&op_device_id=000063066004189990000194&sign=00000000000000000000000000000000

**响应结果**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| code | 否 | 状态码 ，详见参数规定 |
| msg | 否 | 返回信息 |
| sign | 是 | 响应结果的签名串 |

以下字段在state为SUCCESS，且商户未配置时返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| conf_url | 是 | 配置地址（使用该地址生成二维码并展示） |

以下字段在state为SUCCESS，且商户已配置时有返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| mch_id | 是 | 超赢商户号 |
| mch_trade_code | 是 | 商户交易码，大小写敏感 |
| mch_full_name | 是 | 商户全称 |
| mch_short_name | 是 | 商户简称 |
| mch_state | 是 | 商户状态。0-待审核、20-启用、30-停用 |
| device_info | 是 | 设备信息 |
| op_device_id | 是 | 设备唯一编号 |
| op_shop_id | 否 | 门店编号【2022-04-06 新增】 |

**响应结果示例**

```json
// 返回配置地址
{
    "state": "SUCCESS",
    "conf_url": "https://domain.com/Mch/Conf",
    "sign": "00000000000000000000000000000000"
}

// 获取商户配置成功
{
    "state": "SUCCESS",
    "mch_id": "00000001",
    "mch_trade_code": "722e51cdcc",
    "mch_full_name": "商户全称",
    "mch_short_name": "商户简称",
    "mch_state": "20",
    "device_info": "CySoftPayBox",
    "op_device_id": "000063066004189990000194",
    "op_shop_id": "md_001",
    "sign": "00000000000000000000000000000000"
}
```

---

# 支付终端扫描商户二维码获取配置

**应用场景**

该接口提供支付终端扫描商户二维码获取配置功能。

**注意事项**

请求头User-Agent参数须携带固定值“CySoftPayBox”。

【参数取值】

从商户二维码扫描识别获取的链接有存在参数的情况，须判断链接中是否存在Query部分，进行拼接（**原Query参数也需要参与签名**）；

1.扫描商户二维码识别获取链接，如下：

> <https://qrpay.storepos.cn/qrpay/00000001?code_number=f0000000000000000&op_shop_id=id_shop&op_user_id=id_user>

2.从步骤1识别的链接中**获取path最末级值并定义为参数code_number**，并存入待签名集合M

```json
// 集合M
[
    { "code_number": "00000001" }
]
```

3.从步骤1识别的链接中获取原Query，解析并存入待签名集合M（**若集合A中有同名参数，则使用Query参数值覆盖集合A中同名参数的值**）

```json
// 集合M
[
    { "code_number": "f0000000000000000" },
    { "op_shop_id": "id_shop" },
    { "op_user_id": "id_user" }
]
```

4.请求参数存入待签名集合M；后续签名流程参照【[接口规则 - 签名验证](/rules.html#签名验证)】

```json
// 集合M
[
    { "agent_id": "13000000000000000" }
    { "code_number": "f0000000000000000" },
    { "device_info": "CySoftPayBox" }
    { "op_device_id": "000063066004189990000194" },
    { "op_shop_id": "id_shop" },
    { "op_user_id": "id_user" }
    { "pid": "CySoftPayBox" }
    { "version": "1.0" }
]
```

5.拼接上请求参数和签名，得到新链接，如下：

> <https://qrpay.storepos.cn/qrpay/00000001?code_number=f0000000000000000&op_shop_id=id_shop&op_user_id=id_user&agent_id=13000000000000000&device_info=CySoftPayBox&op_device_id=000063066004189990000194&pid=CySoftPayBox&version=1.0&sign=00000000000000000000000000000000>

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td class="tb-head">接口地址</td>
        <td>从商户二维码扫描识别获取（可能存在参数）</td>
    </tr>
    <tr>
        <td class="tb-head">提交方式</td>
        <td>GET</td>
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
| pid | 是 | CySoftPayBox | 调用方产品名称 |
| version | 是 | 1.0 | 调用方版本号 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| device_info | 是 | CySoftPayBox | 设备信息 |
| op_device_id | 是 | 000063066004189990000194 | 设备唯一编号 |
| code_number | 是 | - | 识别二维码获取path最末级值并定义为参数code_number |
| - | 是 | - | 识别二维码并解析出的参数 |

**请求参数示例**

> agent_id=13000000000000000&version=1.0&pid=CySoftPayBox&code_number=f0000000000000000&device_info=CySoftPayBox&op_device_id=000063066004189990000194&op_shop_id=门店01&sign=00000000000000000000000000000000

**响应结果**

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| state | 是 | 通讯状态，详见参数规定 |
| code | 否 | 状态码 ，详见参数规定 |
| msg | 否 | 返回信息 |
| sign | 是 | 响应结果的签名串 |

以下字段在state为SUCCESS，且商户已配置时有返回

| 字段名 | 必填 | 说明 |
| :--- | :---: | :--- |
| mch_id | 是 | 超赢商户号 |
| mch_trade_code | 是 | 商户交易码，大小写敏感 |
| mch_full_name | 是 | 商户全称 |
| mch_short_name | 是 | 商户简称 |
| mch_state | 是 | 商户状态。0-待审核、20-启用、30-停用 |
| device_info | 是 | 设备信息 |
| op_device_id | 是 | 设备唯一编号 |

**响应结果示例**

```json
{
    "state": "SUCCESS",
    "mch_id": "00000001",
    "mch_trade_code": "722e51cdcc",
    "mch_full_name": "商户全称",
    "mch_short_name": "商户简称",
    "mch_state": "20",
    "device_info": "CySoftPayBox",
    "op_device_id": "000063066004189990000194",
    "sign": "00000000000000000000000000000000"
}
```

---

# ~~支付终端展示商户配置二维码【弃用】~~

**应用场景**

由支付终端按传参规则构造链接，展示二维码供商户扫码配置交易参数，并在后台调用【[支付终端轮询商户配置](/mch.html#支付终端轮询商户配置)】接口进行轮询获取。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td class="tb-head">Url地址</td>
        <td>https://account.storepos.cn/Mch/PayBoxConf</td>
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
| pid | 是 | CySoftPayBox | 调用方产品名称 |
| version | 是 | 1.0 | 调用方版本号 |
| sign | 是 | 00000000000000000000000000000000 | 请求参数的签名串 |

**请求参数**

| 参数 | 必填 | 示例值 | 说明 |
| :--- | :---: | :--- | :--- |
| device_info | 是 | CySoftPayBox | 设备信息 |
| op_device_id | 是 | 000063066004189990000194 | 设备唯一编号 |

**二维码内容示例**

> <https://account.storepos.cn/Mch/PayBoxConf?agent_id=13000000000000000&version=1.0&pid=CySoftPayBox&device_info=CySoftPayBox&op_device_id=000063066004189990000194&sign=00000000000000000000000000000000>

---

# ~~获取超赢商户基础信息【弃用】~~

**应用场景**

该接口提供获取超赢商户基础信息功能。

**接口详情**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td class="tb-head">接口地址</td>
        <td>https://api.storepos.cn/Open/GetMchInfo</td>
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
| mch_id | 是 | 00000001 | 超赢商户号 |

**请求参数示例**

> agent_id=13000000000000000&version=1.0&pid=yunpos&mch_id=00000001&sign=00000000000000000000000000000000

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
