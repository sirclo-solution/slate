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
     [
        {
            "order_id" : 123,
            "order_date" : "2006-01-02T15:04:05Z07:00",
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
            "airwaybill_number" : "AWB12345678",
            "currency_code" : "IDR",
            "subtotal" : 110000,
            "discount_total" : 10000,
            "shipping_total" : 15000,
            "total" : 115000,    
            "line_item" : [
                {
                    "id" : 3,   
                    "sku" : "DKL0907",
                    "name" : "Product ABC",
                    "quantity" : 2,
                    "unit_price" : 100000,
                    "discount" :10000,
                    "shipping_total" : 15000,
                }
            ],
           "total_count" :100,
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
            "order_id": 123,
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
                {   
                    "id" : 3,
                    "sku" : "DKL0907",
                    "name" : "Product ABC",
                    "quantity" : 2,
                    "raw_price" : 100000,
                    "discount" :10000,
                    "shipping_total" : 15000,
                }
            ],
        }
    ]
``` 

> The above request will return response like this:

```json
     [
        {
            "order_id" : 123,
            "order_date" : "2006-01-02T15:04:05Z07:00",
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
            "airwaybill_number" : "AWB12345678",
            "currency_code" : "IDR",
            "subtotal" : 110000,
            "discount_total" : 10000,
            "shipping_total" : 15000,
            "total" : 115000,    
            "line_item" : [
                {
                    "id" : 3,   
                    "sku" : "DKL0907",
                    "name" : "Product ABC",
                    "quantity" : 2,
                    "unit_price" : 100000,
                    "discount" :10000,
                    "shipping_total" : 15000,
                }
            ],
           "total_count" :100,
        }
    ]
```

|   Name                | Required | Type     | Description                |
| ----------------------| ---------| -------- | -------------------------- | 
|customer_reference     | No       | string   | customer reference         |
|shipment_reference     | Yes      | string   | shipment reference         |
|shipment_tracked_at    | No       |Timestamp | this shipment tracked time must be must be in RFC3339 format|
|order_date             | No       |Timestamp | the date of order and must be in RFC3339 format|
|status                 | No       | string   | status of orders, If status is empty, then it will be assigned as "pending"|
|                       |          |          | The acceptable statuses are:|
|                       |          |          | 1. Pending                  |
|                       |          |          | 2. Accepted                 |       
|                       |          |          | 3. Packed                   |             
|                       |          |          | 4. Shipped                  |             
|                       |          |          | 5. Completed                |
|                       |          |          | 6. Cancelled                |      
|delivery_name          | No       | string   | name of the buyer in this order|
|delivery_email         | No       | string   | email address of the buyer in this order|
|delivery_street_address| No       | string   | street address of the buyer   |
|delivery_region        | No       | string   | region address of the buyer   |
|delivery_city          | No       | string   | city address of the buyer     |
|delivery_country       | No       | string   | country address of the buyer  |
|delivery_post_code     | No       | string   | post code address of the buyer|
|delivery_method        | No       | string   | the method of delivery     |
|delivery_mobile        | No       | string   | mobile number of the buyer |
|airwaybill_number      | No       | string   | airwaybill number from 3PL |
|currency_code          | No       | string   | currency code for this order is "IDR"  |
|subtotal               | No       | double   | this total value of order before discount and after tax  
|discount_total         | No       | double   | this total discount value for this order (sum of every line_item.discount)|
|shipping_total         | No       | double   | This total shipping cost value for this order|
|tax_total              | No       | double   | tax total all orders       |
|total                  | No       | double   | this total value of order after discount, tax and shipping cost|
| product_code          | No       | string   | product code               |
| product_description   | No       | string   | product description        |
| quantity              | No       | integer  | quantity of order line item|
| raw_price             | No       | double   | this raw price in order line item after discount and tax)
| total_price           | No       | double   | total price product in line item |
| discount              | No       | double   | discount product in line item |
| tax                   | No       | double   | tax order in line item |
| shipping_total        | No       | double   | this shipping total in line item, can be same value with "shipping_total" above, could be optional  |
|total_count            | No       | integer  | this total count of available records |



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
   "orders": [  
        {  
            "order_id":123,
            "order_status":"accept",
            "updated_at":"2017-05-07 18:06:51",
            "order_number":"order001",
            "airwaybill_number":"",
            "received_by":"",
            "cancel_reason":""
        },
        {  
            "order_id":456,
            "order_status":"pack",
            "updated_at":"2017-05-09 18:06:51",
            "order_number":"order010",
            "airwaybill_number":"awb002",
            "received_by":"",
            "cancel_reason":""
        },
        {  
            "order_id":789,
            "order_status":"complete",
            "updated_at":"2017-05-09 18:06:51",
            "order_number":"order015",
            "airwaybill_number":"awb006",
            "received_by":"Kurniawan",
            "cancel_reason":""
        },
        {  
            "order_id":135,
            "order_status":"cancel",
            "updated_at":"2017-05-09 18:06:51",
            "order_number":"order005",
            "airwaybill_number":"",
            "received_by":"",
            "cancel_reason":"salah beli barang"
        }
    ]
}
```

> The above request will return response like this:

```json
     [
        {
            "order_id" : 123,
            "order_date" : "2006-01-02T15:04:05Z07:00",
            "customer_reference" : "JNH7438B",
            "shipment_reference" : "",
            "status" : "shipped",
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
            "currency_code" : "IDR",
            "subtotal" : 110000,
            "discount_total" : 10000,
            "shipping_total" : 15000,
            "total" : 115000,    
            "line_item" : [
                {
                    "id" : 3,   
                    "sku" : "DKL0907",
                    "name" : "Product ABC",
                    "quantity" : 2,
                    "unit_price" : 100000,
                    "discount" :10000,
                    "shipping_total" : 15000,
                }
            ],
           "total_count" :100,
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
[
    {
        "id" : 5,
        "sku" : "DKL0907",
        "name" : "product ABC ",
        "available" : "20",
        "created_at" : "2018-11-07T03:46:16.457936Z",
        "update_at" : "2018-11-07T03:46:16.457938Z"
    }
]
```

<!-- Converted with the swagger-to-slate https://github.com/lavkumarv/swagger-to-slate -->
