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

# Authentication 

Authentication & Authorization is handled by Oauth from Sirclo account module.

<aside class="notice">
All request to fulfillment control are authenticated and authorized using a mechanism discussed in <code>Authentication</code> Section.
</aside>

<aside class="warning">
Don't share your <code>client_secret</code> and <code>access_token</code> with anyone. Protect it
</aside>

# Order API 
## Get Order 


**Description:** Get Order from Connexi  


### HTTP Request 

`**GET** https://api2.connexi.id.dmmy.me/v1/order`

**Parameters**

| Name       | Located in |  Required | Type   |Description |
| ---------- | ---------- |  -------- | ------ |----------- |
| api_key    | header     |  Yes      | string |            |
| api_secret | header     |           |        |            | 
| start      | url        |           |        |            |
| end        | url        |           |        |            |   

**Responses**

> The above command returns JSON structured like this:

```json
    [
        {
            "order_number" : "",
            "quote_expiry_date" : "",
            "required_date" : "",
            "customer_code" : "",
            "remote_order_id" : "",
            "currency_code" : "",
            "exchange_rate" : "",
            "total" : "",
            "customer_reference" : "",
            "payment_method" : "",
            "delivery_name" : "",
            "delivery_street_address" : "",
            "delivery_street_address" : "",
            "delivery_suburb" : "",
            "delivery_city" : "",
            "delivery_region" : "",
            "delivery_post_code" : "",
            "delivery_country" : "",
            "delivery_method" : "",
            "delivery_number" : "",
            "delivery_method_code" : "",
            "remote_order_status" : "",
            "discount" : "",
            "tax_code" : "",
            "tax_rate" : "",
            "tax_total" : "",
            "order_status" : "",
            "remarks" : "",
            "marketplace_code" : "",
            "phone_number" : "",
            "airwaybill_number" : "",
            "buyer_delivery_number" : "",
            "subtotal" : "",
            "discount_total" : "",
            "shipping_total" : "",
            "shipment_tracked_at" : "",
            "raw" : "",
            "accepted_at" : "",
            "accepted_by" : "",
            "cancelled_at" : "",
            "cancelled_by" : "",
            "cancel_reason" : "",
            "packed_at" : "",
            "packed_by" : "",
            "comment" : "",
            "price_adjustment" : "",
            "processed_at" : "",
            "shipment_reference" : "",
            "shipment_extras" : "",
            "edited_at" : "",
            "edit_reason" : "",
            "completed_by" : "",
            "completed_at" : "",
            "received_by" : "",
            "received_at" : "",
            "order_line_item" : [
                {
                    "line_number" : "",
                    "remote_order_item_id" : "",
                    "product_code" : "",
                    "product_description" : "",
                    "order_quantity" : "",
                    "unit_price" : "",
                    "raw_price" : "",
                    "discount_rate" : "",
                    "line_discount" : "",
                    "line_tax" : "",
                    "shipping_amount" : "",
                    "line_total" : "",
                    "line_comments" : "",
                    "line_item_status" : "",
                    "description" : "",
                }
            ]
        }
    ]
```

## Create Order


**Description:** Post Order 


### HTTP Request 
`**POST**, https://api2.connexi.id.dmmy.me/v1/order`

**Parameters**

| Name       | Located in  |  Required | Type   |Description |
| -----------| ------------|  -------- | ------ |----------- |
| api_key    | header      | Yes       | string |            |
| api_secret | header      |           |        |            | 
| Orders     | body        |           |        |            |

### Request Body 
   **Request body parameter must be in the form JSON**

