# Order API

## Get Order

**Description:** Call this endpoint to get orders data that you have previously sent using create order endpoint.

### HTTP Request

`GET /order?since=&until=&limit=&offset=`

### Header Parameters

| Name       | Required | Type   | Description                                                                                                                                                       |
| ---------- | -------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| partner_id | Yes      | String | Partner id value (given from SIRCLO) used for partner identification by SIRCLO                                                                                    |
| Secret     | Yes      | String | HMAC (Hash Based Message Authentication Code) composed by hashing the HTTP request body using, refer to section: <a href="#composing-secret">Composing Secret</a> |

### Query String Parameters

| Parameter | Required | Type      | Description                                                                             |
| --------- | -------- | --------- | --------------------------------------------------------------------------------------- |
| since     | Yes      | Timestamp | Start range of order date of the requested orders (must be in RFC3339 format)           |
| until     | Yes      | Timestamp | End range of order date of the requested orders (must be in RFC3339 format)             |
| limit     | Yes      | Integer   | The maximum number of orders that can be returned, this supported maximum number is 100 |
| offset    | Yes      | Integer   | The number of records to be returned in 1 page                                          |

> Request example
> `GET /v1/partner/order?since=2018-10-13T13:34:52Z&until=2018-10-16T19:22:39Z&limit=100&offset=0`

> The above request returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 1,
      "order_id": "ABC123",
      "order_date": "2006-01-02T15:04:05Z07:00",
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
      "createdAt": "2019-05-27 06:05:11.979185",
      "updatedAt": "2019-05-27 06:05:11.979185"
    }
  ],
  "total_record": 1,
  "message": "",
  "reference": ""
}
```

## Create Order

**Description:** Use this endpoint to create new order.

### HTTP Request

`POST /order`

**Header Parameters**

| Name       | Required | Type   | Description                                                                                                                                                       |
| ---------- | -------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| partner_id | Yes      | String | Partner id value (given from SIRCLO) used for partner identification by SIRCLO                                                                                    |
| Secret     | Yes      | String | HMAC (Hash Based Message Authentication Code) composed by hashing the HTTP request body using, refer to section: <a href="#composing-secret">Composing Secret</a> |

> Request body example :

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
      "name": "Product ABC",
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
    "order_date": "2006-01-02T15:04:05Z07:00",
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
        "name": "Product ABC",
        "quantity": 2,
        "raw_price": 100000,
        "discount": 10000
      }
    ],
    "createdAt": "2019-05-27 06:05:11.979185",
    "updatedAt": "2019-05-27 06:05:11.979185"
  },
  "message": "",
  "reference": ""
}
```

Request body must be a JSON document with the following properties

