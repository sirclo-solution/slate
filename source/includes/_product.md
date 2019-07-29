# Product

## Get Stocks

Description : This endpoint used to get stock from partner system.

| Environment | Host URL               |
| ----------- | ---------------------- |
| Production  | https://api.connexi.id |

### HTTP Request

`GET /product/stock?limit=&offset=`

### Header Parameters

| Name       | Required | Type   | Description                                                                                                                                                       |
| ---------- | -------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| partner_id | Yes      | String | Partner id value (given from sirclo) used for partner identification by sirclo                                                                                    |
| Secret     | Yes      | String | HMAC (Hash Based Message Authentication Code) composed by hashing the HTTP request body using, refer to section: <a href="#composing-secret">Composing Secret</a> |

### Path Parameters

| Parameter | Required | Type    | Description                                                                                                                                                                         |
| --------- | -------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| limit     | Yes      | Integer | The maximum number of orders that can be returned, this supported maximum number is 100                                                                                             |
| offset    | Yes      | Integer | The number of lines to retrieve the next batch of records. For example, if your limit is 100, specifying an offset of 10 will return records 10. If not specified, the default is 0 |

> The above request returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 5,
      "sku": "DKL0907",
      "name": "Product ABC",
      "available": "20",
      "created_at": "2018-11-07T03:46:16.457936Z",
      "update_at": "2018-11-07T03:46:16.457938Z"
    }
  ],
  "message": "",
  "reference": ""
}
```
