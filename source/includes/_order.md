# Orders

## Get Order

### HTTP Request

`GET /v1/partner/order?since=&until=&limit=&offset=`

### Header Parameters

| Name       | Required | Type   | Description                                                                                                       |
| ---------- | -------- | ------ | ----------------------------------------------------------------------------------------------------------------- |
<<<<<<< HEAD
| partner-id | Yes      | String | Partner ID value (given from SIRCLO) used for partner identification                                              |
=======
| partner_id | Yes      | String | Partner ID value (given from SIRCLO) used for partner identification                                              |
>>>>>>> 13bd2b514ddf525b2b3ee60ab289f4c5f8f270b4
| secret     | Yes      | String | HMAC (Hash Based Message Authentication Code), refer to section: <a href="#composing-secret">Composing Secret</a> |

### Query String Parameters

| Parameter | Required | Type      | Description                                                                                            |
| --------- | -------- | --------- | ------------------------------------------------------------------------------------------------------ |
| since     | Yes      | Timestamp | Start range of order date of the requested orders (must be in RFC3339 format)                          |
| until     | Yes      | Timestamp | End range of order date of the requested orders (must be in RFC3339 format)                            |
| limit     | No       | Integer   | Number of orders that want to be returned (by default the number is 100)                               |
| offset    | No       | Integer   | To be used for pagination (use value 10 if you want to skip 10 first datas, by default the value is 0) |
<<<<<<< HEAD
| withDO    | Yes      | Boolean   | Flag value for determining if the returned sales order data include associated delivery orders or not  |   

> Request example
> `GET /v1/partner/order?since=2018-10-13T13:34:52Z&until=2018-10-16T19:22:39Z&limit=10&offset=0withDO=true`
=======

> Request example
> `GET /v1/partner/order?since=2018-10-13T13:34:52Z&until=2018-10-16T19:22:39Z&limit=100&offset=0`
>>>>>>> 13bd2b514ddf525b2b3ee60ab289f4c5f8f270b4

> The above request returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 1,
<<<<<<< HEAD
      "created_at" : "2019-07-31T07:39:29.646799Z",
      "updated_at" : "2019-07-31T07:39:29.646799Z",
      "order_id": "ABC123",
      "order_date": "2006-01-02T15:04:05Z",
      "customer_reference": "JNH7438B",
      "order_status": "accepted",
=======
      "order_id": "ABC123",
      "order_date": "2006-01-02T15:04:05Z",
      "customer_reference": "JNH7438B",
      "shipment_reference": "",
      "status": "accepted",
>>>>>>> 13bd2b514ddf525b2b3ee60ab289f4c5f8f270b4
      "delivery_name": "Artia",
      "delivery_mobile": "082101871618",
      "delivery_email": "artia2@gmail.com",
      "delivery_street_address": "Jl. Anggrek No.106 Blok C5",
<<<<<<< HEAD
      "delivery_region": "DKI Jakarta",
      "delivery_city": "Kota Jakarta Barat - Cengkareng",
      "delivery_country": "Indonesia",
      "delivery_postcode": "11720",
      "delivery_method": "JNE REG",
      "shipment_reference": "",
      "shipment_tracked_at" : "0001-01-01T00:00:00Z",
      "store_id" : "40",
      "marketplace_code" : "levs",
      "payment_method" : "Bank Transfer", 
=======
      "delivery_city": "Kota Jakarta Barat - Cengkareng",
      "delivery_region": "DKI Jakarta",
      "delivery_country": "Indonesia",
      "delivery_post_code": "11720",
      "delivery_method": "JNE REG",
