# ONT Commerce 商户介入指导


## 什么是 ONT Commerce

## 接入前准备

## 接口说明

### 创建收款订单

* **HTTP Request**

https://commerce.ont.io/v1/payment/invoice

* **Arguments**

| PARAMETER         | TYPE          | REQUIRED        | DESCRIPTION                    |
| :---------------- | --------------| --------------- | ------------------------------ |
| merchant_id       | String        | Required        | 商户编号                       |
| currency          | String        | Required        | 默认收款币种，目前为：USDT     |
| description       | String        | Required        | 订单描述，最长100字节          |
| signature         | String        | Required        | 商户数字签名                   |

* **Response**

商户系统将获得唯一的订单编号和二维码数据payout，payout是一个数组，支持多种币种。商户按照币种显示在收银台，供消费者选择合适的币种扫二维码支付。

> 目前支持三个币种，后续将不断扩展，收银台也需要提供相应扩展功能。

```
{
    "action": "create_invoice",
    "version": "v1.0.0",
    "invoice_id": "10ba038e-48da-487b-96e8-8d3b99b6d18a",
	"error": 0,
	"decription": "SUCCESS"
	"created_at": "2019-01-31T20:49:02Z",
    "payout": [
		{
			"blockchain":"etherum",
            "contractHash": "8b344a43204e60750e7ccc8c1b708a67f88f2001",
            "to_address": "0x419f91df39951fd4e8acc8f1874b01c0c78ceba6",
            "amount": "100.01",
            "cointype": "USDT(ERC-20)"
        },
		{
			"blockchain":"etherum",
            "contractHash": "8b344a43204e60750e7ccc8c1b708a67f88f2002",
            "to_address": "0x419f91df39951fd4e8acc8f1874b01c0c78ceba6",
            "amount": "100.01",
            "cointype": "PAX(ERC-20)"
        },
		{
			"blockchain":"etherum",
            "contractHash": "8b344a43204e60750e7ccc8c1b708a67f88f2003",
            "to_address": "0x419f91df39951fd4e8acc8f1874b01c0c78ceba6",
            "amount": "100.01",
            "cointype": "USDC"
        }
    ],
	"signature": "xxxxxxxx"
}
```

* **错误码**

| 返回代码 | 描述信息                      | 说明                              |
| :------- | ----------------------------- | --------------------------------- |
| 0        | SUCCESS                       | 成功                              |
| 1001     | MERCHANT_NOT_EXIST            | 商户不存在或未激活                |
| 1002     | MERCHANT_INVALID_SIGNATURE    | 商户签名错误                      |







