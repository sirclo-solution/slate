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
      "id": 2886789,
      "order_id": "ORD-123",
      "order_date": "2020-01-31T10:47:48Z",
      "order_number": "",
      "customer_reference": "CAHDI831013N3H3J",
      "shipment_reference": "CAHDI831013N3H3J",
      "status": "pending",
      "delivery_name": "John Smith",
      "delivery_mobile": "082130192810",
      "delivery_email": "john.smith@outlook.com",
      "delivery_street_address": "Jalan Anggrek No. 35",
      "delivery_city": "Jakarta Barat",
      "delivery_region": "DKI Jakarta",
      "delivery_suburb": "Kembangan",
      "delivery_country": "Indonesia",
      "delivery_post_code": "11650",
      "delivery_method": "JNE REG",
      "payment_method": "COD",
      "airwaybill_number": "AWB12345678",
      "currency_code": "",
      "subtotal": 80000,
      "discount_total": 15000,
      "shipping_total": 8000,
      "tax_total": 7272.726,
      "total": 73000,
      "line_items": [
        {
          "id": 11776166,
          "order_item_id": "73910HDLJR",
          "sku": "TOP0001",
          "name": "Barang Branded",
          "quantity": 2,
          "unit_price": 40000,
          "discount": 5000,
          "created_at": "2020-02-04T07:15:48.758558Z",
          "updated_at": "2020-02-04T07:15:48.758558Z"
        }
      ],
      "delivery_orders": [
        {
          "id": 12,
          "order_id": "ORD-123",
          "delivery_number": "John Smith",
          "airwaybill_number": "AWB12345678",
          "do_status": "pending",
          "delivery_lines": [
            {
              "id": 21,
              "name": "ABC partial order delivery",
              "sku": "TOP0001",
              "product_name": "Barang Branded",
              "order_quantity": 2,
              "location": "Stock/Commerce",
              "created_at": "2020-02-04T07:15:48.758558Z",
              "updated_at": "2020-02-04T07:15:48.758558Z"
            }
          ],
          "sent_at": "2020-02-04T07:16:40.758558Z",
          "created_at": "2020-02-04T07:15:50.758558Z",
          "updated_at": "2020-02-04T07:15:50.758558Z"
        }
      ],
      "created_at": "2020-02-04T07:15:46.196556Z",
      "updated_at": "2020-02-04T07:15:46.196556Z"
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
| delivery_street_address    | Yes       | String    | Street address for order delivery                                                                              |
| delivery_city              | Yes       | String    | City of the delivery recipient                                                                                 |
| delivery_region            | Yes       | String    | Region (province/district) of the delivery recipient                                                           |
| delivery_suburb            | Yes      | String    | Sub-district of the buyer                                                                                                            |
| delivery_country           | Yes       | String    | Country address of the buyer                                                                                   |
| delivery_post_code         | Yes       | String    | Postal code of the delivery recipient                                                                          |
| delivery_method            | Yes       | String    | Logistics service information (name of the logistics company/service used for order delivery)                  |
| payment_method             | Yes      | String    | Name of payment method                                                                                         |
| airwaybill_number          | No       | String    | Airwaybill number from 3PL 3PL (Logistics/Shipping company)                                                    |
| discount_total             | No       | Double    | The total discount value for this order                                                                        |
| shipping_total             | No       | Double    | The total shipping cost value for this order                                                                   |
| line_items                 | Yes      | Array     |                                                                                                                |
| line_items - order_item_id | No       | String    | ID of the product in line item                                                                                 |
| line_items - sku           | Yes      | String    | SKU of the purchased line item                                                                                 |
| line_items - name          | Yes      | String    | Name of the line item                                                                                          |
| line_items - quantity      | Yes      | Integer   | Quantity of the line item                                                                                      |
| line_items - raw_price    | Yes      | Double    | Price of the line item (before discount)                                                                   |
| line_items - discount      | No       | Double    | Discount value applied on the line item                                                                        |

> Request body example:

