--- 
title: Order 

language_tabs: 
   - shell 

toc_footers: 
   - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a> 

includes: 
   - errors 

search: true 

---

# Introduction 

**Welcome To SIRCLO API Documentation**
You can used this API to connect your backend system to SIRCLO Platform. 

**Version:** 1.0 

# Order API 

## Get Order 


**Description:** This endpoint used to get all orders in partner system.   

|Environment | Host URL               | 
|------------|------------------------|
|Production  |https://api.connexi.id |

### HTTP Request 

`GET /v1/order/?since=&until=&limit=&offset=`

### Header Parameters

| Name       |  Required |Description                       |
| -----------|  -------- |--------------------------------- |
| api_key    | Yes       | api key used to authentication   |
| api_secret | Yes       | api secret used to authentication| 

### Path Parameters 

| Parameter |Required   |  Description                                    |
|-----------|-----------|-------------------------------------------------|
|since      | Yes       |The current time in ISO8601 format timestamp from which the order requested|
|until      | Yes       |The current time in ISO8601 format timestamp to which the order requested  |
|limit      | Yes       |The maximum number of orders that can be returned, this supported maximum number is 100| 
|offset     | Yes       |The number of lines to retrieve the next batch of records. For example, if your limit is 100, specifying an offset of 10 will return records 10. If not specified, the default is 0|

**Responses**

> The above request will return response like this:

```json
{
  "data": [
    {
      "id": 1,
      "order_number0" :"",
      "order_date": "2006-01-02T15:04:05Z07:00",
      "customer_reference": "JNH7438B",
      "shipment_reference": "",
      "status": "accepted",
      "delivery_name": "Artia",
      "delivery_email": "artia2@gmail.com",
      "delivery_street_address": "Jl. Anggrek No.106 Blok C5",
      "delivery_region": "DKI Jakarta",
      "delivery_city": "Kota Jakarta Barat - Cengkareng",
      "delivery_country": "Indonesia",
      "delivery_post_code": "11720",
      "delivery_method": "JNE REG",
      "delivery_mobile": "082101871618",
      "airwaybill_number": "AWB12345678",
      "currency_code": "IDR",
      "subtotal": 110000,
      "discount_total": 10000,
      "shipping_total": 15000,
      "tax_total" : 0,
      "total": 115000,
      "line_item": [
        {
          "id": 3,
          "sku": "DKL0907",
          "name": "Product ABC",
          "quantity": 2,
          "unit_price": 100000,
          "discount": 10000,
          "shipping_total": 15000
        }
      ],
      "total_count": 100
    }
  ],
  "message": "",
  "reference": ""
}
```

## Create Order

**Description:** Use this endpoint to create order. 


### HTTP Request 
`POST https://api.connexi.id/v1/order`

**Header Parameters**

| Name       |  Required | Type   |Description                       |
| -----------|  -------- | ------ |----------------------------------|
| api_key    | Yes       | string | api key used to authentication   |
| api_secret | Yes       | string | api secret used to authentication| 

### Request Body 
   Request body parameter must be in the form of JSON

   > This request orders parameter in body :

```json
        {
            "order_id": "",
            "order_date" : "2006-01-02T15:04:05Z07:00",
            "customer_reference" : "DHU9868NGY",
            "shipment_reference":"",
            "status" : "accepted",
            "delivery_name" : "Artia",
            "delivery_email" : "artia2@gmail.com",
            "delivery_street_address" : "Jl. Anggrek No.106 Blok C5",
            "delivery_region" : "DKI Jakarta",
            "delivery_city" : "Kota Jakarta Barat - Cengkareng",
            "delivery_country" : "Indonesia",
            "delivery_post_code" : "11720",
            "delivery_method" : "JNE REG",
            "delivery_mobile" : "082101871618",
            "airwaybill_number" : "AWB12345678",
            "shipping_total" : 15000,
            "shipment_tracked_at" : "2006-01-02T15:04:05Z07:00", 
            "line_item" : [
                {   "sku": "DKL0907",
                    "quantity": 2,
                    "raw_price": 100000,
                    "discount": 10000,
                    "tax": 0,
                    "shipping_total": 15000
                }
            ]
        }
``` 

