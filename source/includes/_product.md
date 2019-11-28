# Products

## Get Stock

### HTTP Request

`GET /v1/partner/product/stock?limit=&offset=`

### Header Parameters

| Name       | Required | Type   | Description                                                                                                       |
| ---------- | -------- | ------ | ----------------------------------------------------------------------------------------------------------------- |
<<<<<<< HEAD
| partner-id | Yes      | String | Partner ID value (given from SIRCLO) used for partner identification                                              |
=======
| partner_id | Yes      | String | Partner ID value (given from SIRCLO) used for partner identification                                              |
>>>>>>> 13bd2b514ddf525b2b3ee60ab289f4c5f8f270b4
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
<<<<<<< HEAD
      "partner_sku" :"PRODABCDE0001",
      "partner_variant_sku" : "",
      "name": "Product ABC",
      "stock": 20,
      "created_at": "2019-07-09T02:09:25.071496Z",
      "update_at": "2019-09-05T06:11:51.394954Z"
    },
    {
      "id" :8,
      "sku" :"DLP0907",
      "partner_sku" : "",
      "partner_variant_sku" : "",
      "name" : "Product DDA",
      "stock" : 11,
      "created_at" : "2019-08-21T12:33:31.139787Z",
      "update_at" : "2019-08-26T09:43:06.296043Z"
    }
  ],
  "total_record" : 33,
  "offset" : 0,
  "limit" : 2,
  "message": "",
  "reference": "e444c078-3bee-4606-949d-da120886424e"
=======
      "name": "Product ABC",
      "stock": 20,
      "created_at": "2018-11-07T03:46:16Z",
      "update_at": "2018-11-07T03:46:16Z"
    }
  ],
  "message": "",
  "reference": ""
>>>>>>> 13bd2b514ddf525b2b3ee60ab289f4c5f8f270b4
}
```
