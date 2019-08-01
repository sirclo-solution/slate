# Orders

## Get Order

### HTTP Request

`GET /v1/partner/order?since=&until=&limit=&offset=`

### Header Parameters

| Name       | Required | Type   | Description                                                                                                       |
| ---------- | -------- | ------ | ----------------------------------------------------------------------------------------------------------------- |
| partner_id | Yes      | String | Partner ID value (given from SIRCLO) used for partner identification                                              |
| secret     | Yes      | String | HMAC (Hash Based Message Authentication Code), refer to section: <a href="#composing-secret">Composing Secret</a> |

### Query String Parameters

| Parameter | Required | Type      | Description                                                                                            |
| --------- | -------- | --------- | ------------------------------------------------------------------------------------------------------ |
| since     | Yes      | Timestamp | Start range of order date of the requested orders (must be in RFC3339 format)                          |
| until     | Yes      | Timestamp | End range of order date of the requested orders (must be in RFC3339 format)                            |
| limit     | No       | Integer   | Number of orders that want to be returned (by default the number is 100)                               |
| offset    | No       | Integer   | To be used for pagination (use value 10 if you want to skip 10 first datas, by default the value is 0) |

> Request example
> `GET /v1/partner/order?since=2018-10-13T13:34:52Z&until=2018-10-16T19:22:39Z&limit=100&offset=0`

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
      "delivery_email": "artia2@gmail.com",
      "delivery_street_address": "Jl. Anggrek No.106 Blok C5",
      "delivery_region": "DKI Jakarta",
      "delivery_city": "Kota Jakarta Barat - Cengkareng",
      "delivery_country": "Indonesia",
      "delivery_post_code": "11720",
      "delivery_method": "JNE REG",
      "delivery_mobile": "082101871618",
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
          "sku": "DKL0907",
          "name": "Product ABC",
          "quantity": 2,
          "raw_price": 100000,
          "discount": 10000
        }
      ],
      "created_at": "2019-05-27T06:05:11Z",
      "updated_at": "2019-05-27T06:05:11Z"
    }
  ],
  "total_record": 1,
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
| partner_id | Yes      | String | Partner ID value (given from SIRCLO) used for partner identification                                              |
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
| delivery_email          | No       | string    | Email address of the buyer/delivery recipient in this order                                                    |
| delivery_street_address | No       | string    | Street address for order delivery                                                                              |
| delivery_region         | No       | string    | Region (province/district) of the delivery recipient                                                           |
| delivery_city           | No       | string    | City of the delivery recipient                                                                                 |
| delivery_country        | No       | string    | Country address of the buyer                                                                                   |
| delivery_post_code      | No       | string    | Postal code of the delivery recipient                                                                          |
| delivery_method         | No       | string    | Logistics service information (name of the logistics company/service used for order delivery)                  |
| delivery_mobile         | No       | string    | Mobile number of the delivery recipient                                                                        |
| airwaybill_number       | No       | string    | Airwaybill number from 3PL 3PL (Logistics/Shipping company)                                                    |
| shipping_total          | No       | double    | The total shipping cost value for this order                                                                   |
| line_items              | Yes      | array     |                                                                                                                |
| line_items - sku        | Yes      | string    | SKU of the purchased line item                                                                                 |
| line_items - quantity   | Yes      | integer   | Quantity of the line item                                                                                      |
| line_items - unit_price | Yes      | double    | Unit price of the line item (after discount)                                                                   |
| line_items - discount   | Yes      | double    | Discount value applied on the line item                                                                        |

> Request body example:

```json
{
  "order_id": "ORD-123",
  "order_date": "2006-01-02T15:04:05Z07:00",
  "customer_reference": "DHU9868NGY",
  "shipment_reference": "",
  "status": "accepted",
  "delivery_name": "Artia",
  "delivery_email": "artia2@gmail.com",
  "delivery_street_address": "Jl. Anggrek No.106 Blok C5",
  "delivery_region": "DKI Jakarta",
  "delivery_city": "Kota Jakarta Barat - Cengkareng",
  "delivery_country": "Indonesia",
  "delivery_post_code": "11720",
  "delivery_method": "JNE REG",
  "delivery_mobile": "082101871618",
  "airwaybill_number": "AWB12345678",
  "shipping_total": 15000,
  "line_items": [
    {
      "sku": "DKL0907",
      "quantity": 2,
      "raw_price": 100000,
      "discount": 10000
    }
  ]
}
```

> The above request returns JSON structured like this:

```json
{
  "data": {
    "id": 123,
    "order_id": "ORD-123",
    "order_date": "2006-01-02T15:04:05Z",
    "customer_reference": "JNH7438B",
    "shipment_reference": "",
    "status": "accepted",
    "delivery_name": "Artia",
    "delivery_email": "artia2@gmail.com",
    "delivery_street_address": "Jl. Anggrek No.106 Blok C5",
    "delivery_region": "DKI Jakarta",
    "delivery_city": "Kota Jakarta Barat - Cengkareng",
    "delivery_country": "Indonesia",
    "delivery_post_code": "11720",
    "delivery_method": "JNE REG",
    "delivery_mobile": "082101871618",
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
}
```

## Update Order

### HTTP Request

`PATCH /v1/partner/order`

### Header Parameters

| Name       | Required | Type   | Description                                                                                                       |
| ---------- | -------- | ------ | ----------------------------------------------------------------------------------------------------------------- |
| partner_id | Yes      | String | Partner ID value (given from SIRCLO) used for partner identification                                              |
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
        "order_status": "accepted",
        "updated_at": "2019-05-27T06:06:11Z"
      }
    ],
    "failed": [
      {
        "id": 456,
        "order_status": "pending",
        "message": "Parameter yang diberikan salah",
        "updated_at": "2019-05-27T06:06:11Z"
      }
    ]
  },
  "message": "",
  "reference": ""
}
```
