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
        <td>MD5【默认】、SHA1、SHA256、HMAC；若无特殊规定，优先使用MD5</td>
    </tr>
    <tr>
        <td style="width: 100px; text-align: center; font-weight: 700;">签名要求</td>
        <td>部份接口需要校验签名</td>
    </tr>
</table>

# 签名验证

签名生成的通用步骤如下：

**第一步**，设所有传输的数据为集合M，将集合M内**非空参数值的参数**按照参数名ASCII码从小到大排序（字典序），使用URL键值对的格式（即**key1=value1&key2=value2…**）拼接成字符串stringA。

特别注意以下重要规则：

* 参数名ASCII码**从小到大**排序（字典序，大小写不敏感，即A视为a）；
* 如果参数的值为空**不参与签名**；
* 验证调用返回或主动通知签名时，传送的sign参数**不参与签名**，将生成的签名与该sign值作校验；
* 接口可能增加字段，验证签名时**必须支持增加的扩展字段**。

**第二步**，在stringA最后拼接上key（**代理商密钥或商户密钥，按具体接口要求**）得到stringSignTemp字符串（即**stringA&key={KEY}**），并对stringSignTemp进行MD5运算，再将得到的字符串所有字符转换为大写，得到sign值signValue。

# 请求格式

###### 请求示例

```http
// Http
POST /UnifiedPay/Gateway_v2 HTTP/1.1
Host: {BaseURL}
Content-Type: application/x-www-form-urlencoded
Content-Length: 64

method=pay&mch_id=00000001&sign=00000000000000000000000000000000
```

```bash
# cURL
curl --location -g --request POST 'https://{BaseURL}/UnifiedPay/Gateway_v2'
--header 'Content-Type: application/x-www-form-urlencoded'
--data-urlencode 'method=pay'
--data-urlencode 'mch_id=00000001'
--data-urlencode 'sign=00000000000000000000000000000000'
```

```js
// Javascript
var settings = {
  "url": "https://{BaseURL}/UnifiedPay/Gateway_v2",
  "method": "POST",
  "headers": {
    "content-type": "application/x-www-form-urlencoded",
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

```csharp
// C#
var client = new RestClient("https://{BaseURL}/UnifiedPay/Gateway_v2");
var request = new RestRequest(Method.POST);
request.AddHeader("Content-Type", "application/x-www-form-urlencoded");
request.AddParameter("method", "pay");
request.AddParameter("mch_id", "00000001");
request.AddParameter("sign", "00000000000000000000000000000000");
IRestResponse response = client.Execute(request);
Console.WriteLine(response.Content);
```

```java
// Java
OkHttpClient client = new OkHttpClient().newBuilder().build();
MediaType mediaType = MediaType.parse("application/x-www-form-urlencoded");
RequestBody body = RequestBody.create(
    mediaType, 
    "method=pay&mch_id=00000001&sign=00000000000000000000000000000000");
Request request = new Request.Builder()
  .url("https://{BaseURL}/UnifiedPay/Gateway_v2")
  .method("POST", body)
  .addHeader("Content-Type", "application/x-www-form-urlencoded")
  .build();
Response response = client.newCall(request).execute();
```

```py
# Python
import requests

url = "https://{BaseURL}/UnifiedPay/Gateway_v2"

payload = "mch_id=00000001&method=pay&sign=00000000000000000000000000000000"
headers = {
    'content-type': "application/x-www-form-urlencoded",
}

response = requests.request("POST", url, data=payload, headers=headers)
print(response.text)
```

```swift
// swift
import Foundation
#if canImport(FoundationNetworking)
import FoundationNetworking
#endif

var semaphore = DispatchSemaphore (value: 0)

let parameters = "method=pay&mch_id=00000001&sign=00000000000000000000000000000000"
let postData =  parameters.data(using: .utf8)

var request = URLRequest(
    url: URL(string: "https://{BaseURL}/UnifiedPay/Gateway_v2")!, timeoutInterval: Double.infinity)
request.addValue("application/x-www-form-urlencoded", forHTTPHeaderField: "Content-Type")

request.httpMethod = "POST"
request.httpBody = postData

let task = URLSession.shared.dataTask(with: request) { data, response, error in 
  guard let data = data else {
    print(String(describing: error))
    semaphore.signal()
    return
  }
  print(String(data: data, encoding: .utf8)!)
  semaphore.signal()
}

task.resume()
semaphore.wait()
```

```go
// Golang
package main

import (
  "fmt"
  "strings"
  "net/http"
  "io/ioutil"
)

func main() {
  url := "https://{BaseURL}/UnifiedPay/Gateway_v2"
  method := "POST"
  payload := strings.NewReader("method=pay&mch_id=00000001&sign=00000000000000000000000000000000")
  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, payload)

  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("Content-Type", "application/x-www-form-urlencoded")

  res, err := client.Do(req)
  if err != nil {
    fmt.Println(err)
    return
  }
  defer res.Body.Close()

  body, err := ioutil.ReadAll(res.Body)
  if err != nil {
    fmt.Println(err)
    return
  }
  fmt.Println(string(body))
}
```

```php
// PHP
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://{BaseURL}/UnifiedPay/Gateway_v2',
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => 'method=pay&mch_id=00000001&sign=00000000000000000000000000000000',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/x-www-form-urlencoded'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

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
