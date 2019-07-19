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
|Production  |https://api.connexi.id |

### HTTP Request 

`GET /v1/order/:start/:end`

### Header Parameters

| Name       |  Required |Description                       |
| -----------|  -------- |--------------------------------- |
| api_key    | Yes       | api key used to authentication   |
| api_secret | Yes       | api secret used to authentication| 

### Path Parameters 

| Parameter |  Description                                    |
|-----------|-------------------------------------------------|
|start      |ISO 8601 timestamp from which the order requested|
|end        |ISO 8601 timestamp to which the order requested  |

**Responses**

> The above request will return response like this:

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
            "subtotal" : 93000,
            "discount_total" : 10000,
            "shipping_total" : 15000,
            "tax_total" : 0,
            "total" : 93000, 
            "line_item" : 
                {
                    "id" : 3,   
                    "sku" : "DKL0907",
                    "name" : "Product",
                    "quantity" : 2,
                    "unit_price" : 40000,
                    "total_price" : 80000,
                    "discount" : 10000,
                    "tax" : 8000,
                    "shipping_total" : 15000,
                    "total" : 93000,
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
            "currency_code" : "IDR", 
            "subtotal" : 93000,
            "discount_total" : 0,
            "shipping_total" : 15000,
            "tax_total" : 0,
            "total" : 93000,     
            "line_item" : [
                { 
                    "sku" : "DKL0907",
                    "name" : "Product",
                    "quantity" : 2,
                    "unit_price" : 40000,
                    "total_price" : 80000,
                    "discount" :10000 ,
                    "tax" : 8000,
                    "shipping_total" : 15000,
                    "total" : 93000,
                }
            ],
        }
    ]
``` 

> The above request will return response like this:

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
            "currency_code" : "IDR",
            "subtotal" : 93000,
            "discount_total" : 0,
            "shipping_total" : 15000,
            "tax_total" : 0,
            "total" : 93000,    
            "line_item" : [
                {
                    "id" : 3,   
                    "sku" : "DKL0907",
                    "name" : "Product",
                    "quantity" : 2,
                    "unit_price" : 40000,
                    "total_price" : 80000,
                    "discount" :10000 ,
                    "tax" : 8000,
                    "shipping_total" : 15000,
                    "total" : 93000,
                    "created_at" : "2018-11-07T03:46:16.457936Z",
                    "update_at" : "2018-11-07T03:46:16.457938Z",
                }
            ],
            "created_at" : "2018-11-07T03:46:16.8927649",
            "updated_at" : "2018-11-07T03:55:20.149784Z"
        }
    ]
```

|   Name                | Required | Type     | Description                |
| ----------------------| ---------| -------- | -------------------------- | 
|customer_reference     | No       | string   | customer reference         |
|shipment_reference     | Yes      | string   | shipment reference         |
|status                 | No       | string   | status of orders, If status is empty, then it will be assigned as "pending"|
|                       |          |          | The acceptable statuses are:|
|                       |          |          | 1. Pending                  |
|                       |          |          | 2. Accepted                 |       
|                       |          |          | 3. Packed                   |             
|                       |          |          | 4. Shipped                  |             
|                       |          |          | 5. Completed                |
|                       |          |          | 6. Cancelled                |      
|delivery_name          | No       | string   | name of the buyer             |
|delivery_email         | No       | string   | email of the buyer            |
|delivery_street_address| No       | string   | street address of the buyer   |
|delivery_region        | No       | string   | region address of the buyer   |
|delivery_city          | No       | string   | city address of the buyer     |
|delivery_country       | No       | string   | country address of the buyer  |
|delivery_post_code     | No       | string   | post code address of the buyer|
|delivery_method        | No       | string   | the method of delivery     |
|delivery_mobile        | No       | string   | mobile number of the buyer |
|airwaybill_number      | No       | string   | airwaybill number from 3PL |
|currency_code          | No       | string   | currency code              |
|subtotal               | No       | double   | subtotal of orders         | 
|discount_total         | No       | double   | discount total all orders  |
|shipping_total         | No       | double   | shipping total all orders  |
|tax_total              | No       | double   | tax total all orders       |
|total                  | No       | double   | total all orders           |
| product_code          | No       | string   | product code               |
| product_description   | No       | string   | product description        |
| quantity              | No       | integer  | quantity of order line item|
| unit price            | No       | double   | price per unit of product |
| total_price           | No       | double   | total price product in line item |
| discount              | No       | double   | discount product in line item |
| tax                   | No       | double   | tax order in line item |
| shipping_total        | No       | double   | shipping total in line item |
| total                 | No       | double   | total in order line item   |



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

> The above request will return response like this:

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
        "currency_code" : "IDR",
        "subtotal" : 93000,
        "discount_total" : 0,
        "shipping_total" : 15000,
        "tax_total" : 0,
        "total" : 93000, 
        "line_item": 
            {
                "id" : 3,   
                "sku" : "DKL0907",
                "name" : "Product",
                "quantity" : 2,
                "unit_price" : 40000,
                "total_price" : 80000,
                "discount" :10000 ,
                "tax" : 8000,
                "shipping_total" : 15000,
                "total" : 93000,
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
|Production  |https://api.connexi.id  |

### HTTP Request  

`GET /v1/product/stocks/:start/:end`

### Header Parameters

| Name       |  Required |Description                       |
| -----------|  -------- |--------------------------------- |
| api_key    | Yes       | api key used to authentication   |
| api_secret | Yes       | api secret used to authentication| 

### Path Parameters 

| Parameter |  Description                                    |
|-----------|-------------------------------------------------|
|start      |ISO 8601 timestamp from which the order requested|
|end        |ISO 8601 timestamp to which the order requested  |

**Responses**

> The above request will return response like this:

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