>>>>>>> 13bd2b514ddf525b2b3ee60ab289f4c5f8f270b4
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
<<<<<<< HEAD
          "created_at" : "2019-07-31T07:39:29.646799Z",
          "updated_at" : "2019-07-31T07:39:29.646799Z",
          "sku": "DKL0907",
          "name": "Product ABC",
          "quantity": 2,
          "unit_price": 100000,
          "discount": 10000,
          "remote_order_item_id" : ""
        }
      ],
       "delivery_orders": [
        {
          "id": 12,
          "sales_order_id": 1,
          "name": "John Doe",
          "created_at": "2006-01-02T15:04:05Z",
          "updated_at": "2006-01-02T15:04:05Z",
          "airwaybill_number": "AWB12345678",
          "do_status": "pending",
          "sent_at": "2006-01-02T15:04:05Z",
          "delivery_lines": [
            {
              "id": 21,
              "name": "ABC partial order delivery",
              "created_at": "2006-01-02T15:04:05Z",
              "updated_at": "2006-01-02T15:04:05Z",
              "product_id" : "ABC123",
              "product_name": "Product ABC", 
              "order_quantity": 1,
              "location": "Stock/Commerce",
            }
          ]
=======
          "sku": "DKL0907",
          "name": "Product ABC",
          "quantity": 2,
          "raw_price": 100000,
          "discount": 10000
>>>>>>> 13bd2b514ddf525b2b3ee60ab289f4c5f8f270b4
        }
      ],
      "created_at": "2019-05-27T06:05:11Z",
      "updated_at": "2019-05-27T06:05:11Z"
<<<<<<< HEAD
    } 
  ],
  "total_record": 1,
  "offset": 0,
  "limit": 10,
=======
    }
  ],
  "total_record": 1,
