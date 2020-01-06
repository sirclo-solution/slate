# Orders

## Get Order

### HTTP Request

`GET /v1/partner/order`

### Header Parameters

| Name       | Required | Type   | Description                                                                                                       |
| ---------- | -------- | ------ | ----------------------------------------------------------------------------------------------------------------- |
| partner-id | Yes      | String | Partner ID value (given from SIRCLO) used for partner identification                                              |
| secret     | Yes      | String | HMAC (Hash Based Message Authentication Code), refer to section: <a href="#composing-secret">Composing Secret</a> |

### Query String Parameters

| Parameter | Required | Type      | Description                                                                                            |
| --------- | -------- | --------- | ------------------------------------------------------------------------------------------------------ |
| since     | Yes      | Timestamp | Start range of order date of the requested orders (must be in RFC3339 format)                          |
| until     | Yes      | Timestamp | End range of order date of the requested orders (must be in RFC3339 format)                            |
| limit     | No       | Integer   | Number of orders that want to be returned (by default the number is 100)                               |
| offset    | No       | Integer   | To be used for pagination (use value 10 if you want to skip 10 first datas, by default the value is 0) |
| withDO    | Yes      | Boolean   | Flag value for determining if the returned sales order data include associated delivery orders or not  |

> Request example
> `GET /v1/partner/order?since=2018-10-13T13:34:52Z&until=2018-10-16T19:22:39Z&limit=10&offset=0withDO=true`

