# Composing Secret

For every request sent, partner must include **_partner_id_** and **_secret_** in the HTTP request headers.

- **_partner_id_** value to use is given by Sirclo.
- **_secret_** value to send is HMAC (Hash Based Message Authentication Code) using SHA-256 algorithm.
- To compose the HMAC value, partner must use the HTTP Request URI joined with the request Body as the message to hash using a certain **_partner_secret_** value (given by SIRCLO)
- The resulting hash after HMAC calculation is then base64 encoded and placed in HTTP header **_secret_** in the request.

## Example

Given **_partner_id_** and **_partner_secret_**:

| partner_id | partner_secret                              |
| ---------- | ------------------------------------------- |
| B98KL87    | a6jMwv4mFlj1VOh6jZzlJ2upVTcGfbjTtJpA2Hp5fpM |

With request URI **_POST /v1/partner/order_** and the HTTP Request Body Parameter example like on the right side

```json
{
  "order_id": "ORD-256/20190627/FMCG/OA",
  "order_date": "2019-06-02T16:31:55Z",
  "status": "accepted",
  "customer_reference": "DHU9868NGY",
  "shipment_reference": "",
  "delivery_name": "John Smith",
  "delivery_email": "john.fictional.smith@gmail.com",
  "delivery_street_address": "Jl. Anggrek No.106 Blok C5",
  "delivery_region": "DKI Jakarta",
  "delivery_city": "Kota Jakarta Barat - Cengkareng",
  "delivery_country": "Indonesia",
  "delivery_post_code": "11720",
  "delivery_method": "JNE Reguler",
  "delivery_mobile": "082101871618",
  "airwaybill_number": "AWB12345678",
  "shipping_total": 15000,
  "line_items": [
    {
      "sku": "DKL0907",
      "name": "Organic Instant Noodles Special Chicken Flavor - 150 gr",
      "quantity": 2,
      "raw_price": 10000,
      "discount": 100
    },
    {
      "sku": "CCF0985",
      "name": "Organic Instant Coffee With Brown Sugar - 100 gr",
      "quantity": 5,
      "raw_price": 5000,
      "discount": 0
    }
  ]
}
```

The message used for HMAC calculation is taken from the HTTP request URI joined with the HTTP request body:

```
message_to_be_hashed = /v1/partner/order/create{"order_id":"ORD-256/20190627/FMCG/OA","order_date":"2019-06-02T16:31:55+07:00","status":"accepted","customer_reference":"DHU9868NGY","shipment_reference":"","delivery_name":"John Smith","delivery_email":"john.fictional.smith@gmail.com","delivery_street_address":"Jl. Anggrek No.106 Blok C5","delivery_region":"DKI Jakarta","delivery_city":"Kota Jakarta Barat - Cengkareng","delivery_country":"Indonesia","delivery_post_code":"11720","delivery_method":"JNE Reguler","delivery_mobile":"082101871618","ariwaybill_number":"AWB12345678","shipping_total":15000,"line_items":[{"sku":"DKL0907","name":"Organic Instant Noodles Special Chicken Flavor - 150 gr","quantity":2,"raw_price":10000,"discount":100},{"sku":"CCF0985","name":"Organic Instant Coffee With Brown Sugar - 100 gr","quantity":5,"raw_price":5000,"discount":0}]}
```

The **_message_to_be_hashed_** is then used with the **_partner_secret_** value when calculating the HMAC

```
hmac = hmac_sha256(message_to_be_hashed, ABCDEFG123)
```

The resulting hmac is in binary format, it is then base64 encoded

```
result = bas64_encode(hmac)
       = +GrDKknDsrMW1SJv2d1GeBO8iHUR8CypU9c0LxvRklo=
```

Partner must include this HMAC value in HTTP header: "**_secret_**" along with HTTP header "**_partner_id_**". Example request that the partner needs to send becomes as follows:

```cURL
POST /v1/partner/order/create HTTP/1.1
Host: api.connexi.id
Content-Type: application/json
partner_id: B98KL87
secret: +GrDKknDsrMW1SJv2d1GeBO8iHUR8CypU9c0LxvRklo=

{"order_id":"ORD-256/20190627/FMCG/OA","order_date":"2019-06-02T16:31:55+07:00","status":"accepted","customer_reference":"DHU9868NGY","shipment_reference":"","delivery_name":"John Smith","delivery_email":"john.fictional.smith@gmail.com","delivery_street_address":"Jl. Anggrek No.106 Blok C5","delivery_region":"DKI Jakarta","delivery_city":"Kota Jakarta Barat - Cengkareng","delivery_country":"Indonesia","delivery_post_code":"11720","delivery_method":"JNE Reguler","delivery_mobile":"082101871618","airway_bill_number":"AWB12345678","shipping_total":15000,"line_items":[{"sku":"DKL0907","name":"Organic Instant Noodles Special Chicken Flavor - 150 gr","quantity":2,"raw_price":10000,"discount":100},{"sku":"CCF0985","name":"Organic Instant Coffee With Brown Sugar - 100 gr","quantity":5,"raw_price":5000,"discount":0}]}
```

Code examples of on how to calculate HMAC in various programming languages: <https://github.com/danharper/hmac-examples>

## Another example

- The partner wants to send a HTTP request like the following:

```cURL
GET /v1/partner/order?since=2018-10-13T13:34:52Z&until=2018-10-16T19:22:39Z&limit=100&offset=0 HTTP/1.1
Host: api.connexi.id
```

The request URI of the HTTP request is "_/v1/partner/order?since=2018-10-13T13:34:52Z&until=2018-10-16T19:22:39Z&limit=100&offset=0_"

<aside class="notice">Note: The query string values in the request URI should be in their original form (i.e. not URL encoded) when composing HMAC. For example:</aside>

- "_since_" in the example above is "_2018-10-13T13:34:52Z_", not URL encoded value "_2018-10-13T13%3A34%3A52Z_",
- "_until_" is "_2018-10-16T19:22:39Z_", not URL encoded value "_2018-10-16T19%3A22%3A39Z_"

```
message_to_be_hashed = /v1/partner/order?since=2018-10-13T13:34:52Z&until=2018-10-16T19:22:39Z&limit=100&offset=0
hmac = hmac_sha256(message_to_be_hashed, ABCDEFG123)
secret = bas64_encode(hmac) = /XjtjtmnE43I3SaTEp0u2Ia0FrjWQlU4yEgVQrOEHi4=
```

The HTTP request to send then becomes as follows:

```cURL
GET /v1/partner/order?since=2018-10-13T13:34:52Z&until=2018-10-16T19:22:39Z&limit=100&offset=0
Host : api.connexi.id
partner_id: B98KL87
secret: /XjtjtmnE43I3SaTEp0u2Ia0FrjWQlU4yEgVQrOEHi4=
```
