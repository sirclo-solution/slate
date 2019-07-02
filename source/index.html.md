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

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | header  |             | Yes      | string |
| api_secret | header |           |          |        | 
| start  | url   |             |          |        | 
| end    | url   |             |          |        |  

**Responses**

> The above command returns JSON structured like this:

```json
{
    "orders": [
        {
            "id": 111,
            "created_at": "2018-11-07T03:46:16.457936Z",
            "updated_at": "2018-11-07T03:46:16.457938Z",
            "order_number": "",
            "order_date": "2018-11-07T03:40:57Z",
            "customer_code": "",
            "remote_order_id": "1362230256",
            "currency_code": "IDR",
            "exchange_rate": 1,
            "customer_reference": "181362230256",
            "quote_expiry_date": "0001-01-01T00:00:00Z",
            "required_date": "0001-01-01T00:00:00Z",
            "warehouse_code": "",
            "payment_method": "",
            "delivery_name": "Danny",
            "delivery_street_address": "Jl Biak no 19C\r\nsebelah Bank Permata",
            "delivery_street_address_2": "",
            "delivery_suburb": "Gambir",
            "delivery_city": "Jakarta Pusat",
            "delivery_region": "DKI Jakarta",
            "delivery_post_code": "10150",
            "delivery_country": "Indonesia",
            "delivery_method": "JNE REG",
            "delivery_number": "",
            "delivery_method_code": "",
            "delivery_enterprise_code": "",
            "delivery_enterprise_name": "",
            "buyer_delivery_number": "",
            "remote_order_status": "pending",
            "discount": 0,
            "tax_code": "PPN",
            "tax_rate": 0.1,
            "tax_total": 0,
            "shipping_total": 45000,
            "discount_total": 0,
            "subtotal": 2500,
            "total": 47500,
            "order_status": "",
            "remarks": "",
            "marketplace_code": "bklp",
            "phone_number": "087867255331",
            "airwaybill_number": "",
            "shipment_reference": "",
            "shipment_extras": "",
            "processed_at": "0001-01-01T00:00:00Z",
            "accepted_at": "0001-01-01T00:00:00Z",
            "packed_at": "0001-01-01T00:00:00Z",
            "cancelled_at": "0001-01-01T00:00:00Z",
            "shipment_tracked_at": "0001-01-01T00:00:00Z",
            "edited_at": "0001-01-01T00:00:00Z",
            "exported_at": "0001-01-01T00:00:00Z",
            "printed_at": "0001-01-01T00:00:00Z",
            "accepted_by": 0,
            "packed_by": 0,
            "cancelled_by": 0,
            "printed_by": 0,
            "line_items": null,
            "store_id": 4,
            "store_name": "",
            "comment": "",
            "price_adjustment": 0,
            "edit_reason": "",
            "cancel_reason": ""
        },
    ]
}
```

## Create Order


**Description:** Post Order 


### HTTP Request 
`**POST** https://api2.connexi.id.dmmy.me/v1/order` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | header  |             | Yes      | string |
| api_secret | header |           |          |        | 
| Orders  | body   |              |        |        | 
 
**Request Body**
> 

**Responses**

> The above command returns JSON structured like this:


## Update Order


**Description:** Update Order 


### HTTP Request 

`**PATCH** https://api2.connexi.id.dmmy.me/v1/order` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | header  |             | Yes      | string |
| api_secret | header |           |          |        | 
| Orders  | body  |               |          |        | 
 
**Request Body**
> This request order in body : 

```json
[
    {
        "id" : "int",
        "status" : "string"
    }
]
```

**Responses**

> The above command returns JSON structured like this:

# Product 

## Get Stocks 

**Summary: Get All Stocks**

### HTTP Request  

`**GET** https://api2.connexi.id.dmmy.me/v1/product/stocks`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | header  |             | Yes      | string |
| api_secret | header |           |          |        | 
| start  | url   |             |          |        | 
| end    | url   |             |          |        | 

**Responses**

> The above command returns JSON structured like this:

```json
{
    "locations": [
        {
            "location_code": "ID",
            "provider_data": "INDONESIA",
            "provinces": [
                {
                    "location_code": "ID-AC",
                    "provider_data": "NANGGROE ACEH DARUSSALAM (NAD)",
                    "cities": [
                        {
                            "location_code": "ID-AC01",
                            "provider_data": "ACEH BARAT",
                            "districts": [
                                {
                                    "location_code": "ID-AC0101",
                                    "provider_data": "ACEH BARAT-ARONGAN LAMBALEK"
                                },
                                {
                                    "location_code": "ID-AC0102",
                                    "provider_data": "ACEH BARAT-BUBON"
                                },
                                {
                                    "location_code": "ID-AC0103",
                                    "provider_data": "ACEH BARAT-JOHAN PAHLAWAN"
                                },
                                {
                                    "location_code": "ID-AC0104",
                                    "provider_data": "ACEH BARAT-KAWAY XVI"
                                },
                                {
                                    "location_code": "ID-AC0105",
                                    "provider_data": "ACEH BARAT-MEUREUBO"
                                },
                                {
                                    "location_code": "ID-AC0106",
                                    "provider_data": "ACEH BARAT-PANTE CEUREUMEN (PANTAI CEUREMEN)"
                                },
                                {
                                    "location_code": "ID-AC0107",
                                    "provider_data": "ACEH BARAT-PANTON REU"
                                },
                                {
                                    "location_code": "ID-AC0108",
                                    "provider_data": "ACEH BARAT-SAMATIGA"
                                },
                                {
                                    "location_code": "ID-AC0109",
                                    "provider_data": "ACEH BARAT-SUNGAI MAS"
                                },
                                {
                                    "location_code": "ID-AC010A",
                                    "provider_data": "ACEH BARAT-WOYLA"
                                },
                                {
                                    "location_code": "ID-AC010B",
                                    "provider_data": "ACEH BARAT-WOYLA BARAT"
                                },
                                {
                                    "location_code": "ID-AC010C",
                                    "provider_data": "ACEH BARAT-WOYLA TIMUR"
                                }
                            ]
                        }
                     ]
                },
```

<!-- Converted with the swagger-to-slate https://github.com/lavkumarv/swagger-to-slate -->
