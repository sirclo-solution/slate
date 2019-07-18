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

|Environment | Host URL               | 
|------------|------------------------|
|Production  |https://api2.connexi.id |

### HTTP Request 

`GET /v1/order/:start/:end`

### Path Parameters 

| Parameter |  Description     |
|-----------|------------------|
|start      |fulfillment start |
|end        |fulfillment end   |

### Header Parameters

| Name       |  Required |Description                       |
| -----------|  -------- |--------------------------------- |
| api_key    | Yes       | api key used to authentication   |
| api_secret | Yes       | api secret used to authentication| 

**Responses**

> The above command returns JSON structured like this:

```json
    [
        {
            "id" : 2,
            "customer_reference" : "DHU9868NGY",
            "status" : "accepted",
            "delivery_name" : "Angga",
            "delivery_email" : "angga@gmail.com",
            "delivery_street_address" : "Jl. Anggrek No.106 Blok C5",
            "delivery_region" : "DKI Jakarta",
            "delivery_city" : "Kota Jakarta Barat - Cengkareng",
            "delivery_country" : "Indonesia",
            "delivery_post_code" : "11720",
            "delivery_method" : "JNE REG",
            "delivery_mobile" : "082101871618",
            "airwaybill_number" : "",
            "currency_code" : "", 
            "subtotal" : "489000",
            "discount_total" : "0",
            "shipping_total" : "27000",
            "tax_total" : "0",
            "total" : "75900", 
            "line_item" : 
                {
                    "id" : 3,
                    "sku" : "DKL0907",
                    "quantity" : 2,
                    "total" : "80000",
                    "created_at" : "2018-11-07T03:46:16.457936Z",
                    "update_at" : "2018-11-07T03:46:16.457938Z",
                },
            "created_at" : "2018-11-07T03:46:16.8927649",
            "updated_at" : "2018-11-07T03:55:20.149784Z"
        }
    ]
```

## Create Order


**Description:** Use this endpoint to create order in connexi from partner system. 


### HTTP Request 
`POST https://api2.connexi.id/v1/order`

**Header Parameters**

| Name       |  Required | Type   |Description                       |
| -----------|  -------- | ------ |----------------------------------|
| api_key    | Yes       | string | api key used to authentication   |
| api_secret | Yes       | string | api secret used to authentication| 

### Request Body 

   **Request body parameter must be in the form JSON**

|   Name                | Required | Type     | Description                |
| ----------------------| ---------| -------- | -------------------------- | 
|customer_reference     | No       | string   | customer reference         |
|shipment_reference     | Yes      | string   | shipment reference         |
|status                 | No       | string   | Status of orders           | 
|delivery_name          | No       | string   | deliery name               |
|delivery_email         | No       | string   | delivery email             |
|delivery_street_address| No       | string   | delivery address           |
|delivery_region        | No       | string   | delivery region            |
|delivery_city          | No       | string   | delivery city              |
|delivery_country       | No       | string   | delivery country           |
|delivery_post_code     | No       | string   | delivery post code         |
|delivery_method        | No       | string   | delivery method            |
|delivery_mobile        | No       | string   | delivery mobile number     |
|airwaybill_number      | No       | string   | airwaybill number          |
|currency_code          | No       | string   | currency code              |
|subtotal               | No       | double   | subtotal of order          | 
|discount_total         | No       | double   | discount total             |
|shipping_total         | No       | double   | shipping total             |
|tax_total              | No       | double   | tax total                  |
|total                  | No       | double   | total all orders           |
| product_code          | No       | string   | product code               |
| product_description   | No       | string   | product description        |
| quantity              | No       | integer  | quantity of order line item|
| total                 | No       | double   | total in order line item   |

> This request orders parameter in body : 

```json
    [
        {
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
            "total" : "double",    
            "line_item" : [
                {
                   "sku" : "string",
                   "name" : "string",
                   "quantity" : "integer",
                   "id" : "integer",
                   "total" :"double"
                }
            ],
        }
    ]
```

> The above command returns JSON structured like this:

