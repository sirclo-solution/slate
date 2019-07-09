--- 
title: Order 

language_tabs: 
   - shell 

toc_footers: 
   - <a href='#'>Sign Up for a Developer Key</a> 
   - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a> 

includes: 
   - errors 

search: true 

--- 

# Introduction 

**Welcome To SIRCLO API Documentation**
You can used this API to connect your backend system to Sirclo system. 

**Version:** 1.0 

# Order API 
## Get Order 


**Description:** Get Order from Connexi  


### HTTP Request 

`**GET** https://api2.connexi.id/v1/order`

**Parameters**

| Name       | Located in |  Required | Type   |Description |
| -----------| ---------- |  -------- | ------ |----------- |
| api_key    | header     | Yes       | string | api key to authentication  |
| api_secret | header     | Yes       | string | api secret to authenticatio|
| start      | url        | Yes       | timestamp | start date | 
| end        | url        | Yes       | timestamp | end date   |  

**Responses**

> The above command returns JSON structured like this:

```json
    [
        {
            "order_number" : "string",
            "quote_expiry_date" : "timestamp",
            "required_date" : "timestamp",
            "customer_code" : "string",
            "remote_order_id" : "string",
            "currency_code" : "string",
            "exchange_rate" : "double",
            "total" : "double",
            "customer_reference" : "string",
            "payment_method" : "string",
            "delivery_name" : "string",
            "delivery_street_address" : "text",
            "delivery_street_address" : "text",
            "delivery_suburb" : "string",
            "delivery_city" : "string",
            "delivery_region" : "string",
            "delivery_post_code" : "string",
            "delivery_country" : "string",
            "delivery_method" : "string",
            "delivery_number" : "string",
            "delivery_method_code" : "string",
            "remote_order_status" : "string",
            "discount" : "double",
            "tax_code" : "string",
            "tax_rate" : "double",
            "tax_total" : "double",
            "order_status" : "string",
            "remarks" : "text",
            "marketplace_code" : "string",
            "phone_number" : "string",
            "airwaybill_number" : "string",
            "buyer_delivery_number" : "string",
            "subtotal" : "double",
            "discount_total" : "double",
            "shipping_total" : "double",
            "shipment_tracked_at" : "timestamp",
            "raw" : "text",
            "accepted_at" : "timestamp",
            "accepted_by" : "integer",
            "cancelled_at" : "timestamp",
            "cancelled_by" : "integer",
            "cancel_reason" : "string",
            "packed_at" : "timstamp",
            "packed_by" : "integer",
            "comment" : "text",
            "price_adjustment" : "double",
            "processed_at" : "timestamp",
            "shipment_reference" : "text",
            "shipment_extras" : "json",
            "edited_at" : "timestamp",
            "edit_reason" : "text",
            "completed_by" : "integer",
            "completed_at" : "timestamp",
            "received_by" : "string",
            "received_at" : "timestamp",
            "order_line_item" : [
                {
                    "line_number" : "integer",
                    "remote_order_item_id" : "string",
                    "product_code" : "string",
                    "product_description" : "text",
                    "order_quantity" : "integer",
                    "unit_price" : "double",
                    "raw_price" : "double",
                    "discount_rate" : "double",
                    "line_discount" : "double",
                    "line_tax" : "double",
                    "shipping_amount" : "double",
                    "line_total" : "double",
                    "line_comments" : "text",
                    "line_item_status" : "string",
                    "discount_amount" : "double",
                    "description" : "text",
                }
            ]

        }
    ]
```

## Create Order


**Description:** Post Order 


### HTTP Request 
`**POST**, https://api2.connexi.id/v1/order`

**Parameters**

| Name       | Located in  |  Required | Type   |Description |
| -----------| ------------|  -------- | ------ |----------- |
| api_key    | header      | Yes       | string | api key to authentication |
| api_secret | header      | Yes       | string | api secret to authentication| 
| Orders     | body        |           |        | request body with json format|

### Request Body 
   **Request body parameter must be in the form JSON**

