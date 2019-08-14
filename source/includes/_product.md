# Products

## Get Stock

### HTTP Request

`GET /v1/partner/product/stock?limit=&offset=`

### Header Parameters

| Name       | Required | Type   | Description                                                                                                       |
| ---------- | -------- | ------ | ----------------------------------------------------------------------------------------------------------------- |
| partner_id | Yes      | String | Partner ID value (given from SIRCLO) used for partner identification                                              |
| secret     | Yes      | String | HMAC (Hash Based Message Authentication Code), refer to section: <a href="#composing-secret">Composing Secret</a> |

### Path Parameters

| Parameter | Required | Type    | Description                                                                                            |
| --------- | -------- | ------- | ------------------------------------------------------------------------------------------------------ |
| limit     | No       | Integer | Number of orders that want to be returned (by default the number is 100)                               |
| offset    | No       | Integer | To be used for pagination (use value 10 if you want to skip 10 first datas, by default the value is 0) |

> The above request returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 5,
      "sku": "DKL0907",
      "name": "Product ABC",
      "stock": 20,
      "created_at": "2018-11-07T03:46:16Z",
      "update_at": "2018-11-07T03:46:16Z"
    }
  ],
  "message": "",
  "reference": ""
}
```