> The above request will return response like this:

```json
{
  "data": {
    "order_id": 123,
    "order_number" : "",
    "order_date": "2006-01-02T15:04:05Z07:00",
    "customer_reference": "JNH7438B",
    "shipment_reference": "",
    "status": "accepted",
    "delivery_name": "Artia",
    "delivery_email": "artia2@gmail.com",
    "delivery_street_address": "Jl. Anggrek No.106 Blok C5",
    "delivery_region": "DKI Jakarta",
    "delivery_city": "Kota Jakarta Barat - Cengkareng",
    "delivery_country": "Indonesia",
    "delivery_post_code": "11720",
    "delivery_method": "JNE REG",
    "delivery_mobile": "082101871618",
    "airwaybill_number": "AWB12345678",
    "currency_code": "IDR",
    "subtotal": 110000,
    "discount_total": 10000,
    "shipping_total": 15000,
    "total": 115000,
    "line_item": [
      {
        "id": 3,
        "sku": "DKL0907",
        "name": "Product ABC",
        "quantity": 2,
        "unit_price": 100000,
        "discount": 10000,
        "shipping_total": 15000
      }
    ],
    "total_count": 100
  },
  "message": "",
  "reference": ""
]
```

|   Name                | Required | Type     | Description                |
| ----------------------| ---------| -------- | -------------------------- | 
| order_number                | No       | string    | order number                                                                                       |
| order_date                  | Yes      | Timestamp | the date of order and must be in ISO8601 format timestamp                                          |
| customer_reference          | No       | string    | customer reference                                                                                 |
| shipment_reference          | Yes      | string    | shipment reference                                                                                 |
| status                      | No       | string    | status of orders, If status is empty, then it will be assigned as "pending"                        |
|                             |          |           | The acceptable statuses are:                                                                       |
|                             |          |           | 1. pending                                                                                         |
|                             |          |           | 2. accepted                                                                                        |
|                             |          |           | 3. packed                                                                                          |
|                             |          |           | 4. completed                                                                                       |
|                             |          |           | 5. cancelled                                                                                       |
| delivery_name               | No       | string    | name of the buyer in this order                                                                    |
| delivery_email              | No       | string    | email address of the buyer in this order                                                           |
| delivery_street_address     | No       | string    | street address of the buyer                                                                        |
| delivery_region             | No       | string    | region address of the buyer                                                                        |
| delivery_city               | No       | string    | city address of the buyer                                                                          |
| delivery_country            | No       | string    | country address of the buyer                                                                       |
| delivery_post_code          | No       | string    | post code address of the buyer                                                                     |
| delivery_method             | No       | string    | the method of delivery                                                                             |
| delivery_mobile             | No       | string    | mobile number of the buyer                                                                         |
| airwaybill_number           | No       | string    | airwaybill number from 3PL                                                                         |
| currency_code               | No       | string    | currency code for this order is "IDR"                                                              |
| subtotal                    | No       | double    | this total value of order before discount and after tax                                            |
| discount_total              | No       | double    | this total discount value for this order (sum of every line_item.discount)                         |
| shipping_total              | No       | double    | This total shipping cost value for this order                                                      |
| tax_total                   | No       | double    | tax total all orders                                                                               |
| total                       | No       | double    | this total value of order after discount, tax and shipping cost                                    |
| line_items                  | Yes      | array     |                                                                                                    |
| line_items - sku            | Yes      | string    | sku of the product                                                                                 |
| line_items - quantity       | Yes      | integer   | quantity of the order line item                                                                    |
| line_items - raw_price      | Yes      | double    | this raw price in order line item after discount and tax)                                          |
| line_items - discount       | Yes      | double    | discount product in line item                                                                      |
| line_items - tax            | Yes      | double    | tax order in line item                                                                             |
| line_items - shipping_total | Yes      | double    | this shipping total in line item, can be same value with "shipping_total" above, could be optional |
| line_items - total_price    | Yes      | double    | total price product in line item                                                                   |

