# 超赢聚合支付API在线文档

[![超赢科技](/assets/logo.png)](http://pos.cn/ "超赢科技")

> 当前版本：v3.2.1
>
> 最后维护：尹自强，yinziqiang@chaoying.com.cn
>
> 更新日期：2024-01-12

## 版本说明

【*v3.2.1*】 2024-01-12

* 更新部分接口描述

【*v3.2.0*】 2023-12-25

* 添加获取商户信息接口
* 添加对账单下载接口

【*v3.1.0*】 2023-05-31

* 添加主扫支付v3接口

【*v3.0.1*】 2023-05-25

* 更新部分接口描述

【*v3.0.0*】 2023-05-22

* 添加被扫支付v3接口

【*v2.15.0*】 2022-12-29

* 添加微信APIv3请求代签名接口

【*v2.14.1*】 2022-08-31

* 主扫接口支持数字人民币

【*v2.14.0*】 2022-07-28

* 支持数字人民币

【*v2.13.1*】 2022-05-07

* 修改支付终端轮询商户配置接口地址

【*v2.13.0*】 2022-04-12

* 修改主扫v2接口
* 修改支付终端轮询商户配置接口，添加gateway响应参数
* 修改支付终端扫描商户二维码获取配置接口，添加gateway响应参数

【*v2.12.1*】 2022-04-08

* 更新部分接口描述

【*v2.12.0*】 2022-04-06

* 修改支付终端轮询商户配置接口
* 修改支付终端扫描商户二维码获取配置接口

【*v2.11.0*】 2022-03-28

* 添加支付终端展示商户配置二维码描述

【*v2.10.1*】 2022-03-24

* 更新支付终端扫描商户二维码获取配置接口描述

【*v2.10.0*】 2022-03-09

* 升级部分接口支持v2版
* 优化接口分类
* 更新接口描述

【*v2.9.1*】 2022-03-02

* 更新支付终端轮询商户配置接口描述

【*v2.9.0*】 2022-03-01

* 添加支付终端类接口

<!-- 

【*v2.8.1*】 2021-07-19

* 被扫支付接口、刷脸支付接口添加sub_appid参数

【*v2.8.0*】 2021-07-13

* 添加付款码查询买家Id接口

【*v2.7.3*】 2021-07-13

* 调整被扫支付部分接口响应参数

【*v2.7.2*】 2021-02-20

* 支付宝和微信预下单接口添加attach参数

【*v2.7.1*】 2020-11-18

* 更新支付宝和微信预下单结果通知第三方订单号为非必填参数

【*v2.7.0*】 2020-09-03

* 被扫支付各接口添加paytype响应参数

【*v2.6.3*】 2020-04-22

* 更新部分接口描述

【*v2.6.2*】 2020-04-22

* 更新各接口地址域名

【*v2.6.1*】 2020-03-06

* 支付接口添加分账参数

【*v2.6.0*】 2020-03-01

* 添加微信子商户支付配置新增接口

【*v2.5.3*】 2019-08-06

* 添加小程序用户code登录接口

【*v2.5.2*】 2019-08-05

* 添加获取超赢商户基础信息接口

【*v2.5.1*】 2019-06-10

* 修改退款查询接口移除商户单号out_trade_no和平台单号transaction_id请求参数
* 修复退款查询接口BUG

【*v2.5.0*】 2019-06-04

* 修改所有接口pid和version请求参数为必填项
* 修改支付类接口响应参数添加订单应付金额base_fee字段，total_fee字段修改为订单实付金额
* 修改刷脸支付-提交支付接口添加商品详情goods_detail请求参数，goods_tag字段修改为订单优惠标记；添加营销详情promotion_detail响应参数
* 修改被扫支付-提交支付接口添加商品详情goods_detail请求参数，goods_tag字段修改为订单优惠标记；添加营销详情promotion_detail响应参数
* 修改预下单支付-微信预下单接口添加商品详情goods_detail请求参数，goods_tag字段修改为订单优惠标记；
* 修改预下单支付-微信预下单结果通知添加营销详情promotion_detail响应参数
* 修改被扫支付-订单查询接口添加营销详情promotion_detail响应参数
* 修改交易退款接口添加应付金额base_fee，应退金额base_refund_fee；refund_fee字段修改为实退金额
* 修改退款查询接口添加应退金额汇总base_refund_fee_summary，应退金额base_refund_fee响应字段
* 修改支付类接口响应参数添加微信服务商商户号wx_mch_id字段，微信子商户号wx_sub_mch_id字段（具体参考各接口响应参数）

【*v2.4.1*】 2019-04-10

* 获取超赢商户微信子商户号接口说明修改

【*v2.4.0*】 2019-04-03

* 添加获取超赢商户微信子商户号接口

【*v2.3.7*】 2019-03-20

* 微信预下单接口添加pid和version请求参数
* 支付宝预下单接口添加pid和version请求参数

【*v2.3.6*】 2019-01-17

* 修改被扫支付-交易退款接口移除scene请求参数
* 修改被扫支付-交易撤销接口移除scene请求参数

【*v2.3.5*】 2019-01-09

* 修改刷脸支付-提交支付接口移除sub_openid请求参数

【*v2.3.4*】 2018-12-28

* 修改获取SDK调用凭证接口移除store_id响应参数

【*v2.3.3*】 2018-12-28

* 修改获取SDK调用凭证接口添加mch_id和paytype请求参数
* 修改刷脸支付接口添加paytype请求参数

【*v2.3.2*】 2018-12-27

* 修改刷脸支付接口face_code参数描述

【*v2.3.1*】 2018-12-27

* 添加获取SDK调用凭证接口
* 修改刷脸支付接口添加openid和sub_openid请求参数

【*v2.3.0*】 2018-12-20

* 添加刷脸支付接口

【*v2.2.2*】 2018-10-23

* 获取超赢商户号接口响应参数添加商户全称和商户简称

【*v2.2.1*】 2018-10-22

* 微信预下单接口添加门店编号参数
* 支付宝预下单接口添加门店编号参数

【*v2.2.0*】 2018-10-19

* 被扫支付-提交支付接口移除paytype参数

【*v2.1.2*】 2018-10-18

* 更新获取超赢商户号接口

【*v2.1.1*】 2018-09-13

* 添加下发获取超赢商户号验证短信接口
* 更新获取超赢商户号接口

【*v2.0.1*】 2018-08-23

* 被扫支付接口示例报文修改

【*v2.0.0*】 2018-08-16

* 在线文档改版

【*v1.0.18*】 2018-07-02

* 微信公众号、小程序、APPx2支付时sub_appid改为必传项

【*v1.0.17*】 2018-06-27

* 商户进件接口地址修改
* 商户进件接口添加门头照和内景照参数

-->