>>>>>>> 13bd2b514ddf525b2b3ee60ab289f4c5f8f270b4
  "message": "",
  "reference": ""
}
```

## Create Order

### HTTP Request

`POST /v1/partner/order`

### Header Parameters

| Name       | Required | Type   | Description                                                                                                       |
| ---------- | -------- | ------ | ----------------------------------------------------------------------------------------------------------------- |
<<<<<<< HEAD
| partner-id | Yes      | String | Partner ID value (given from SIRCLO) used for partner identification                                              |
=======
| partner_id | Yes      | String | Partner ID value (given from SIRCLO) used for partner identification                                              |
>>>>>>> 13bd2b514ddf525b2b3ee60ab289f4c5f8f270b4
| secret     | Yes      | String | HMAC (Hash Based Message Authentication Code), refer to section: <a href="#composing-secret">Composing Secret</a> |

### Request Body Parameters

Request body must be a JSON document with the following properties

| Name                    | Required | Type      | Description                                                                                                    |
| ----------------------- | -------- | --------- | -------------------------------------------------------------------------------------------------------------- |
| order_id                | Yes      | string    | ID of the order in partner's application                                                                       |
| order_date              | Yes      | Timestamp | The date of order ( must be in RFC3339 format timestamp )                                                      |
| customer_reference      | Yes      | string    | Customer reference value                                                                                       |
| shipment_reference      | No       | string    | Shipment reference value                                                                                       |
| status                  | No       | string    | Status of the order (by default pending if empty. The acceptable status values are:                            |
| 1. Pending              |          |           | Order is received from buyer but not yet accepted/acknowledged by seller.                                      |
| 2. Accepted             |          |           | Order is already accepted by seller. Waiting for buyer payment or seller to send ordered items.                |
| 3. Packed               |          |           | Order is already sent by seller. Order should have airway bill no from 3PL/shipping courier/logistics company. |
| 4. Completed            |          |           | Ordered items is already received by buyer.                                                                    |
| 5. Cancelled            |          |           | Order has been canceled by buyer or seller                                                                     |
| delivery_name           | No       | string    | Name of the buyer/delivery recipient in this order                                                             |
<<<<<<< HEAD
| delivery_email          | No       | string    | Email address of the buyer/delivery recipient in this order                                                    |
| delivery_street_address | No       | string    | Street address for order delivery                                                                              |
| delivery_region         | No       | string    | Region (province/district) of the delivery recipient                                                           |
| delivery_city           | No       | string    | City of the delivery recipient                                                                                 |
| delivery_country        | No       | string    | Country address of the buyer                                                                                   |
| delivery_post_code      | No       | string    | Postal code of the delivery recipient                                                                          |
| delivery_method         | No       | string    | Logistics service information (name of the logistics company/service used for order delivery)                  |
| delivery_mobile         | No       | string    | Mobile number of the delivery recipient                                                                        |
| airwaybill_number       | No       | string    | Airwaybill number from 3PL 3PL (Logistics/Shipping company)                                                    |
| payment_method          | Yes      | string    | Name of payment method                                                                                         |
| shipping_total          | No       | double    | The total shipping cost value for this order                                                                   |
| remote_order_item_id    | No       |           | List of id for any order item                                                                                  |
| line_items              | Yes      | array     |                                                                                                                |
| line_items - name       | Yes      | string    | Name of the line item                                                                                          |
| line_items - sku        | Yes      | string    | SKU of the purchased line item                                                                                 |
| line_items - quantity   | Yes      | integer   | Quantity of the line item                                                                                      |
| line_items - unit_price | Yes      | double    | Unit price of the line item (after discount)                                                                   |
=======
| delivery_mobile         | No       | string    | Mobile number of the delivery recipient                                                                        |
| delivery_email          | No       | string    | Email address of the buyer/delivery recipient in this order                                                    |
| delivery_street_address | No       | string    | Street address for order delivery                                                                              |
| delivery_city           | No       | string    | City of the delivery recipient                                                                                 |
| delivery_region         | No       | string    | Region (province/district) of the delivery recipient                                                           |
| delivery_country        | No       | string    | Country address of the buyer                                                                                   |
| delivery_postcode       | No       | string    | Postal code of the delivery recipient                                                                          |
| delivery_method         | No       | string    | Logistics service information (name of the logistics company/service used for order delivery)                  |
| airwaybill_number       | No       | string    | Airwaybill number from 3PL 3PL (Logistics/Shipping company)                                                    |
| shipping_total          | No       | double    | The total shipping cost value for this order                                                                   |
| line_items              | Yes      | array     |                                                                                                                |
| line_items - sku        | Yes      | string    | SKU of the purchased line item                                                                                 |
| line_items - quantity   | Yes      | integer   | Quantity of the line item                                                                                      |
| line_items - raw_price  | Yes      | double    | Unit price of the line item (after discount)                                                                   |
>>>>>>> 13bd2b514ddf525b2b3ee60ab289f4c5f8f270b4
| line_items - discount   | Yes      | double    | Discount value applied on the line item                                                                        |

> Request body example:

```json
{
<<<<<<< HEAD
  "orders" :
  [
    {
      "order_id": "ORD-123",
      "order_date": "2006-01-02T15:04:05Z07:00",
      "customer_reference": "DHU9868NGY",
      "shipment_reference": "",
      "status": "accepted",
      "delivery_name": "Artia",
      "delivery_mobile": "082101871618",
      "delivery_email": "artia2@gmail.com",
      "delivery_street_address": "Jl. Anggrek No.106 Blok C5",
      "delivery_region": "DKI Jakarta",
      "delivery_city": "Kota Jakarta Barat - Cengkareng",
      "delivery_country": "Indonesia",
      "delivery_post_code": "11720",
      "delivery_method": "JNE REG",
      "payment_method" : "Bank Transfer", 
      "airwaybill_number": "AWB12345678",
      "shipping_total": 15000,
      "line_items": [
      {
        "name" : "Product ABC",
        "sku": "DKL0907",
        "quantity": 2,
        "unit_price": 100000,
        "discount": 10000
      }
      ]
    },
    {
      "order_id": "LEVSORD-003101",
      "order_date": "2019-10-22T10:27:48Z",
      "customer_reference": "ASHD1301FHF7512",
      "shipment_reference": "",
      "status": "pending",
      "delivery_name": "Agus Setiawan",
      "delivery_email": "agusetiawan@gmail.com",
      "delivery_street_address": "Jalan Anggrek No. 15",
      "delivery_region": "DKI Jakarta",
      "delivery_city": "Kota Jakarta Barat",
      "delivery_country": "Indonesia",
      "delivery_post_code": "11540",
      "delivery_method": "JNE REG",
      "delivery_mobile": "085812805429",
      "payment_method": "COD",
      "line_items":[
      {
         "sku": "ADSME-00128",
          "name": "Sepatu Test",
          "quantity": 2,
          "unit_price": 75000,
          "discount": 10000,
          "order_item_id": "12914ADNAL"
      }
      ]
    },
=======
  "order_id": "ORD-123",
  "order_date": "2006-01-02T15:04:05Z07:00",
  "customer_reference": "DHU9868NGY",
  "shipment_reference": "",
  "status": "accepted",
  "delivery_name": "Artia",
  "delivery_mobile": "082101871618",
  "delivery_email": "artia2@gmail.com",
  "delivery_street_address": "Jl. Anggrek No.106 Blok C5",
  "delivery_city": "Kota Jakarta Barat - Cengkareng",
  "delivery_region": "DKI Jakarta",
  "delivery_country": "Indonesia",
  "delivery_post_code": "11720",
  "delivery_method": "JNE REG",
  "airwaybill_number": "AWB12345678",
  "shipping_total": 15000,
  "line_items": [
    {
      "sku": "DKL0907",
      "quantity": 2,
      "raw_price": 100000,
      "discount": 10000
    }
>>>>>>> 13bd2b514ddf525b2b3ee60ab289f4c5f8f270b4
  ]
}
```

> The above request returns JSON structured like this:

```json
{
<<<<<<< HEAD
  "orders/data":
  [
    {
      "id": 123,
      "order_id": "ORD-123",
      "order_date": "2006-01-02T15:04:05Z",
      "customer_reference": "JNH7438B",
      "shipment_reference": "",
      "order_status": "accepted",
      "delivery_name": "Artia",
      "delivery_mobile": "082101871618",
      "delivery_email": "artia2@gmail.com",
      "delivery_street_address": "Jl. Anggrek No.106 Blok C5",
      "delivery_region": "DKI Jakarta",
      "delivery_city": "Kota Jakarta Barat - Cengkareng",
      "delivery_country": "Indonesia",
      "delivery_postcode": "11720",
      "delivery_method": "JNE REG",
      "payment_method" : "Bank Transfer", 
      "airwaybill_number": "AWB12345678",
      "marketplace_code": "levs",
      "store" : "41",
      "currency_code": "IDR",
      "subtotal": 110000,
      "discount_total": 10000,
      "tax_total" : 0,
      "shipping_total": 15000,
      "total": 115000,
      "line_items": [
        {
          "name" : "Product ABC",
          "id": 3,
          "sku": "DKL0907",
          "quantity": 2,
          "unit_price": 100000,
          "discount": 10000,
          "remote_order_item_id" : ""
        }
      ],
      "created_at": "2019-05-27T06:05:11Z",
      "updated_at": "2019-05-27T06:05:11Z"
    },
    {
      "order_id": "LEVSORD-003101",
      "order_date": "2019-10-22T10:27:48Z",
      "customer_reference": "ASHD1301FHF7512",
      "shipment_reference": "",
      "status": "pending",
      "delivery_name": "Agus Setiawan",
      "delivery_email": "agusetiawan@gmail.com",
      "delivery_street_address": "Jalan Anggrek No. 15",
      "delivery_region": "DKI Jakarta",
      "delivery_city": "Kota Jakarta Barat",
      "delivery_country": "Indonesia",
      "delivery_post_code": "11540",
      "delivery_method": "JNE REG",
      "delivery_mobile": "085812805429",
      "payment_method": "COD",
      "line_items":[
        {
          "sku": "ADSME-00128",
          "name": "Sepatu Test",
          "quantity": 2,
          "unit_price": 75000,
          "discount": 10000,
          "remote_order_item_id" : ""
        }
      ],
      "created_at": "2019-05-27T06:05:11Z",
      "updated_at": "2019-05-27T06:05:11Z"
    }
  ],    
  "message" : "Order created successfully",
  "reference" : "8608798c-3ca1-42ce-8b7d-0ab3d65ef312"
=======
  "data": {
    "id": 123,
    "order_id": "ORD-123",
    "order_date": "2006-01-02T15:04:05Z",
    "customer_reference": "JNH7438B",
    "shipment_reference": "",
    "status": "accepted",
    "delivery_name": "Artia",
    "delivery_mobile": "082101871618",
    "delivery_email": "artia2@gmail.com",
    "delivery_street_address": "Jl. Anggrek No.106 Blok C5",
    "delivery_city": "Kota Jakarta Barat - Cengkareng",
    "delivery_region": "DKI Jakarta",
    "delivery_country": "Indonesia",
    "delivery_post_code": "11720",
    "delivery_method": "JNE REG",
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
        "quantity": 2,
        "raw_price": 100000,
        "discount": 10000
      }
    ],
    "created_at": "2019-05-27T06:05:11Z",
    "updated_at": "2019-05-27T06:05:11Z"
  },
  "message": "",
  "reference": ""
