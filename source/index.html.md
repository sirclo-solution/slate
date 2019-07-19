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
            "delivery_name" : "Artia",
            "delivery_email" : "artia@gmail.com",
            "delivery_street_address" : "Jl. Anggrek No.106 Blok C5",
            "delivery_region" : "DKI Jakarta",
            "delivery_city" : "Kota Jakarta Barat - Cengkareng",
            "delivery_country" : "Indonesia",
            "delivery_post_code" : "11720",
            "delivery_method" : "JNE REG",
            "delivery_mobile" : "082101871618",
            "airwaybill_number" : "",
            "currency_code" : "", 
            "subtotal" : "103000",
            "discount_total" : "0",
            "shipping_total" : "15000",
            "tax_total" : "0",
            "total" : "103000", 
            "line_item" : 
                {
                    "id" : 3,   
                    "sku" : "DKL0907",
                    "name" : "Product",
                    "quantity" : 2,
                    "unit_price" : "40000",
                    "total_price" : "80000",
                    "discount" : "",
                    "tax" : "8000",
                    "shipping_total" : "15000",
                    "total" : "103000",
                    "created_at" :"2018-11-07T03:46:16.457936Z",
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
|subtotal               | No       | double   | subtotal of orders          | 
|discount_total         | No       | double   | discount total all orders  |
|shipping_total         | No       | double   | shipping total all orders  |
|tax_total              | No       | double   | tax total all orders       |
|total                  | No       | double   | total all orders           |
| product_code          | No       | string   | product code               |
| product_description   | No       | string   | product description        |
| quantity              | No       | integer  | quantity of order line item|
| unit price            | No       | double   | unit price product in line item |
| total_price           | No       | double   | total price product in line item |
| discount              | No       | double   | discount product in line item |
| tax                   | No       | double   | tax order in line item |
| shipping_total        | No       | double   | shipping total in line item |
| total                 | No       | double   | total in order line item   |

> This request orders parameter in body : 

```json
    [
        {
            "customer_reference" : "DHU9868NGY",
            "status" : "",
            "delivery_name" : "Artia",
            "delivery_email" : "artia@gmail.com",
            "delivery_street_address" : "Jl. Anggrek No.106 Blok C5",
            "delivery_region" : "DKI Jakarta",
            "delivery_city" : "Kota Jakarta Barat - Cengkareng",
            "delivery_country" : "Indonesia",
            "delivery_post_code" : "11720",
            "delivery_method" : "JNE REG",
            "delivery_mobile" : "082101871618",
            "airwaybill_number" : "",
            "currency_code" : "", 
            "subtotal" : "103000",
            "discount_total" : "0",
            "shipping_total" : "15000",
            "tax_total" : "0",
            "total" : "103000",     
            "line_item" : [
                { 
                    "sku" : "DKL0907",
                    "name" : "Product",
                    "quantity" : 2,
                    "unit_price" : "40000",
                    "total_price" : "80000",
                    "discount" : "",
                    "tax" : "8000",
                    "shipping_total" : "15000",
                    "total" : "103000",
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
            "subtotal" : "103000",
            "discount_total" : "0",
            "shipping_total" : "15000",
            "tax_total" : "0",
            "total" : "103000",    
            "line_item" : [
                {
                    "id" : 3,   
                    "sku" : "DKL0907",
                    "name" : "Product",
                    "quantity" : 2,
                    "unit_price" : "40000",
                    "total_price" : "80000",
                    "discount" : "",
                    "tax" : "8000",
                    "shipping_total" : "15000",
                    "total" : "103000",
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
        "id" : 2,
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
        "airwaybill_number" : "",
        "currency_code" : "",
        "subtotal" : "103000",
        "discount_total" : "0",
        "shipping_total" : "15000",
        "tax_total" : "0",
        "total" : "103000", 
        "line_item": 
            {
                "id" : 3,   
                "sku" : "DKL0907",
                "name" : "Product",
                "quantity" : 2,
                "unit_price" : "40000",
                "total_price" : "80000",
                "discount" : "",
                "tax" : "8000",
                "shipping_total" : "15000",
                "total" : "103000",
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