| Name                    | Required | Type      | Description                                                                                                    |
| ----------------------- | -------- | --------- | -------------------------------------------------------------------------------------------------------------- |
| order_id                | Yes      | string    | Id of the order in partner's application                                                                       |
| order_date              | Yes      | Timestamp | the date of order ( must be in RFC3339 format timestamp )                                                      |
| customer_reference      | No       | string    | customer reference value                                                                                       |
| shipment_reference      | Yes      | string    | shipment reference value                                                                                       |
| status                  | No       | string    | Status of the order (by default pending if empty. The acceptable status values are:                            |
| 1. Pending              |          |           | Order is received from buyer but not yet accepted/acknowledged by seller.                                      |
| 2. Accepted             |          |           | Order is already accepted by seller. Waiting for buyer payment or seller to send ordered items.                |
| 3. Packed               |          |           | Order is already sent by seller. Order should have airway bill no from 3PL/shipping courier/logistics company. |
| 4. Completed            |          |           | Ordered items is already received by buyer.                                                                    |
| 5. Cancelled            |          |           | Order has been canceled by buyer or seller                                                                     |
| delivery_name           | No       | string    | name of the buyer/delivery recipient in this order                                                             |
| delivery_email          | No       | string    | email address of the buyer/delivery recipient in this order                                                    |
| delivery_street_address | No       | string    | street address for order delivery                                                                              |
| delivery_region         | No       | string    | region (province/district) of the delivery recipient                                                           |
| delivery_city           | No       | string    | city of the delivery recipient                                                                                 |
| delivery_country        | No       | string    | country address of the buyer                                                                                   |
| delivery_post_code      | No       | string    | post code of the delivery recipient                                                                            |
| delivery_method         | No       | string    | logistics service information (name of the logistics company/service used for order delivery)                  |
| delivery_mobile         | No       | string    | mobile number of the delivery recipient                                                                        |
| airwaybill_number       | No       | string    | airwaybill number from 3PL 3PL (Logistics/Shipping company)                                                    |
| shipping_total          | No       | double    | This total shipping cost value for this order                                                                  |
| line_items              | Yes      | array     |                                                                                                                |
| line_items - id         | Yes      | int       | id of the product                                                                                              |
| line_items - sku        | Yes      | string    | sku of the purchased line item                                                                                 |
| line_items - name       | Yes      | string    | name of the purchased line item                                                                                |
| line_items - quantity   | Yes      | integer   | quantity of the line item                                                                                      |
| line_items - unit_price | Yes      | double    | unit price of the line item (after discount)                                                                   |
| line_items - discount   | Yes      | double    | discount value applied on the line item                                                                        |

## Update Order

**Description:** This endpoint used to update order from partner system.

### HTTP Request

`PATCH /order`

### Header Parameters

| Name       | Required | Type   | Description                                                                                                                                                       |
| ---------- | -------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| partner_id | Yes      | String | Partner id value (given from SIRCLO) used for partner identification by SIRCLO                                                                                    |
| Secret     | Yes      | String | HMAC (Hash Based Message Authentication Code) composed by hashing the HTTP request body using, refer to section: <a href="#composing-secret">Composing Secret</a> |

> Request body example :

```json
{
  "accepted": [
    {
      "id": 123,
      "updated_at": "2019-05-27 06:05:11.979185"
    }
  ],
  "packed": [
    {
      "id": 456,
      "airwaybill_number": "awb002",
      "updated_at": "2019-05-27 06:05:11.979185"
    }
  ],
  "completed": [
    {
      "id": 789,
      "received_by": "Yosua",
      "updated_at": "2019-05-27 06:05:11.979185"
    }
  ],
  "cancelled": [
    {
      "id": 135,
      "cancel_reason": "",
      "updated_at": "2019-05-27 06:05:11.979185"
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
        "updated_at": "2019-05-27 06:06:11.979185"
      }
    ],
    "failed": [
      {
        "id": 456,
        "order_status": "pending",
        "message": "Parameter yang diberikan salah",
        "updated_at": "2019-05-27 06:06:11.979185"
      }
    ]
  },
  "message": "",
  "reference": ""
}
```

| Name                       | Required | Type      | Description                                                                        |
| -------------------------- | -------- | --------- | ---------------------------------------------------------------------------------- |
| accepted                   | No       | array     | array of order that want to be accepted                                            |
| accepted - id              | Yes      | int       | SIRCLO Platform order id                                                           |
| accepted - updated_at      | Yes      | timestamp | the last updated timestamp for this order and must be in RFC3339 format timestamp  |
| packed                     | No       | array     | array of order that want to be packed                                              |
| packed - id                | Yes      | int       | SIRCLO Platform order id                                                           |
| packed - airwaybill_number | Yes      | string    | the airwaybill number for this order                                               |
| packed - updated_at        | Yes      | timestamp | the last updated timestamp for this order and must be in RFC3339 format timestamp  |
| completed                  | No       | array     | array of order that want to be completed                                           |
| completed - id             | Yes      | int       | SIRCLO Platform order id                                                           |
| completed - received_by    | No       | string    | name of the receiver                                                               |
| completed - updated_at     | Yes      | timestamp | the last updated timestamp for this order and must be in RFC3339 format timestamp  |
| cancelled                  | No       | array     | array of order that want to be cancelled                                           |
| cancelled - id             | Yes      | int       | SIRCLO Platform order id                                                           |
| cancelled - cancel_reason  | No       | string    | reason why the order is cancelled                                                  |
| cancelled - updated_at     | Yes      | timestamp | the last updated timestamp for this order and must be in RFCC3339 format timestamp |  |
