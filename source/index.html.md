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
You can used this API to connect to SIRCLO Platform.

**Version:** 1.0

# Order API

## Get Order

**Description:** Call this endpoint to get orders data that you have previously sent using create order endpoint.

| Environment | Host URL               |
| ----------- | ---------------------- |
| Production  | https://api.connexi.id |

### HTTP Request

`GET /v1/partner/page/{pageNo}?since={since}&until={until}&perpage={perpage}`

### Header Parameters
These parameters exist in the HTTP request headers

| Name       | Required | Description                       |
| ---------- | -------- |--------------------------------- |
| partner_id | Yes      | Partner id value (given from sirclo) used for partner identification by sirclo    |
| MAC        | Yes      | HMAC (Hash Based Message Authentication Code) composed by hashing the HTTP request body using, refer to section: Composing HMAC |

### Query String Parameters
These parameters exist in the http request query string

| Parameter | Required | Description                                                                                                                                                                         |
| --------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| since     | Yes      | Start range of order date of the requested orders with current time in RFC3339 format timestamp                                                                                     |
| until     | Yes      | End range of order date of the requested orders current time in RFC3339 format timestamp to which the order requested                                                                                                           |
| pageNo    | Yes      | The maximum number of orders that can be returned, this supported maximum number is 100                                                                                             |
| perpage   | Yes      | The number of records to be returned in 1 page |

**Request example**

`GET /v1/partner/page/2?since=2018-10-13T13:3A34:3A52:2B07:3A00&until=2018-10-16T19:3A22:3A39:2B07:3A00&perpage=1`

|              |                |
|--------------|----------------|
| Host :       | api.connexi.id |
| partner_id : | B98KL87        |
| MAC :        | a6jMwv4mFlj1VOh6jZzlJ2upVTcGfbjTtJpA2Hp5fpM= |    

**Responses**

> The above request will return response like this:

```json
{
  "data": [
    {
      "id": 1,
      "order_number": "ABC123",
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
      "tax_total": 0,
      "total": 115000,
      "line_items": [
        {
          "id": 3,
          "sku": "DKL0907",
          "name": "Product ABC",
          "quantity": 2,
          "raw_price": 100000,
          "discount": 10000
        }
      ],
      "createdAt": "2019-05-27 06:05:11.979185",
      "updatedAt": "2019-05-27 06:05:11.979185"
    }
  ],
  "total_record" : 1,
  "message": "",
  "reference": ""
}
```

## Create Order

**Description:** Use this endpoint to create order.

### HTTP Request

`POST https://api.connexi.id/v1/order`

**Header Parameters**
These parameters exist in the HTTP request headers

| Name       | Required | Description                                                                                                                    |
| ---------- | -------- |--------------------------------------------------------------------------------------------------------------------------------|
| partner_id | Yes      | Partner id value (given from sirclo) used for partner identification by sirclo                                                 |
| MAC        | Yes      |HMAC (Hash Based Message Authentication Code) composed by hashing the HTTP request body using, refer to section: Composing HMAC |

### Request Body

Request body parameter must be in the form of JSON

> This request orders parameter in body :

```json
{
  "order_id": "ORD-123",
  "order_date": "2006-01-02T15:04:05Z07:00",
  "customer_reference": "DHU9868NGY",
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
  "shipping_total": 15000,
  "line_items": [
    {
      "id": 3,
      "sku": "DKL0907",
      "name": "Product ABC",
      "quantity": 2,
      "raw_price": 100000,
      "discount": 10000
    }
  ]
}
```

> The above request will return response like this:

```json
{
  "data": {
    "id": 123,
    "order_id": "ORD-123",
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
    "line_items": [
      {
        "id": 3,
        "sku": "DKL0907",
        "name": "Product ABC",
        "quantity": 2,
        "raw_price": 100000,
        "discount": 10000
      }
    ],
    "createdAt": "2019-05-27 06:05:11.979185",
    "updatedAt": "2019-05-27 06:05:11.979185"
  },
  "message": "",
  "reference": ""
}
```
Request body must be a JSON document with the following properties