```json
{
  "orders": [
    {
      "order_id": "ORD-123",
      "order_date": "2020-01-31T10:47:48Z",
      "customer_reference": "CAHDI831013N3H3J",
      "shipment_reference": "CAHDI831013N3H3J",
      "status": "pending",
      "delivery_name": "John Smith",
      "delivery_email": "johnsmith@outlook.com",
      "delivery_street_address": "Jalan Anggrek No. 35",
      "delivery_region": "DKI Jakarta",
      "delivery_city": "Jakarta Barat",
      "delivery_suburb": "Kembangan",
      "delivery_country": "Indonesia",
      "delivery_post_code": "11650",
      "delivery_method": "JNE REG",
      "delivery_mobile": "082130192810",
      "payment_method": "COD",
      "discount_total": 15000,
      "shipping_total": 8000,
      "line_items": [
        {
          "sku": "TOP0001",
          "name": "Barang Branded",
          "quantity": 2,
          "raw_price" : 45000,
          "discount": 5000,
          "order_item_id": "73910HDLJR"
        }
      ]
    },
    {
      "order_id": "ORD-124",
      "order_date": "2020-01-31T04:27:11Z",
      "customer_reference": "JSAL1349SSM2JS9",
      "shipment_reference": "JSAL1349SSM2JS9",
      "status": "pending",
      "delivery_name": "John Due",
      "delivery_email": "johndue@gmail.com",
      "delivery_street_address": "Jalan Gajah No. 35",
      "delivery_region": "DKI Jakarta",
      "delivery_city": "Jakarta Selatan",
      "delivery_suburb": "Setia Budi",
      "delivery_country": "Indonesia",
      "delivery_post_code": "12940",
      "delivery_method": "JNE REG",
      "delivery_mobile": "085310355429",
      "payment_method": "Credit Card",
      "shipping_total": 18000,
      "line_items": [
        {
          "sku": "LVB9C50",
          "name": "Sepatu",
          "quantity": 2,
          "raw_price" : 97000,
          "discount": 12000,
          "order_item_id": "71034JFERM"
        }
      ]
    },
    {
      "order_id": "ORD-125",
      "order_date": "2020-01-31T07:11:48Z",
      "customer_reference": "NCEDI83820143NSJ",
      "shipment_reference": "NCEDI83820143NSJ",
      "status": "pending",
      "delivery_name": "John Wick",
      "delivery_email": "johnwick@gmail.com",
      "delivery_street_address": "Jalan Nelimurni No. 12",
      "delivery_region": "DKI Jakarta",
      "delivery_city": "Jakarta Pusat",
      "delivery_suburb": "Menteng",
      "delivery_country": "Indonesia",
      "delivery_post_code": "10250",
      "delivery_method": "JNE REG",
      "delivery_mobile": "085812120429",
      "payment_method": "COD",
      "discount_total": 15000,
      "shipping_total": 8000,
      "line_items": [
        {
          "sku": "TOP0001",
          "name": "Barang Branded",
          "quantity": 1,
          "raw_price": 50000,
          "order_item_id": "78205HJSLE"
        }
      ]
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
                "id": 2886789,
                "order_id": "ORD-123",
                "order_date": "2020-01-31T10:47:48Z",
                "order_number": "",
                "customer_reference": "CAHDI831013N3H3J",
                "shipment_reference": "CAHDI831013N3H3J",
                "status": "pending",
                "delivery_name": "John Smith",
                "delivery_mobile": "082130192810",
                "delivery_email": "john.smith@outlook.com",
                "delivery_street_address": "Jalan Anggrek No. 35",
                "delivery_city": "Jakarta Barat",
                "delivery_region": "DKI Jakarta",
                "delivery_suburb": "Kembangan",
                "delivery_country": "Indonesia",
                "delivery_post_code": "11650",
                "delivery_method": "JNE REG",
                "payment_method": "COD",
                "airwaybill_number": "",
                "currency_code": "",
                "subtotal": 80000,
                "discount_total": 15000,
                "shipping_total": 8000,
                "tax_total": 7272.726,
                "total": 73000,
                "line_items": [
                    {
                        "id": 11776166,
                        "order_item_id": "73910HDLJR",
                        "sku": "TOP0001",
                        "name": "Barang Branded",
                        "quantity": 2,
                        "unit_price": 40000,
                        "discount": 5000,
                        "created_at": "2020-02-04T07:15:48.758558Z",
                        "updated_at": "2020-02-04T07:15:48.758558Z"
                    }
                ],
                "created_at": "2020-02-04T07:15:46.196556Z",
                "updated_at": "2020-02-04T07:15:46.196556Z"
            },
            {
                "id": 2886790,
                "order_id": "ORD-124",
                "order_date": "2020-01-31T04:27:11Z",
                "order_number": "",
                "customer_reference": "JSAL1349SSM2JS9",
                "shipment_reference": "JSAL1349SSM2JS9",
                "status": "pending",
                "delivery_name": "John Due",
                "delivery_mobile": "085310355429",
                "delivery_email": "johndue@gmail.com",
                "delivery_street_address": "Jalan Gajah No. 35",
                "delivery_city": "Jakarta Selatan",
                "delivery_region": "DKI Jakarta",
                "delivery_suburb": "Setia Budi",
                "delivery_country": "Indonesia",
                "delivery_post_code": "12940",
                "delivery_method": "JNE REG",
                "payment_method": "Credit Card",
                "airwaybill_number": "",
                "currency_code": "",
                "subtotal": 170000,
                "discount_total": 12000,
                "shipping_total": 18000,
                "tax_total": 15454.544,
                "total": 176000,
                "line_items": [
                    {
                        "id": 11776167,
                        "order_item_id": "71034JFERM",
                        "sku": "LVB9C50",
                        "name": "Sepatu",
                        "quantity": 2,
                        "unit_price": 85000,
                        "discount": 12000,
                        "created_at": "2020-02-04T07:15:49.149511Z",
                        "updated_at": "2020-02-04T07:15:49.149511Z"
                    }
                ],
                "created_at": "2020-02-04T07:15:49.146403Z",
                "updated_at": "2020-02-04T07:15:49.146403Z"
            }
        ],
        "failed": [
            {
                "order_id": "ORD-125",
                "reason": "existing order with remote order id: ORD-125 already exists"
            }
        ]
    },
    "message": "Requested order count: 3, Created order count: 2, Failed to create order count: 1",
    "reference": "fd8ece53-f778-4c1b-bbda-1b12c612fc3d"
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
