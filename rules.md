# 协议规则

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">传输方式</td>
        <td>为保证交易安全性，采用HTTPS传输（开发时可使用HTTP）</td>
    </tr>
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">数据格式</td>
        <td>若无指定，默认返回数据为JSON格式（application/json）</td>
    </tr>
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">字符编码</td>
        <td>统一采用UTF-8字符编码</td>
    </tr>
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">内容类型</td>
        <td>统一采用x-www-form-urlencoded编码格式</td>
    </tr>
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">签名算法</td>
        <td>MD5，后续会兼容SHA1、SHA256、HMAC等</td>
    </tr>
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">签名要求</td>
        <td>部份接口需要校验签名</td>
    </tr>
</table>

# 签名验证

签名生成的通用步骤如下：

**第一步**，设所有传输的数据为集合M，将集合M内非空参数值的参数按照参数名ASCII码从小到大排序（字典序），使用URL键值对的格式（即**key1=value1&key2=value2…**）拼接成字符串stringA。

特别注意以下重要规则：

* 参数名ASCII码**从小到大**排序（字典序）；
* 如果参数的值为空**不参与签名**；
* 参数名区分大小写；
* 验证调用返回或主动通知签名时，传送的sign参数**不参与签名**，将生成的签名与该sign值作校验；
* 接口可能增加字段，验证签名时**必须支持增加的扩展字段**。

**第二步**，在stringA最后拼接上key得到stringSignTemp字符串（即**stringA&key={KEY}**），并对stringSignTemp进行MD5运算，再将得到的字符串所有字符转换为大写，得到sign值signValue。

# 请求格式

###### 请求示例

```js
// Javascript
var settings = {
  "async": true,
  "crossDomain": true,
  "url": "http://{BaseURL}/UnifiedPay/Gateway",
  "method": "POST",
  "headers": {
    "content-type": "application/x-www-form-urlencoded",
    "cache-control": "no-cache",
    "X-Requested-With":"XMLHttpRequest",
  },
  "data": {
    "method": "pay",
    "mch_id": "00000001",
    "sign", "00000000000000000000000000000000"
  }
}

$.ajax(settings).done(function (response) {
  console.log(response);
});
```

```py
# Python
import requests

url = "http://{BaseURL}/UnifiedPay/Gateway"

payload = "mch_id=00000001&method=pay&sign=00000000000000000000000000000000"
headers = {
    'content-type': "application/x-www-form-urlencoded",
    'cache-control': "no-cache",
    'X-Requested-With': "XMLHttpRequest",
    }

response = requests.request("POST", url, data=payload, headers=headers)
print(response.text)
```

# 响应格式

| **字段名** | **必填** | **类型** | **说明** |
| :--- | :---: | :---: | :--- |
| state | 是 | String | 通讯状态，详见参数规定 |
| code | 否 | String | 状态码 ，详见参数规定 |
| msg | 否 | String | 返回信息；若调用失败则为错误原因 |
| trade_state | 否 | String | 交易状态，详见参数规定 |
| sign | 是 | String | 响应结果的签名串 |

###### 成功示例

```json
{
    "state": "SUCCESS",
    "code": "10000",
    "msg": "SUCCESS",
    "trade_state": "SUCCESS",
    "sign": "00000000000000000000000000000000"
}
```

###### 失败示例

```json
{
    "state": "FAIL",
    "code": "10002",
    "msg": "签名错误",
    "sign": "00000000000000000000000000000000"
}
```
