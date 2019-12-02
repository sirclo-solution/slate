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

> Request example
> `GET /v1/partner/product/stock?limit=100&offset=0`

> The above request returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 5,
      "sku": "DKL0907",
      "partner_sku": "PRODABCDE0001",
      "partner_variant_sku": "PRODABCDE0001-S",
      "name": "Product ABC",
      "stock": 20,
      "created_at": "2019-07-09T02:09:25.071496Z",
      "update_at": "2019-09-05T06:11:51.394954Z"
    },
    {
      "id": 8,
      "sku": "DLP0907",
      "partner_sku": "PRODABCDE0002",
      "partner_variant_sku": "PRODABCDE0002-M",
      "name": "Product DDA",
      "stock": 11,
      "created_at": "2019-08-21T12:33:31.139787Z",
      "update_at": "2019-08-26T09:43:06.296043Z"
    }
  ],
  "total_record": 33,
  "offset": 0,
  "limit": 2,
  "message": "",
  "reference": "e444c078-3bee-4606-949d-da120886424e"
}
```

## Create Product

### HTTP Request

`POST /v1/partner/product`

### Header Parameters

| Name       | Required | Type   | Description                                                                                                       |
| ---------- | -------- | ------ | ----------------------------------------------------------------------------------------------------------------- |
| partner_id | Yes      | String | Partner ID value (given from SIRCLO) used for partner identification                                              |
| secret     | Yes      | String | HMAC (Hash Based Message Authentication Code), refer to section: <a href="#composing-secret">Composing Secret</a> |

### Request Body Parameters

Request body must be a JSON document with the following properties

| Name                           | Required | Type   | Description                                   |
| ------------------------------ | -------- | ------ | --------------------------------------------- |
| sku                            | Yes      | String | SKU of the product in Connexi                 |
| partner_sku                    | Yes      | String | SKU of the product in Partner                 |
| partner_variant                | Yes      | Object |                                               |
| partner_variant - variant_sku  | Yes      | String | SKU of the variant product                    |
| partner_variant - variant_name | Yes      | String | Name of the variant product                   |
| name                           | Yes      | String | Name of the product                           |
| decription                     | Yes      | String | Information about feature, benefit of product |
| currency                       | Yes      | String | Currency of the product                       |
| price                          | Yes      | Double | Price of the product                          |
| weight                         | Yes      | Double | Weight of the product                         |
| height                         | Yes      | Double | Height of the product                         |
| length                         | Yes      | Double | Length of the product                         |
| width                          | Yes      | Double | Width of the product                          |

> Request body example:

```json
{
  "products": [
    {
      "sku": "DKL0907",
      "partner_sku": "PRODABCDE0001",
      "partner_variant": {
        "variant_sku": "PRODABCDE0001-S",
        "variant_name": "Product ABC - S"
      },
      "name": "Product ABC",
      "description": "Product ABC Description",
      "currency": "IDR",
      "price": 340000,
      "weight": 250,
      "height": 86,
      "lenght": 95,
      "width": 98
    },
    {
      "sku": "DLP0907",
      "partner_sku": "PRODABCDE0002",
      "partner_variant": {
        "variant_sku": "PRODABCDE0002-S",
        "variant_name": "Product DDA - S"
      },
      "name": "Product DDA",
      "description": "Product DDA Description",
      "currency": "IDR",
      "price": 340000,
      "weight": 250,
      "height": 86,
      "lenght": 95,
      "width": 98
    }
  ]
}
```

> The above request returns JSON structured like this:

```json
{
  "data": {
    "succeed": [
      {
        "id": 411,
        "sku": "DKL0907",
        "partner_sku": "PRODABCDE0001",
        "partner_variant_sku": "PRODABCDE0001-S",
        "name": "Product ABC"
      }
    ],
    "failed": [
      {
        "partner_sku": "PRODABCDE0002",
        "reason": "error happened"
      }
    ]
  },
  "message": "",
  "reference": "3c6bdd10-63b3-4c58-b89a-c2b1e99e885f"
}
```
