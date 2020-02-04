# Composing Secret

For every request sent, partner must include **_partner-id_** and **_secret_** in the HTTP request headers.

- **_partner-id_** value to use is given by SIRCLO.
For every request sent, partner must include **_partner-id_** and **_secret_** in the HTTP request headers.

- **_partner-id_** value to use is given by SIRCLO.
- **_secret_** value to send is HMAC (Hash Based Message Authentication Code) using SHA-256 algorithm.
- To compose the HMAC value, partner must use the HTTP Request URI joined with the request Body as the message to hash using a certain **_partner_secret_** value (given by SIRCLO)
- The resulting hash after HMAC calculation is then base64 encoded and placed in HTTP header **_secret_** in the request.

## Example

Given **_partner_id_** and **_partner_secret_**:

| partner_id | partner_secret                              |
| ---------- | ------------------------------------------- |
| B98KL87    | 1IieSn9qXCYu3FeEG1eH05QxTMldKEiNIkLSN/5xtgc=|
|            |                                             |

> With request URI **_POST /v1/partner/order_** and the HTTP Request Body Parameter example like on the right side

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
          "unit_price": 40000,
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
          "unit_price": 85000,
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
          "unit_price": 50000,
          "order_item_id": "78205HJSLE"
        }
      ]
    }
  ]
}
```

> The message used for HMAC calculation is taken from the HTTP request URI joined with the HTTP request body:

```text
message_to_be_hashed = v1/partner/order{"orders":[{"order_id":"ORD-123","order_date":"2020-01-31T10:47:48Z","customer_reference":"CAHDI831013N3H3J","shipment_reference":"CAHDI831013N3H3J","status":"pending","delivery_name":"John Smith","delivery_email":"johnsmith@outlook.com","delivery_street_address":"Jalan Anggrek No. 35","delivery_region":"DKI Jakarta","delivery_city":"Jakarta Barat","delivery_suburb":"Kembangan","delivery_country":"Indonesia","delivery_post_code":"11650","delivery_method":"JNE REG","delivery_mobile":"082130192810","payment_method":"COD","discount_total":15000,"shipping_total":8000,"line_items":[{"sku":"TOP0001","name":"Barang Branded","quantity":2,"unit_price":40000,"discount":5000,"order_item_id":"73910HDLJR"}]},{"order_id":"ORD-124","order_date":"2020-01-31T04:27:11Z","customer_reference":"JSAL1349SSM2JS9","shipment_reference":"JSAL1349SSM2JS9","status":"pending","delivery_name":"John Due","delivery_email":"johndue@gmail.com","delivery_street_address":"Jalan Gajah No. 35","delivery_region":"DKI Jakarta","delivery_city":"Jakarta Selatan","delivery_suburb":"Setia Budi","delivery_country":"Indonesia","delivery_post_code":"12940","delivery_method":"JNE REG","delivery_mobile":"085310355429","payment_method":"Credit Card","shipping_total":18000,"line_items":[{"sku":"LVB9C50","name":"Sepatu","quantity":2,"unit_price":85000,"discount":12000,"order_item_id":"71034JFERM"}]},{"order_id":"ORD-125","order_date":"2020-01-31T07:11:48Z","customer_reference":"NCEDI83820143NSJ","shipment_reference":"NCEDI83820143NSJ","status":"pending","delivery_name":"John Wick","delivery_email":"johnwick@gmail.com","delivery_street_address":"Jalan Nelimurni No. 12","delivery_region":"DKI Jakarta","delivery_city":"Jakarta Pusat","delivery_suburb":"Menteng","delivery_country":"Indonesia","delivery_post_code":"10250","delivery_method":"JNE REG","delivery_mobile":"085812120429","payment_method":"COD","discount_total":15000,"shipping_total":8000,"line_items":[{"sku":"TOP0001","name":"Barang Branded","quantity":1,"unit_price":50000,"order_item_id":"78205HJSLE"}]}]}
```

> The **_message_to_be_hashed_** is then used with the **_partner_secret_** value when calculating the HMAC

```text
hmac = hmac_sha256(message_to_be_hashed, partner_secret)
hmac = hmac_sha256(message_to_be_hashed, 1IieSn9qXCYu3FeEG1eH05QxTMldKEiNIkLSN/5xtgc=)
```

> The resulting hmac is in binary format, it is then base64 encoded

```text
result = base64_encode(hmac) = CxWnlMigAoSQgKcFIxVme0bXYk8Ftk99daJXssYCXC8=
```

> Partner must include this HMAC value in HTTP header: "**_secret_**" along with HTTP header "**_partner_id_**". Example request that the partner needs to send becomes as follows:

```cURL
POST /v1/partner/order HTTP/1.1
Host: api.connexi.id
Content-Type: application/json
partner-id: B98KL87
secret: CxWnlMigAoSQgKcFIxVme0bXYk8Ftk99daJXssYCXC8=