|   Name                | Required | Type     | Description                |
| ----------------------| ---------| -------- | -------------------------- |
|order_number           | No       | string   | order number               |   
|quote_expiry_date      | No       | timestamp| quote expiry date of order |
|required_date          | No       | timestamp| required date              |
|customer_code          | No       | string   | customer code              |
|currency_code          | No       | string   | currency code              |
|exchange_rate          | No       | double   | exchange code              |
|total                  | No       | double   | total price                |
|customer_reference     | No       | string   |  customer reference        | 
|payment_method         | No       | string   | payment of method          |
|delivery_name          | No       | string   |deliery name                |
|delivery_street_address| No       | text     |delivery address            |
|delivery_street_address_2| No     | text     | delivery address           |
|delivery_suburb        | No       | string   | delivery suburb            |
|delivery_city          | No       | string   |  delivery city             |
|delivery_region        | No       | string   |  delivery region           |
|delivery_post_code     | No       | string   |  delivery post code        |
|delivery_country       | No       | string   | delivery country           |
|delivery_method        | No       | string   |    delivery method         |
|delivery_method_code   | No       | string   |   delivery method code     |
|remote_order_status    | Yes      | string   |  remote order status       |  
|discount               | No       | double   |    discount                |
|tax_code               | No       | string   |  tax code                  |
|tax_rate               | No       | double   |    tax rate                |
|tax_total              | No       | double   |    tax total               |
|order_status           | No       | string   |     order status           |
|remarks                | No       | text     |    remarks                 |
|marketplace_code       | No       | string   |    marketplace code        |
|phone_number           | No       | string   |   phone number             |
|airwaybill_number      | No       | string   |      airwaybill number     |
|buyer_delivery_number  | No       | string   |    buyer delivery number   |
|subtotal               | No       | double   |   subtotal                 | 
|discount_total         | No       | double   |   discount total           |
|shipping_total         | No       | double   |   shipping total           |
|shipment_tracked_at    | No       | timestamp|   shipment tracked at      |
|raw                    | No       | text     |   raw                      |
|accepted_at            | Yes      | timestamp|   accepted at              |
|accepted_by            | No       | integer  |   accepted by              |
|cancelled_at           | No       | timestamp|   cancelled at             |
|cancelled_by           | No       | integer  |   cancelled by             |
|cancel_reason          | No       | string   |   cancel reason            | 
| packed_at             | Yes      | timestamp|   packed at                |
| packed_by             | No       | integer  |   packed by                |
| comment               | No       | text     |   comment                  |
| price_adjustment      | No       | double   |   price adjustment         |
| processed_at          | No       | timestamp|   processed at             |
| shipment_reference    |Yes       | text     |   shipment reference       |
| shipment_extras       | No       | jsonb    |   shipment extras          |
| edited_at             | No       | timestamp|   edited at                | 
| edit_reason           | No       | text     |   edit reason              |
| completed_by          | No       | integer  |   completed by             |
| completed_at          | Yes      | timestamp|   completed at             |
| received_by           | No       | string   |   received by              |
| received_at           | No       | timestamp|   received at              |
| line_number           | No       | integer  |   line number              |
| remote_order_item_id  | No       | string   |   remote order item id     |
| product_code          | No       | string   |   product code             |
| product_description   | No       | text     |   product description      |
| order_quantity        | No       | integer  |   order quantity           |
| unit_price            | No       | double   |   unit price               |
| raw_price             | No       | double   |   raw price                |
| discount_rate         | No       | double   |   discount rate            |
| line_discount         | No       | double   |   line discount            |
| line_tax              | No       | double   |   line tax                 |
| shipping_amount       | No       | double   |   shipping amount          |
| line_total            | No       | double   |   line total               |
| line_comments         | No       | text     |   line comments            |
| line_item_status      | No       | string   |   line item status         |
| discount_amount       | No       | double   |   discount amount          |
| description           | No       | text     |   description              |
 
**Request Body**

```json
    [
        {
            "order_number" : "string",
            "quote_expiry_date" : "timestamp",
            "required_date" : "timestamp",
            "customer_code" : "string",
            "remote_order_id" : "string",
            "currency_code" : "string",
            "exchange_rate" : "double",
            "total" : "double",
            "customer_reference" : "string",
            "payment_method" : "string",
            "delivery_name" : "string",
            "delivery_street_address" : "text",
            "delivery_street_address" : "text",
            "delivery_suburb" : "string",
            "delivery_city" : "string",
            "delivery_region" : "string",
            "delivery_post_code" : "string",
            "delivery_country" : "string",
            "delivery_method" : "string",
            "delivery_number" : "string",
            "delivery_method_code" : "string",
            "remote_order_status" : "string",
            "discount" : "double",
            "tax_code" : "string",
            "tax_rate" : "double",
            "tax_total" : "double",
            "order_status" : "string",
            "remarks" : "text",
            "marketplace_code" : "string",
            "phone_number" : "string",
            "airwaybill_number" : "string",
            "buyer_delivery_number" : "string",
            "subtotal" : "double",
            "discount_total" : "double",
            "shipping_total" : "double",
            "shipment_tracked_at" : "timestamp",
            "raw" : "text",
            "accepted_at" : "timestamp",
            "accepted_by" : "integer",
            "cancelled_at" : "timestamp",
            "cancelled_by" : "integer",
            "cancel_reason" : "string",
            "packed_at" : "timstamp",
            "packed_by" : "integer",
            "comment" : "text",
            "price_adjustment" : "double",
            "processed_at" : "timestamp",
            "shipment_reference" : "text",
            "shipment_extras" : "json",
            "edited_at" : "timestamp",
            "edit_reason" : "text",
            "completed_by" : "integer",
            "completed_at" : "timestamp",
            "received_by" : "string",
            "received_at" : "timestamp",
            "order_line_item" : [
                {
                    "line_number" : "integer",
                    "remote_order_item_id" : "string",
                    "product_code" : "string",
                    "product_description" : "text",
                    "order_quantity" : "integer",
                    "unit_price" : "double",
                    "raw_price" : "double",
                    "discount_rate" : "double",
                    "line_discount" : "double",
                    "line_tax" : "double",
                    "shipping_amount" : "double",
                    "line_total" : "double",
                    "line_comments" : "text",
                    "line_item_status" : "string",
                    "discount_amount" : "double",
                    "description" : "text",
                }
            ]

        }
    ]
```

