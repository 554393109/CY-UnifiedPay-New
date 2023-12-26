# 概述

* [概述](README.md)
* [接口规则 v1/v2](rules.md)
  * [协议规则 v1/v2](rules.md#协议规则-v1v2)
  * [签名验证](rules.md#签名验证)
  * [请求格式](rules.md#请求格式)
  * [响应格式](rules.md#响应格式)
* [接口规则 v3](rules_v3.md)
  * [协议规则 v3](rules_v3.md#协议规则-v3)
  * [报文content加密](rules_v3.md#报文content加密)
  * [签名验证](rules_v3.md#签名验证)
  * [请求格式](rules_v3.md#请求格式)
  * [响应格式](rules_v3.md#响应格式)
* [参数规定](parameters.md)

## 支付类接口

* [被扫支付](api/micropay.md)
  * [提交支付](api/micropay.md#提交支付)
  * [订单查询](api/micropay.md#订单查询)
  * [交易退款](api/micropay.md#交易退款)
  * [退款查询](api/micropay.md#退款查询)
  * [交易撤销](api/micropay.md#交易撤销)
  * [付款码查询买家id](api/micropay.md#付款码查询买家id)
  * [对账单下载](api/micropay.md#对账单下载)
* [主扫支付](api/preorderpay.md)
  * [主扫预下单v2](api/preorderpay.md#主扫预下单v2)
  * [微信下单](api/preorderpay.md#微信下单)
  * [支付宝下单](api/preorderpay.md#支付宝下单)
  * [微信付款通知](api/preorderpay.md#微信付款通知)
  * [支付宝付款通知](api/preorderpay.md#支付宝付款通知)
* [刷脸支付](api/facepay.md)
  * [获取sdk调用凭证](api/facepay.md#获取sdk调用凭证)
  * [提交支付](api/facepay.md#提交支付)

## 支付类接口v3

* [被扫支付v3](api/micropay_v3.md)
  * [提交支付](api/micropay_v3.md#提交支付)
  * [订单查询](api/micropay_v3.md#订单查询)
  * [交易退款](api/micropay_v3.md#交易退款)
  * [退款查询](api/micropay_v3.md#退款查询)
  * [交易撤销](api/micropay_v3.md#交易撤销)
  * [付款码查询买家id](api/micropay_v3.md#付款码查询买家id)
* [主扫支付v3](api/preorderpay_v3.md)
  * [主扫预下单v3](api/preorderpay_v3.md#主扫预下单v3)
  * [主扫付款通知v3](api/preorderpay_v3.md#主扫付款通知v3)

## 其它接口

* [商户](api/mch.md)
  * [获取商户信息](api/mch.md#获取商户信息)
  * [注册超赢虚拟商户](api/mch.md#注册超赢虚拟商户)
  * [获取超赢商户号](api/mch.md#获取超赢商户号)
  * [获取超赢商户微信子商户号](api/mch.md#获取超赢商户微信子商户号)
  * [支付终端查询商户配置](api/mch.md#支付终端查询商户配置)
  * [支付终端扫描商户二维码获取配置](api/mch.md#支付终端扫描商户二维码获取配置)
  
* [运维管理](api/operation.md)
  * [下发获取超赢商户号验证短信](api/operation.md#下发获取超赢商户号验证短信)
  * [小程序用户code登录](api/operation.md#小程序用户code登录)
  * [微信apiv3请求代签名](api/operation.md#微信apiv3请求代签名)
