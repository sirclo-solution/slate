# Products

## Get Stock

### HTTP Request

`GET /v1/partner/product/stock`

### Header Parameters

| Name       | Required | Type   | Description                                                                                                       |
| ---------- | -------- | ------ | ----------------------------------------------------------------------------------------------------------------- |
| partner_id | Yes      | String | Partner ID value (given from SIRCLO) used for partner identification                                              |
| secret     | Yes      | String | HMAC (Hash Based Message Authentication Code), refer to section: <a href="#composing-secret">Composing Secret</a> |

> The above request returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 5,
      "sku": "DKL0907",
      "name": "Product ABC",
      "available": "20",
      "created_at": "2018-11-07T03:46:16Z",
      "update_at": "2018-11-07T03:46:16Z"
    }
  ],
  "message": "",
  "reference": ""
}
```