|   Name                | Required | Type     | Description                |
| ----------------------| ---------| -------- | -------------------------- |
|order_number           | No       | string   | order number               |   
|quote_expiry_date      | No       | timestamp| quote expiry date of order |
|required_date          | No       | timestamp|                            |
|customer_code          | No       | string   |                            |
|currency_code          | No       | string   |                            |
|exchange_rate          | No       | double   |                            |
|total                  | No       | double   |                            |
|customer_reference     | No       | string   |                            |
|payment_method         | No       | string   |                            |
|delivery_name          | No       | string   |                            |
|delivery_street_address| No       | text     |                            |
|delivery_street_address_2| No     | text     |                            |
|delivery_suburb        | No       | string   |                            |
|delivery_city          | No       | string   |                            |
|delivery_region        | No       | string   |                            |
|delivery_post_code     | No       | string   |                            |
|delivery_country       | No       | string   |                            |
|delivery_method        | No       | string   |                            |
|delivery_method_code   | No       | string   |                            |
|remote_order_status    | Yes      | string   |                            |  
|discount               | No       | double   |                            |
|tax_code               | No       | string   |                            |
|tax_rate               | No       | double   |                            |
|tax_total              | No       | double   |                            |
|order_status           | No       | string   |                            |
|remarks                | No       | text     |                            |
|marketplace_code       | No       | string   |                            |
|phone_number           | No       | string   |                            |
|airwaybill_number      | No       | string   |                            |
|buyer_delivery_number  | No       | string   |                            |
|subtotal               | No       | double   |                            | 
|discount_total         | No       | double   |                            |
|shipping_total         | No       | double   |                            |
|shipment_tracked_at    | No       | timestamp|                            |
|raw                    | No       | text     |                            |
|accepted_at            | Yes      | timestamp|                            |
|accepted_by            | No       | integer  |                            |
|cancelled_at           | No       | timestamp|                            |
|cancelled_by           | No       | integer  |                            |
|cancel_reason          | No       | string   |                            | 
| packed_at             | Yes      | timestamp|                            |
| packed_by             | No       | integer  |                            |
| comment               | No       | text     |                            |
| price_adjustment      | No       | double   |                            |
| processed_at          | No       | timestamp|                            |
| shipment_reference    |Yes       | text     |                            |
| shipment_extras       | No       | jsonb    |                            |
| edited_at             | No       | timestamp|                            | 
| edit_reason           | No       | text     |                            |
| completed_by          | No       | integer  |                            |
| completed_at          | Yes      | timestamp|                            |
| received_by           | No       | string   |                            |
| received_at           | No       | timestamp|                            |
| line_number           | No       | integer  |                            |
| remote_order_item_id  | No       | string   |                            |
| product_code          | No       | string   |                            |
| product_description   | No       | text     |                            |
| order_quantity        | No       | integer  |                            |
| unit_price            | No       | double   |                            |
| raw_price             | No       | double   |                            |
| discount_rate         | No       | double   |                            |
| line_discount         | No       | double   |                            |
| line_tax              | No       | double   |                            |
| shipping_amount       | No       | double   |                            |
| line_total            | No       | double   |                            |
| line_comments         | No       | text     |                            |
| line_item_status      | No       | string   |                            |
| discount_amount       | No       | double   |                            |
| description           | No       | text     |                            |
 
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
            "order_number" : "",
            "quote_expiry_date" : "",
            "required_date" : "",
            "customer_code" : "",
            "remote_order_id" : "",
            "currency_code" : "",
            "exchange_rate" : "",
            "total" : "",
            "customer_reference" : "",
            "payment_method" : "",
            "delivery_name" : "",
            "delivery_street_address" : "",
            "delivery_street_address" : "",
            "delivery_suburb" : "",
            "delivery_city" : "",
            "delivery_region" : "",
            "delivery_post_code" : "",
            "delivery_country" : "",
            "delivery_method" : "",
            "delivery_number" : "",
            "delivery_method_code" : "",
            "remote_order_status" : "",
            "discount" : "",
            "tax_code" : "",
            "tax_rate" : "",
            "tax_total" : "",
            "order_status" : "",
            "remarks" : "",
            "marketplace_code" : "",
            "phone_number" : "",
            "airwaybill_number" : "",
            "buyer_delivery_number" : "",
            "subtotal" : "",
            "discount_total" : "",
            "shipping_total" : "",
            "shipment_tracked_at" : "",
            "raw" : "",
            "accepted_at" : "",
            "accepted_by" : "",
            "cancelled_at" : "",
            "cancelled_by" : "",
            "cancel_reason" : "",
            "packed_at" : "",
            "packed_by" : "",
            "comment" : "",
            "price_adjustment" : "",
            "processed_at" : "",
            "shipment_reference" : "",
            "shipment_extras" : "",
            "edited_at" : "",
            "edit_reason" : "",
            "completed_by" : "",
            "completed_at" : "",
            "received_by" : "",
            "received_at" : "",
            "order_line_item" : [
                {
                    "line_number" : "",
                    "remote_order_item_id" : "",
                    "product_code" : "",
                    "product_description" : "",
                    "order_quantity" : "",
                    "unit_price" : "",
                    "raw_price" : "",
                    "discount_rate" : "",
                    "line_discount" : "",
                    "line_tax" : "",
                    "shipping_amount" : "",
                    "line_total" : "",
                    "line_comments" : "",
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

`**PATCH**, https://api2.connexi.id.dmmy.me/v1/order` 

**Parameters**

| Name      | Located in |  Required | Type   |Description         |
| ----------| ---------- |---------- | ----   |------------------- |
| api_key   | header     | Yes       | string |api key             | 
| api_secret| header     |           |        |api secret          | 
| Orders    | body       |           |        |request orders parameter with json format in body| 
 
**Request Body**

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
        "id" : "",
        "status" : ""
    }
]
```

# Product 

## Get Stocks 

**Summary: Get All Stocks**

### HTTP Request  

`**GET**, https://api2.connexi.id.dmmy.me/v1/product/stocks`

**Parameters**

| Name       | Located in |  Required | Type   |Description |
| -----------| ---------- |  -------- | ------ |----------- |
| api_key    | header     | Yes       | string |            |
| api_secret | header     |           |        |            |
| start      | url        |           |        |            | 
| end        | url        |           |        |            | 

**Responses**

> The above command returns JSON structured like this:

```json
    {

    }
```

<!-- Converted with the swagger-to-slate https://github.com/lavkumarv/swagger-to-slate -->