```json
     [
        {
            "id" : 2,
            "customer_reference" : "JNH7438B",
            "shipment_reference" : "",
            "status" : "pending",
            "delivery_name" : "Artia",
            "delivery_email" : "artia2@gmail.com",
            "delivery_street_address" : "Jl. Anggrek No.106 Blok C5",
            "delivery_region" : "DKI Jakarta",
            "delivery_city" : "Kota Jakarta Barat - Cengkareng",
            "delivery_country" : "Indonesia", 
            "delivery_post_code" : "11720",
            "delivery_method" : "JNE REG",
            "delivery_mobile" : "082101871618",
            "airwaybill_number" : "",
            "currency_code" : "",
            "subtotal" : "489000",
            "discount_total" : "0",
            "shipping_total" : "27000",
            "tax_total" : "0",
            "total" : "75900",    
            "line_item" : [
                {
                    "id" : 2,
                    "sku" : "CKS973",
                    "quantity" : 4,
                    "total" : "800000",
                    "created_at" : "2018-11-07T03:46:16.457936Z",
                    "update_at" : "2018-11-07T03:46:16.457938Z",
                }
            ],
            "created_at" : "2018-11-07T03:46:16.8927649",
            "updated_at" : "2018-11-07T03:55:20.149784Z"
        }
    ]
```

## Update Order


**Description:** This endpoint used to update order from partner system.  


### HTTP Request 

`PATCH https://api2.connexi.id/v1/order` 

### Header Parameters

| Name      |  Required | Type   |Description         |
| ----------|---------- | ----   |------------------- |
| api_key   | Yes       | string |api key used to authentication | 
| api_secret| Yes       | string |api secret used to authentication | 
 
###Request Body

**Request body parameter must be in the form JSON**

> This request orders parameter in body : 

```json
[
    {
        "id" : "integer",
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
    }
]
```

> The above command returns JSON structured like this:

```json 
[
    {
        "id" : 55,
        "customer_reference" : "GHG867V",
        "shipment_reference" : "",
        "status" : "cancelled",
        "delivery_name" : "Artia",
        "delivery_email" : "artia2@gmail.com",
        "delivery_street_address" : "Jl. Anggrek No.106 Blok C5",
        "delivery_region" : "DKI Jakarta",
        "delivery_city" : "Kota Jakarta Barat - Cengkareng",
        "delivery_country" : "Indonesia", 
        "delivery_post_code" : "11720",
        "delivery_method" : "JNE REG",
        "delivery_mobile" : "082101871618",
        "airwaybill_number" : "",
        "currency_code" : "",
        "subtotal" : "489000",
        "discount_total" : "0",
        "shipping_total" : "27000",
        "tax_total" : "0",
        "total" : "75900",
        "line_item": 
            {
                "id" : 2,
                "product_code" : "CKS973",
                "product_description" : "",
                "quantity" : 4,
                "total" : "800000",
                "created_at" : "2018-11-07T03:46:16.457936Z",
                "update_at" : "2018-11-07T03:46:16.457938Z",
            },
        "created_at" : "2018-11-07T03:46:16.8927649",
        "updated_at" : "2018-11-07T03:55:20.149784Z"
    }
]
```

# Product 

## Get Stocks 

Description : This endpoint used to get stock from partner system. 

|Environment | Host URL               | 
|------------|------------------------|
|Production  |https://api2.connexi.id |

### HTTP Request  

`GET /v1/product/stocks/:start/:end`

### Path Parameters 

| Parameter |  Description     |
|-----------|------------------|
|start      |fulfillment start |
|end        |fulfillment end   |

### Header Parameters

| Name       |  Required |Description                       |
| -----------|  -------- |--------------------------------- |
| api_key    | Yes       | api key used to authentication   |
| api_secret | Yes       | api secret used to authentication| 


**Responses**

> The above command returns JSON structured like this:

```json
[
    {
        "id" : 5,
        "sku" : "DR0003",
        "name" : "product",
        "available" : "20",
        "created_at" : "2018-11-07T03:46:16.457936Z",
        "update_at" : "2018-11-07T03:46:16.457938Z"
    }
]
```

<!-- Converted with the swagger-to-slate https://github.com/lavkumarv/swagger-to-slate -->
