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

```query {
    salesOrders {
        id
        orderNumber
        customerReference
        status
        deliveryName
        deliveryEmail
        deliveryStreetAddress
        deliveryRegion
        deliveryCity
        deliveryCountry
        deliveryPostCode
        deliveryMethod
        deliveryMobile
        airwaybillNumber
        currencyCode
        subTotal
        discountTotal
        shippingTotal
        taxTotal
        total
        lineItem {
            id
            sku
            name
            quantity
            total
            createdAt
            updatedAt
        }
        shipmentTrackedAt
        createdAt
        updatedAt
    }
}
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
|status                 | No       | text     | Status of orders           | 
|delivery_name          | No       | string   | deliery name               |
|delivery_email         | No       | string   | delivery email             |
|delivery_street_address| No       | text     | delivery address           |
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
|total                  | No       | double   | total                      |
| product_code          | No       | string   | product code               |
| product_description   | No       | text     | product description        |
| order_quantity        | No       | integer  | order quantity             |
| line_total            | No       | double   | line total                 |
| created_at            | Yes      | timestamp| time of created order      |
| updated_at            | Yes      | timestamp| time of updated order      |
|shipment_tracked_at    | No       | timestamp| shipment tracked at        |

 
**Request Body and response structured like this**

``` json {
    createSalesOrder(
        orderNumber: "orderNumber",
        customerReference: "customerReference",
        shipmentReference: "shipmentReference",
        status: "status",
        deliveryName: "deliveryName",
        deliveryEmail: "deliveryEmail",
        deliveryStreetAddress: "deliveryStreetAddress",
        deliveryRegion: "deliveryRegion",
        deliveryCity: "deliveryCity",
        deliveryCountry: "deliveryCountry",
        deliveryPostCode: "deliveryPostCode",
        deliveryMethod: "deliveryMethod",
        deliveryMobile: "deliveryMobile",
        airwaybillNumber: "airwaybillNumber",
        currencyCode: "currencyCode",
        subTotal: 0,
        discountTotal: 0,
        shippingTotal: 0,
        taxTotal: 0,
        total: 0,
        lineItem: [{
            sku: "sku",
            name: "name",
            quantity: 0,
            total: 0
        }],
        shipmentTrackedAt: "shipmentTrackedAt"
    ) {
        id
        orderNumber
        customerReference
        shipmentReference
        status
        deliveryName
        deliveryEmail
        deliveryStreetAddress
        deliveryRegion
        deliveryCity
        deliveryCountry
        deliveryPostCode
        deliveryMethod
        deliveryMobile
        airwaybillNumber
        currencyCode
        subTotal
        discountTotal
        shippingTotal
        taxTotal
        total
        lineItem {
            id
            sku
            name
            quantity
            total
            createdAt
            updatedAt
        }
        shipmentTrackedAt
        createdAt
        updatedAt
    }
}```

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
        "order_number" : "76",
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
                "sku" : "CKS973",
                "name" : "product",
                "quantity" : 4,
                "total" : "800000",
                "created_at" : "2018-11-07T03:46:16.457936Z",
                "update_at" : "2018-11-07T03:46:16.457938Z",
            },
        "shipment_tracked_at" : "0001-01-01T00:00:00Z",
        "created_at" : "2018-11-07T03:46:16.8927649",
        "updated_at" : "2018-11-07T03:55:20.149784Z"
    }
]
```

# Product 

## Get Stocks 

Description : This endpoint used to get stock from partner system. 

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
        "sku" : "DR0003",
        "name" : "product",
        "available" : "20",
        "created_at" : "2018-11-07T03:46:16.457936Z",
        "update_at" : "2018-11-07T03:46:16.457938Z"
    }
]
```

<!-- Converted with the swagger-to-slate https://github.com/lavkumarv/swagger-to-slate -->