> The above command returns JSON structured like this:

```json
    [
        {
            "order_number" : 60,
            "quote_expiry_date" : "0001-01-01T00:00:00Z",
            "required_date" : "0001-01-01T00:00:00Z",
            "customer_code" : "",
            "remote_order_id" : "213",
            "currency_code" : "IDR",
            "exchange_rate" : "1",
            "total" : "16000",
            "customer_reference" : "201800241",
            "payment_method" : "bank-transfer",
            "delivery_name" : "Angga",
            "delivery_street_address" : "Melati 6 no 38 Kapuk Cengkareng",
            "delivery_street_address" : "",
            "delivery_suburb" : "",
            "delivery_city" : "Kota Jakarta Barat - Cengkareng",
            "delivery_region" : "DKI Jakarta",
            "delivery_post_code" : "11720",
            "delivery_country" : "Indonesia",
            "delivery_method" : "JNE REG",
            "delivery_number" : "",
            "delivery_method_code" : "",
            "remote_order_status" : "Shipped",
            "discount" : "0",
            "tax_code" : "PPN",
            "tax_rate" : "0.1",
            "tax_total" : "0",
            "order_status" : "packed",
            "remarks" : "message",
            "marketplace_code" : "src",
            "phone_number" : "087867255331",
            "airwaybill_number" : "",
            "buyer_delivery_number" : "",
            "subtotal" : "489000",
            "discount_total" : "0",
            "shipping_total" : "27000",
            "shipment_tracked_at" : "",
            "raw" : "",
            "accepted_at" : "0001-01-01T00:00:00Z",
            "accepted_by" : "2018-11-06T10:00:11.126466Z",
            "cancelled_at" : "0001-01-01T00:00:00",
            "cancelled_by" : "0001-01-01T00:00:00Z",
            "cancel_reason" : "",
            "packed_at" : "2018-11-06T10:00:11.126466Z",
            "packed_by" : "0",
            "comment" : "test",
            "price_adjustment" : "0",
            "processed_at" : "2018-11-02T02:29:42Z",
            "shipment_reference" : "",
            "shipment_extras" : "",
            "edited_at" : "0001-01-01T00:00:00Z",
            "edit_reason" : "0",
            "completed_by" : "",
            "completed_at" : "",
            "received_by" : "",
            "received_at" : "",
            "order_line_item" : [
                {
                    "line_number" : "2",
                    "remote_order_item_id" : "5",
                    "product_code" : "A-29J",
                    "product_description" : "",
                    "order_quantity" : "2",
                    "unit_price" : "100000",
                    "raw_price" : "0",
                    "discount_rate" : "7",
                    "line_discount" : "0",
                    "line_tax" : "",
                    "shipping_amount" : "",
                    "line_total" : "",
                    "line_comments" : "message",
                    "line_item_status" : "",
                    "description" : "",
                }
            ]

        }
    ]
```

## Update Order


**Description:** Update Order 


### HTTP Request 

`**PATCH**, https://api2.connexi.id/v1/order` 

**Parameters**

| Name      | Located in |  Required | Type   |Description         |
| ----------| ---------- |---------- | ----   |------------------- |
| api_key   | header     | Yes       | string |api key to authentication | 
| api_secret| header     | Yes       | string |api secret to authentication | 
| Orders    | body       | Yes       |        |request orders parameter with json format in body| 
 
**Request Body**
**Request body parameter must be in the form JSON**

> This request orders parameter in body : 

```json
[
    {
        "id" : "int",
        "status" : "string"
    }
]
```

> The above command returns JSON structured like this:

```json 
[
    {
        "id" : "55",
        "status" : "accepted"
    }
]
```

# Product 

## Get Stocks 

**Summary: Get All Stocks**

### HTTP Request  

`**GET**, https://api2.connexi.id/v1/product/stocks`

**Parameters**

| Name       | Located in |  Required | Type   |Description |
| -----------| ---------- |  -------- | ------ |----------- |
| api_key    | header     | Yes       | string | api key to authentication  |
| api_secret | header     | Yes       | string | api secret to authentication|
| start      | url        | Yes       | timestamp | start date | 
| end        | url        | Yes       | timestamp | end date   | 

**Responses**

> The above command returns JSON structured like this:

```json
    {

    }
```

<!-- Converted with the swagger-to-slate https://github.com/lavkumarv/swagger-to-slate -->