>>>>>>> 13bd2b514ddf525b2b3ee60ab289f4c5f8f270b4
}
```

## Update Order

### HTTP Request

`PATCH /v1/partner/order/status`

### Header Parameters

| Name       | Required | Type   | Description                                                                                                       |
| ---------- | -------- | ------ | ----------------------------------------------------------------------------------------------------------------- |
<<<<<<< HEAD
| partner-id | Yes      | String | Partner ID value (given from SIRCLO) used for partner identification                                              |
=======
| partner_id | Yes      | String | Partner ID value (given from SIRCLO) used for partner identification                                              |
>>>>>>> 13bd2b514ddf525b2b3ee60ab289f4c5f8f270b4
| secret     | Yes      | String | HMAC (Hash Based Message Authentication Code), refer to section: <a href="#composing-secret">Composing Secret</a> |

### Request Body Parameters

Request body must be a JSON document with the following properties

| Name                       | Required | Type      | Description                                                                        |
| -------------------------- | -------- | --------- | ---------------------------------------------------------------------------------- |
| accepted                   | No       | array     | Array of order that want to be accepted                                            |
| accepted - id              | Yes      | int       | SIRCLO Platform order id                                                           |
| accepted - updated_at      | Yes      | timestamp | The last updated timestamp for this order and must be in RFC3339 format timestamp  |
| packed                     | No       | array     | Array of order that want to be packed                                              |
| packed - id                | Yes      | int       | SIRCLO Platform order id                                                           |
| packed - airwaybill_number | Yes      | string    | The airwaybill number for this order                                               |
| packed - updated_at        | Yes      | timestamp | The last updated timestamp for this order and must be in RFC3339 format timestamp  |
| completed                  | No       | array     | Array of order that want to be completed                                           |
| completed - id             | Yes      | int       | SIRCLO Platform order id                                                           |
| completed - received_by    | No       | string    | Name of the receiver                                                               |
| completed - updated_at     | Yes      | timestamp | The last updated timestamp for this order and must be in RFC3339 format timestamp  |
| cancelled                  | No       | array     | Array of order that want to be cancelled                                           |
| cancelled - id             | Yes      | int       | SIRCLO Platform order id                                                           |
| cancelled - cancel_reason  | No       | string    | Reason why the order is cancelled                                                  |
| cancelled - updated_at     | Yes      | timestamp | The last updated timestamp for this order and must be in RFCC3339 format timestamp |

> Request body example:

```json
{
  "accepted": [
    {
      "id": 123,
      "updated_at": "2019-05-27T06:05:11Z"
    }
  ],
  "packed": [
    {
      "id": 456,
      "airwaybill_number": "awb002",
      "updated_at": "2019-05-27T06:05:11Z"
    }
  ],
  "completed": [
    {
      "id": 789,
      "received_by": "Yosua",
      "updated_at": "2019-05-27T06:05:11Z"
    }
  ],
  "cancelled": [
    {
      "id": 135,
      "cancel_reason": "",
      "updated_at": "2019-05-27T06:05:11Z"
    }
  ]
}
```

> The above request returns JSON structured like this:

```json
{
  "data": {
    "succeed": [
      {
        "id": 123,
        "status": "accepted",
        "updated_at": "2019-05-27T06:06:11Z"
      }
    ],
    "failed": [
      {
        "id": 456,
        "status": "pending",
        "message": "Parameter yang diberikan salah",
        "updated_at": "2019-05-27T06:06:11Z"
      }
    ]
  },
<<<<<<< HEAD
  "message": "1 out of 2 order(s) updated successfully",
  "reference": "15ca05af-8765-4367-994a-333ed985406a"
=======
  "message": "",
  "reference": ""
>>>>>>> 13bd2b514ddf525b2b3ee60ab289f4c5f8f270b4
}
```
