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

|Name                 | Required | Type   | Description                                                      | 
|---------------------| ---------|--------|------------------------------------------------------------------|
| SKU                 |  Yes     | String | Stok Keeping Unit in Connexi                                     |
| partner_sku         |  Yes     | String | SKU product used in partner                                      |
| variant_sku         |   No     | String | SKU variant of product used in partner                           |
| variant_name        |   No     | string | Name of variant product                                          | 
| name                |   No     | string | Name of product                                                  |
| decription          |   No     | string | Information about feature, benefit of product                    |

> Request body example:

```json 
  {
    "products":[
      {
        "sku" : "LEVS-319",
        "partner_sku":"LEVS-319",
        "partner_variants":[
          {
            "variant_sku":"LEVS-319-32001",
            "variant_name":"Levi's Jeans Regular fit 32"
          },
          {
            "variant_sku" : "LEVS-319-34001",
            "variant_name":"Levi's Jeans Black Slim Fit 34"
          }
        ], 
        "name" : "Levi's",
        "description" : "Levi's merupakan merek jeans ternama di seluruh dunia, Ayo pakai Levi's!",
        "currency" : "IDR", 
        "price":340000,
        "weight" : 250, 
        "height" : 86, 
        "lenght" : 95, 
        "width"  : 98,
      }
    ]
  }
```
> The above request returns JSON structured like this:
```json
{
  "data":{
    "succeed":[
      {
        "id" : 5019,
        "sku" : "LEVS-319",
        "partner_sku" : "",
        "partner_variant_sku":"",
        "name":"Levi's merupakan merek jeans ternama di seluruh dunia. Ayo pakai Levi's!",
        "created_at" : "2019-11-28T08:04:03.225186Z", 
        "updated_at" : "2019-11-29T06:41:30.603645505Z"
      },
      {
        "id" : 5020,
        "sku" : "LEVS-319-32001",
        "partner_sku" : "",
        "partner_variant_sku":"",
        "name":"Levi's merupakan merek jeans ternama di seluruh dunia. Ayo pakai Levi's!",
        "created_at" : "2019-11-28T08:04:03.225186Z", 
        "updated_at" : "2019-11-29T06:41:30.603645505Z"
      },
      {
        "id" : 5021,
        "sku" : "LEVS-319-34001",
        "partner_sku" : "",
        "partner_variant_sku":"",
        "name":"Levi's merupakan merek jeans ternama di seluruh dunia. Ayo pakai Levi's!",
        "created_at" : "2019-11-28T08:04:03.225186Z", 
        "updated_at" : "2019-11-29T06:41:30.603645505Z"
      }
    ],
    "failed" :[]
  },
  "message" : "Product creayed successfully",
  "reference" : "3c6bdd10-63b3-4c58-b89a-c2b1e99e885f"
}
```