## Update Order


**Description:** This endpoint used to update order from partner system.  


### HTTP Request 

`PATCH https://api.connexi.id/v1/order` 

### Header Parameters

| Name      |  Required | Type   |Description         |
| ----------|---------- | ----   |------------------- |
| api_key   | Yes       | string |api key used to authentication | 
| api_secret| Yes       | string |api secret used to authentication | 
 
###Request Body

**Request body parameter must be in the form JSON**

> This request orders parameter in body : 

```json
{  
    "accepted_orders":[  
        {  
            "order_id":101,
            "updated_at":"2017-05-07 18:06:51",
            "order_number":"order001"
        }
    ],
    "packed_orders":[
        {  
            "order_id":102,
            "updated_at":"2017-05-09 18:06:51",
            "airwaybill_number":"awb002"
        }
    ],
    "completed_orders":[
        {  
            "order_id":103,
            "updated_at":"2017-05-09 18:06:51",
            "received_by":"Yosua"
        }
    ],
    "cancelled_orders":[
        {  
            "order_id":104,
            "updated_at":"2017-05-09 18:06:51",
            "cancel_reason":"Salah beli barang"
        }
    ]
]
```

> The above request will return response like this:

```json
    {  
    "data": {
        "succeed": [
            {
                "order_id":101,
                "order_status":"accepted",
                "updated_at":"2008-09-15T15:53:00",
            },
            {
                "order_id":102,
                "order_status":"packed",
                "updated_at":"2008-09-15T15:53:00",
            },
            {
                "order_id":103,
                "order_status":"completed",
                "updated_at":"2008-09-15T15:53:00",
            },
            {
                "order_id":104,
                "order_status":"cancelled",
                "updated_at":"2008-09-15T15:53:00",
            }
        ],
        "failed" : [
            {
                "order_id":105,
                "order_status":"accepted",
                "updated_at":"2008-09-15T15:53:00",
                "error_message":"Parameter yang diberikan salah" 
            }
        ]
    },
    "message" : "4 dari 5 order berhasil diubah",
    "reference": "as0b2-b3as8-kv1c6-3sj6z"
}
```

# Product 

## Get Stocks 

Description : This endpoint used to get stock from partner system. 

|Environment | Host URL               | 
|------------|------------------------|
|Production  |https://api.connexi.id  |

### HTTP Request  

`GET /v1/order/?since=&until=&limit=&offset=`

### Header Parameters

| Name       |  Required |Description                       |
| -----------|  -------- |--------------------------------- |
| api_key    | Yes       | api key used to authentication   |
| api_secret | Yes       | api secret used to authentication| 

### Path Parameters 

| Parameter |Required   |  Description                      |
|-----------|-----------|-----------------------------------------|
|limit      | Yes       |The maximum number of orders that can be returned, this supported maximum number is 100| 
|offset     | Yes       |The number of lines to retrieve the next batch of records. For example, if your limit is 100, specifying an offset of 10 will return records 10. If not specified, the default is 0|

**Responses**

> The above request will return response like this:

```json
{
  "data": [
    {
      "id": 5,
      "sku": "DKL0907",
      "name": "product ABC ",
      "available": "20",
      "created_at": "2018-11-07T03:46:16.457936Z",
      "update_at": "2018-11-07T03:46:16.457938Z"
    }
  ],
  "message": "",
  "reference": ""
]
```

<!-- Converted with the swagger-to-slate https://github.com/lavkumarv/swagger-to-slate -->