{"orders":[{"order_id":"ORD-123","order_date":"2020-01-31T10:47:48Z","customer_reference":"CAHDI831013N3H3J","shipment_reference":"CAHDI831013N3H3J","status":"pending","delivery_name":"John Smith","delivery_email":"johnsmith@outlook.com","delivery_street_address":"Jalan Anggrek No. 35","delivery_region":"DKI Jakarta","delivery_city":"Jakarta Barat","delivery_suburb":"Kembangan","delivery_country":"Indonesia","delivery_post_code":"11650","delivery_method":"JNE REG","delivery_mobile":"082130192810","payment_method":"COD","discount_total":15000,"shipping_total":8000,"line_items":[{"sku":"TOP0001","name":"Barang Branded","quantity":2,"unit_price":40000,"discount":5000,"order_item_id":"73910HDLJR"}]},{"order_id":"ORD-124","order_date":"2020-01-31T04:27:11Z","customer_reference":"JSAL1349SSM2JS9","shipment_reference":"JSAL1349SSM2JS9","status":"pending","delivery_name":"John Due","delivery_email":"johndue@gmail.com","delivery_street_address":"Jalan Gajah No. 35","delivery_region":"DKI Jakarta","delivery_city":"Jakarta Selatan","delivery_suburb":"Setia Budi","delivery_country":"Indonesia","delivery_post_code":"12940","delivery_method":"JNE REG","delivery_mobile":"085310355429","payment_method":"Credit Card","shipping_total":18000,"line_items":[{"sku":"LVB9C50","name":"Sepatu","quantity":2,"unit_price":85000,"discount":12000,"order_item_id":"71034JFERM"}]},{"order_id":"ORD-125","order_date":"2020-01-31T07:11:48Z","customer_reference":"NCEDI83820143NSJ","shipment_reference":"NCEDI83820143NSJ","status":"pending","delivery_name":"John Wick","delivery_email":"johnwick@gmail.com","delivery_street_address":"Jalan Nelimurni No. 12","delivery_region":"DKI Jakarta","delivery_city":"Jakarta Pusat","delivery_suburb":"Menteng","delivery_country":"Indonesia","delivery_post_code":"10250","delivery_method":"JNE REG","delivery_mobile":"085812120429","payment_method":"COD","discount_total":15000,"shipping_total":8000,"line_items":[{"sku":"TOP0001","name":"Barang Branded","quantity":1,"unit_price":50000,"order_item_id":"78205HJSLE"}]}]}
```

Code examples of on how to calculate HMAC in various programming languages: <https://github.com/danharper/hmac-examples>

## Another example

> The partner wants to send a HTTP request like the following:

```cURL
GET /v1/partner/order?since=2018-10-13T13:34:52Z&until=2018-10-16T19:22:39Z&limit=100&offset=0 HTTP/1.1
Host: api.connexi.id
```

> The request URI of the HTTP request is "_/v1/partner/order?since=2018-10-13T13:34:52Z&until=2018-10-16T19:22:39Z&limit=100&offset=0_"

```text
message_to_be_hashed = /v1/partner/order?since=2018-10-13T13:34:52Z&until=2018-10-16T19:22:39Z&limit=100&offset=0

hmac = hmac_sha256(message_to_be_hashed, 1IieSn9qXCYu3FeEG1eH05QxTMldKEiNIkLSN/5xtgc=)

secret = base64_encode(hmac) = XoPRRDtfNWaGm4nbw7A0LY/c2U0+jg3F3Ay2d3VR3bM=
```

> The HTTP request to send then becomes as follows:

```cURL
GET /v1/partner/order?since=2018-10-13T13:34:52Z&until=2018-10-16T19:22:39Z&limit=100&offset=0
Host : api.connexi.id
partner-id: B98KL87
secret: XoPRRDtfNWaGm4nbw7A0LY/c2U0+jg3F3Ay2d3VR3bM=
```
