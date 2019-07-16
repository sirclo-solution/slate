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
You can used this API to connect your backend system to Sirclo system. 

**Version:** 1.0 

# Order API 
## Get Order 


**Description:** This endpoint used to get all orders in partner system.   


### HTTP Request 

`GET https://api2.connexi.id/v1/order`

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
    [
        {
            "id" : 2,
            "order_number" : "60",
            "customer_reference" : "",
            "status" : "",
            "delivery_name" : "Angga",
            "delivery_email" : "",
            "delivery_street_address" : "Melati 6 no 38 Kapuk Cengkareng",
            "delivery_region" : "DKI Jakarta",
            "delivery_city" : "Kota Jakarta Barat - Cengkareng",
            "delivery_country" : "Indonesia",
            "delivery_post_code" : "11720",
            "delivery_method" : "JNE REG",
            "delivery_mobile" : "",
            "airwaybill_number" : "",
            "currecycode" : "", 
            "subtotal"``` : "489000",
            "discount_total" : "0",
            "shipping_total" : "27000",
            "tax_total" : "",
            "total" : "", 
            "order_line_item" : 
                {
                    "id" : ,
                    "sku" : "",
                    "quantity" : "",
                    "total" : "",
                    "created_at" : "",
                    "update_at" : "",
                },
            "shipment_tracked_at" : "",
            "created_at" : "",
            "updated_at" : ""
        }
    ]
```

## Create Order


**Description:** Use this endpoint to create order in connexi from partner system. 


### HTTP Request 
`POST https://api2.connexi.id/v1/order`

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
|customer_reference     | No       | string   | customer reference         |
|shipment_reference     | Yes      | text     | shipment reference         |
|status                 |          | text     | Status of orders           | 
|delivery_name          | No       | string   | deliery name               |
|delivery_email         |          | string   |                            |
|delivery_street_address| No       | text     | delivery address           |
|delivery_region        | No       | string   | delivery region            |
|delivery_city          | No       | string   | delivery city              |
|delivery_country       | No       | string   | delivery country           |
|delivery_post_code     | No       | string   | delivery post code         |
|delivery_method        | No       | string   | delivery method            |
|delivery_mobile        |          |          |                            |
|airwaybill_number      | No       | string   | airwaybill number          |
|currencycode           |          |          |                            |
|subtotal               | No       | double   | subtotal                   | 
|discount_total         | No       | double   | discount total             |
|shipping_total         | No       | double   | shipping total             |
|tax_total              | No       | double   | tax total                  |
|total                  |          |          |                            |
| product_code          | No       | string   | product code               |
| product_description   | No       | text     | product description        |
| order_quantity        | No       | integer  | order quantity             |
| line_total            | No       | double   | line total                 |
| created_at            |          |          |                            |
| updated_at            |          |          |                            |
|shipment_tracked_at    | No       | timestamp| shipment tracked at        |

 
**Request Body**

```json
    [
        {
            "order_number" : "string",
            "customer_reference" : "string",
            "shipment_reference" : "text",
            "status" : "string",
            "delivery_name" : "string",
            "delivery_email" : "string",
            "delivery_street_address" : "text",
            "delivery_region" : "string",
            "delivery_city" : "string",
            "delivery_country" : "string", 
            "delivery_post_code" : "string",
            "delivery_method" : "string",
            "delivery_mobile" : "string",
            "airwaybill_number" : "string",
            "currency_code" : "",
            "subtotal" : "double",
            "discount_total" : "double",
            "shipping_total" : "double",
            "tax_total" : "double",
            "total" : "",    
            "line_item" : [
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
            ],
            "shipment_tracked_at" : "timestamp",
        }
    ]
```

> The above command returns JSON structured like this:

```json
     [
        {
            "order_number" : "string",
            "customer_reference" : "string",
            "shipment_reference" : "text",
            "status" : "string",
            "delivery_name" : "string",
            "delivery_email" : "string",
            "delivery_street_address" : "text",
            "delivery_region" : "string",
            "delivery_city" : "string",
            "delivery_country" : "string", 
            "delivery_post_code" : "string",
            "delivery_method" : "string",
            "delivery_mobile" : "string",
            "airwaybill_number" : "string",
            "currency_code" : "",
            "subtotal" : "double",
            "discount_total" : "double",
            "shipping_total" : "double",
            "tax_total" : "double",
            "total" : "",    
            "line_item" : [
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
            ],
            "shipment_tracked_at" : "timestamp",
             "created_at" : "",
             "updated_at" : ""
        }
    ]
```

## Update Order


**Description:** This endpoint used to update order from partner system.  


### HTTP Request 

`PATCH https://api2.connexi.id/v1/order` 

**Parameters**

| Name      | Located in |  Required | Type   |Description         |
| ----------| ---------- |---------- | ----   |------------------- |
| api_key   | header     | Yes       | string |api key to authentication | 
| api_secret| header     | Yes       | string |api secret to authentication | 
| Orders    | body       | Yes       |        |request orders parameter with json format in body| 
 
###Request Body

**Request body parameter must be in the form JSON**

> This request orders parameter in body : 

```json
[
    {
        "id" : "integer",
        "shipment_reference" : "",
        "status" : "string",
        "delivery_name" : "",
        "delivery_email" : "",
        "delivery_street_address" : "", 
        "delivery_region" : "",
        "delivery_city" : "",
        "delivery_country" : "",
        "delivery_post_code" : "",
        "delivery_method" : "",
        "delivery_mobile" : "",
        "airwaybill_number" : "", 
    }
]
```

> The above command returns JSON structured like this:

```json 
[
    {
        "id" : 55,
        "order_number" : "",
        "customer_reference" : "",
        "shipment_reference" : "",
        "status" : "accepted",
        "delivery_name" : "",
        "delivery_email" : "",
        "delivery_street_address" : "", 
        "delivery_region" : "",
        "delivery_city" : "",
        "delivery_country" : "",
        "delivery_post_code" : "",
        "delivery_method" : "",
        "delivery_mobile" : "",
        "airwaybill_number" : "", 
        "currency_code" : "",
        "subtotal" : "",
        "discount_total" : "",
        "shipping_total" : "",
        "tax_total" : "",
        "total" : "",
        "line_item": 
        {
            "id" : "",
            "product_code" : "",
            "product_description" : "",
            "order_quantity" : "",
            "line_total" : "",
            "created_at" : "",
            "update_at" : "",
        },
        "shipment_tracked_at" : "",
        "created_at" : "",
        "updated_at" : "",
    }
]
```

# Product 

## Get Stocks 

Description : This endpoint used to get all stocks from partner system. 

### HTTP Request  

`GET https://api2.connexi.id/v1/product/stocks`

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
[
    {
        "id" : 5,
        "SKU" : "DR0003",
        "name" : "",
        "available" : "",
        "created_at" : "",
        "update_at" : ""
    }
]
```

<!-- Converted with the swagger-to-slate https://github.com/lavkumarv/swagger-to-slate -->