> The above request returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 1,
      "order_id": "ABC123",
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
      "payment_method": "Bank Transfer",
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
          "order_item_id": "29673073",
          "sku": "DKL0907",
          "name": "Product ABC",
          "quantity": 2,
          "unit_price": 100000,
          "discount": 10000,
          "created_at": "2019-07-31T07:39:29.646799Z",
          "updated_at": "2019-07-31T07:39:29.646799Z"
        }
      ],
      "delivery_orders": [
        {
          "id": 12,
          "order_id": 1,
          "delivery_number": "John Doe",
          "airwaybill_number": "AWB12345678",
          "do_status": "pending",
          "delivery_lines": [
            {
              "id": 21,
              "name": "ABC partial order delivery",
              "sku": "ABC123",
              "product_name": "Product ABC",
              "order_quantity": 1,
              "location": "Stock/Commerce",
              "created_at": "2006-01-02T15:04:05Z",
              "updated_at": "2006-01-02T15:04:05Z"
            }
          ],
          "sent_at": "2006-01-02T15:04:05Z",
          "created_at": "2006-01-02T15:04:05Z",
          "updated_at": "2006-01-02T15:04:05Z"
        }
      ],
      "created_at": "2019-07-31T07:39:29.646799Z",
      "updated_at": "2019-07-31T07:39:29.646799Z"
    }
  ],
  "total_record": 1,
  "offset": 0,
  "limit": 10,
  "message": "",
  "reference": "c5170ab9-7afb-4b71-a080-3d0c06e79fa7"
}
```

## Create Order

### HTTP Request

`POST /v1/partner/order`

### Header Parameters

| Name       | Required | Type   | Description                                                                                                       |
| ---------- | -------- | ------ | ----------------------------------------------------------------------------------------------------------------- |
| partner-id | Yes      | String | Partner ID value (given from SIRCLO) used for partner identification                                              |
| secret     | Yes      | String | HMAC (Hash Based Message Authentication Code), refer to section: <a href="#composing-secret">Composing Secret</a> |

### Request Body Parameters

Request body must be a JSON document with the following properties

| Name                       | Required | Type      | Description                                                                                                    |
| -------------------------- | -------- | --------- | -------------------------------------------------------------------------------------------------------------- |
| order_id                   | Yes      | String    | ID of the order in partner's application                                                                       |
| order_date                 | Yes      | Timestamp | The date of order ( must be in RFC3339 format Timestamp )                                                      |
| customer_reference         | Yes      | String    | Customer reference value                                                                                       |
| shipment_reference         | No       | String    | Shipment reference value                                                                                       |
| status                     | No       | String    | Status of the order (by default pending if empty. The acceptable status values are:                            |
| 1. Pending                 |          |           | Order is received from buyer but not yet accepted/acknowledged by seller.                                      |
| 2. Accepted                |          |           | Order is already accepted by seller. Waiting for buyer payment or seller to send ordered items.                |
| 3. Packed                  |          |           | Order is already sent by seller. Order should have airway bill no from 3PL/shipping courier/logistics company. |
| 4. Completed               |          |           | Ordered items is already received by buyer.                                                                    |
| 5. Cancelled               |          |           | Order has been canceled by buyer or seller                                                                     |
| delivery_name              | No       | String    | Name of the buyer/delivery recipient in this order                                                             |
| delivery_mobile            | No       | String    | Mobile number of the delivery recipient                                                                        |
| delivery_email             | No       | String    | Email address of the buyer/delivery recipient in this order                                                    |
| delivery_street_address    | No       | String    | Street address for order delivery                                                                              |
| delivery_city              | No       | String    | City of the delivery recipient                                                                                 |
| delivery_region            | No       | String    | Region (province/district) of the delivery recipient                                                           |
| delivery_country           | No       | String    | Country address of the buyer                                                                                   |
| delivery_post_code         | No       | String    | Postal code of the delivery recipient                                                                          |
| delivery_method            | No       | String    | Logistics service information (name of the logistics company/service used for order delivery)                  |
| payment_method             | Yes      | String    | Name of payment method                                                                                         |
| airwaybill_number          | No       | String    | Airwaybill number from 3PL 3PL (Logistics/Shipping company)                                                    |
| discount_total             | No       | Double    | The total discount value for this order                                                                        |
| shipping_total             | No       | Double    | The total shipping cost value for this order                                                                   |
| line_items                 | Yes      | Array     |                                                                                                                |
| line_items - order_item_id | No       | String    | ID of the product in line item                                                                                 |
| line_items - sku           | Yes      | String    | SKU of the purchased line item                                                                                 |
| line_items - name          | Yes      | String    | Name of the line item                                                                                          |
| line_items - quantity      | Yes      | Integer   | Quantity of the line item                                                                                      |
| line_items - unit_price    | Yes      | Double    | Unit price of the line item (after discount)                                                                   |
| line_items - discount      | No       | Double    | Discount value applied on the line item                                                                        |

> Request body example:

```json
{
  "orders": [
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
      "delivery_city": "Kota Jakarta Barat - Cengkareng",
      "delivery_region": "DKI Jakarta",
      "delivery_country": "Indonesia",
      "delivery_post_code": "11720",
      "delivery_method": "JNE REG",
      "payment_method": "Bank Transfer",
      "airwaybill_number": "AWB12345678",
      "shipping_total": 15000,
      "line_items": [
        {
          "order_item_id": "",
          "sku": "DKL0907",
          "name": "Product ABC",
          "quantity": 2,
          "unit_price": 100000,
          "discount": 10000,
          "created_at": "2019-07-31T07:39:29.646799Z",
          "updated_at": "2019-07-31T07:39:29.646799Z"
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
      "delivery_mobile": "085812805429",
      "delivery_email": "agusetiawan@gmail.com",
      "delivery_street_address": "Jalan Anggrek No. 15",
      "delivery_city": "Kota Jakarta Barat",
      "delivery_region": "DKI Jakarta",
      "delivery_country": "Indonesia",
      "delivery_post_code": "11540",
      "delivery_method": "JNE REG",
      "payment_method": "COD",
      "airwaybill_number": "AWB12345679",
      "line_items": [
        {
          "order_item_id": "",
          "sku": "ADSME-00128",
          "name": "Sepatu Test",
          "quantity": 2,
          "unit_price": 75000,
          "discount": 10000
        }
      ]
    }
  ]
}
```

> The above request returns JSON structured like this:

```json
{
  "data": [
    {
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
      "payment_method": "Bank Transfer",
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
          "order_item_id": "",
          "sku": "DKL0907",
          "name": "Product ABC",
          "quantity": 2,
          "unit_price": 100000,
          "discount": 10000,
          "created_at": "",
          "updated_at": ""
        }
      ],
      "created_at": "2019-05-27T06:05:11Z",
      "updated_at": "2019-05-27T06:05:11Z"
    },
    {
      "id": 124,
      "order_id": "LEVSORD-003101",
      "order_date": "2019-10-22T10:27:48Z",
      "customer_reference": "ASHD1301FHF7512",
      "shipment_reference": "",
      "status": "pending",
      "delivery_name": "Agus Setiawan",
      "delivery_mobile": "085812805429",
      "delivery_email": "agusetiawan@gmail.com",
      "delivery_street_address": "Jalan Anggrek No. 15",
      "delivery_city": "Kota Jakarta Barat",
      "delivery_region": "DKI Jakarta",
      "delivery_country": "Indonesia",
      "delivery_post_code": "11540",
      "delivery_method": "JNE REG",
      "payment_method": "COD",
      "airwaybill_number": "AWB12345679",
      "currency_code": "IDR",
      "subtotal": 110000,
      "discount_total": 10000,
      "shipping_total": 15000,
      "tax_total": 0,
      "total": 115000,
      "line_items": [
        {
          "id": 4,
          "order_item_id": "",
          "sku": "ADSME-00128",
          "name": "Sepatu Test",
          "quantity": 2,
          "unit_price": 75000,
          "discount": 10000,
          "created_at": "",
          "updated_at": ""
        }
      ],
      "created_at": "2019-05-27T06:05:11Z",
      "updated_at": "2019-05-27T06:05:11Z"
    }
  ],
  "message": "Order created successfully",
  "reference": "8608798c-3ca1-42ce-8b7d-0ab3d65ef312"
}
```

## Update Order

### HTTP Request

`PATCH /v1/partner/order/status`

### Header Parameters

| Name       | Required | Type   | Description                                                                                                       |
| ---------- | -------- | ------ | ----------------------------------------------------------------------------------------------------------------- |
| partner-id | Yes      | String | Partner ID value (given from SIRCLO) used for partner identification                                              |
| secret     | Yes      | String | HMAC (Hash Based Message Authentication Code), refer to section: <a href="#composing-secret">Composing Secret</a> |

### Request Body Parameters

Request body must be a JSON document with the following properties

| Name                       | Required | Type      | Description                                                                        |
| -------------------------- | -------- | --------- | ---------------------------------------------------------------------------------- |
| accepted                   | No       | Array     | Array of order that want to be accepted                                            |
| accepted - id              | Yes      | Integer   | SIRCLO Platform order id                                                           |
| accepted - updated_at      | Yes      | Timestamp | The last updated Timestamp for this order and must be in RFC3339 format Timestamp  |
| packed                     | No       | Array     | Array of order that want to be packed                                              |
| packed - id                | Yes      | Integer   | SIRCLO Platform order id                                                           |
| packed - airwaybill_number | Yes      | String    | The airwaybill number for this order                                               |
| packed - updated_at        | Yes      | Timestamp | The last updated Timestamp for this order and must be in RFC3339 format Timestamp  |
| completed                  | No       | Array     | Array of order that want to be completed                                           |
| completed - id             | Yes      | Integer   | SIRCLO Platform order id                                                           |
| completed - received_by    | No       | String    | Name of the receiver                                                               |
| completed - updated_at     | Yes      | Timestamp | The last updated Timestamp for this order and must be in RFC3339 format Timestamp  |
| cancelled                  | No       | Array     | Array of order that want to be cancelled                                           |
| cancelled - id             | Yes      | Integer   | SIRCLO Platform order id                                                           |
| cancelled - cancel_reason  | No       | String    | Reason why the order is cancelled                                                  |
| cancelled - updated_at     | Yes      | Timestamp | The last updated Timestamp for this order and must be in RFCC3339 format Timestamp |

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
  "message": "1 out of 2 order(s) updated successfully",
  "reference": "15ca05af-8765-4367-994a-333ed985406a"
}
```