| Name                    | Required | Type      | Description                                                                 |
| ----------------------- | -------- | --------- | --------------------------------------------------------------------------- |
| order_id                | Yes      | string    | your order id                                                               |
| order_date              | Yes      | Timestamp | the date of order and must be in RFC3339 format timestamp                   |
| customer_reference      | No       | string    | customer reference                                                          |
| shipment_reference      | Yes      | string    | shipment reference                                                          |
| status                  | No       | string    | status of orders, If status is empty, then it will be assigned as "pending" |
|                         |          |           | The acceptable statuses are:                                                |
|                         |          |           | 1. pending                                                                  |
|                         |          |           | 2. accepted                                                                 |
|                         |          |           | 3. packed                                                                   |
|                         |          |           | 4. completed                                                                |
|                         |          |           | 5. cancelled                                                                |
| delivery_name           | No       | string    | name of the buyer in this order                                             |
| delivery_email          | No       | string    | email address of the buyer in this order                                    |
| delivery_street_address | No       | string    | street address of the buyer                                                 |
| delivery_region         | No       | string    | region address of the buyer                                                 |
| delivery_city           | No       | string    | city address of the buyer                                                   |
| delivery_country        | No       | string    | country address of the buyer                                                |
| delivery_post_code      | No       | string    | post code address of the buyer                                              |
| delivery_method         | No       | string    | the method of delivery                                                      |
| delivery_mobile         | No       | string    | mobile number of the buyer                                                  |
| airwaybill_number       | No       | string    | airwaybill number from 3PL                                                  |
| shipping_total          | No       | double    | This total shipping cost value for this order                               |
| line_items              | Yes      | array     |                                                                             |
| line_items - id         | Yes      | int       | id of the product                                                           |
| line_items - sku        | Yes      | string    | sku of the product                                                          |
| line_items - name       | Yes      | string    | name of the product                                                         |
| line_items - quantity   | Yes      | integer   | quantity of the order line item                                             |
| line_items - raw_price  | Yes      | double    | this raw price in order line item after discount and tax)                   |
| line_items - discount   | Yes      | double    | discount product in line item                                               |

## Update Order

**Description:** This endpoint used to update order from partner system.

### HTTP Request

`PATCH https://api.connexi.id/v1/order`

### Header Parameters

| Name       | Required | Type   | Description                       |
| ---------- | -------- | ------ | --------------------------------- |
| api_key    | Yes      | string | api key used to authentication    |
| api_secret | Yes      | string | api secret used to authentication |

###Request Body

**Request body parameter must be in the form JSON**

> This request orders parameter in body :

```json
{
  "accepted": [
    {
      "id": 123,
      "order_number": "order001",
      "updated_at": "2019-05-27 06:05:11.979185"
    }
  ],
  "packed": [
    {
      "id": 456,
      "order_number": "order002",
      "airwaybill_number": "awb002",
      "updated_at": "2019-05-27 06:05:11.979185"
    }
  ],
  "completed": [
    {
      "id": 789,
      "order_number": "order003",
      "received_by": "Yosua",
      "updated_at": "2019-05-27 06:05:11.979185"
    }
  ],
  "cancelled": [
    {
      "id": 135,
      "order_number": "order004",
      "cancel_reason": "",
      "updated_at": "2019-05-27 06:05:11.979185"
    }
  ]
}
```

> The above request will return response like this:

```json
{
  "data": {
    "succeed": [
      {
        "id": 123,
        "order_status": "accepted",
        "updated_at": "2019-05-27 06:06:11.979185"
      }
    ],
    "failed": [
      {
        "id": 456,
        "order_status": "pending",
        "message": "Parameter yang diberikan salah",
        "updated_at": "2019-05-27 06:06:11.979185"
      }
    ]
  },
  "message": "",
  "reference": ""
}
```

# Product

## Get Stocks

Description : This endpoint used to get stock from partner system.

| Environment | Host URL               |
| ----------- | ---------------------- |
| Production  | https://api.connexi.id |

### HTTP Request

`GET /v1/order/?since=&until=&limit=&offset=`

### Header Parameters

| Name       | Required | Type   | Description                       |
| ---------- | -------- | ------ | --------------------------------- |
| api_key    | Yes      | string | api key used to authentication    |
| api_secret | Yes      | string | api secret used to authentication |

### Path Parameters

| Parameter | Required | Description                                                                                                                                                                         |
| --------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| limit     | Yes      | The maximum number of orders that can be returned, this supported maximum number is 100                                                                                             |
| offset    | Yes      | The number of lines to retrieve the next batch of records. For example, if your limit is 100, specifying an offset of 10 will return records 10. If not specified, the default is 0 |

**Responses**

> The above request will return response like this:

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

<!-- Converted with the swagger-to-slate https://github.com/lavkumarv/swagger-to-slate -->
