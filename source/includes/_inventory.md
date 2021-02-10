# Inventory

## Update Stocks

### HTTP Request

`POST /v1/partner/inventory/updatestocks`

### Header Parameters

| Name       | Required | Type   | Description                      |
| ---------- | -------- | ------ | ----------------------------------------------------------------------------------------------------------------- |
| partner-id | Yes      | String | Partner ID value (given from SIRCLO) used for partner identification                                              |
| secret     | Yes      | String | HMAC (Hash Based Message Authentication Code), refer to section: <a href="#composing-secret">Composing Secret</a> |

### Request Body Parameters

Request body must be a JSON document with the following properties

| Name                           | Required | Type   | Description                                   |
| ------------------------------ | -------- | ------ | --------------------------------------------- |
|sku| Yes | String | Stock keeping unit (SKU) of the product in Connexi |
|sync_stock| No | String | Synchronization between the stock marketplace and default 'false' |
|warehouse| Yes | String | Name of warehouse provide multi warehouse in Connexi, for those who don't use multi warehouse, fill in "default"|
|available_stock|Yes | Integer | Available stock of the product in Connexi (the integer not negatif and by default '0')|
|buffer_stock| Yes | Integer | buffer stock of the product in Connexi (not bigger than available_stock, the integer not negatif and by default '0')| 
| channel_stock | Yes | Array | stock of the product displayed in each marketplace|
|channel_stock - code| Yes | String | Marketplace code in Connexi | 
|channel_stock - qty | Yes | Integer | The number stock of product displayed in marketplace | 

> Request body example:

```json
 {
   "sku": "sku1", 
   "sync_stock": false, 
   "warehouse": "default", 
   "available_stock": 100, 
   "buffer_stock": 0, 
   "channel_stock": [ 
     {
       "code": "bklp", 
       "qty": 30 
     },
     {
       "code": "blib",
       "qty": 20
     }
   ]
 }
```

> The above request returns JSON structured like this:

```json
{
"transaction_code" : "591d4ab5-841e-499a-bfa2-99a4fb879e44"
}
 
```

## Get Update History

### HTTP Request

`GET /v1/partner/inventory/history`

### Header Parameters

| Name       | Required | Type   | Description                      |
| ---------- | -------- | ------ | ----------------------------------------------------------------------------------------------------------------- |
| partner-id | Yes      | String | Partner ID value (given from SIRCLO) used for partner identification                                              |
| secret     | Yes      | String | HMAC (Hash Based Message Authentication Code), refer to section: <a href="#composing-secret">Composing Secret</a> |

### Path Parameters

| Parameter | Required | Type    | Description                                                                                            |
| --------- | -------- | ------- | ------------------------------------------------------------------------------------------------------ |
|updated_at | No | Timestamp | The last updated Timestamp for this stock and must be in RFC3339 format Timestamp|
| limit     | Yes      | Integer | Number of stock history that want to be returned (by default the number is 100)                               |
| offset    | Yes      | Integer | To be used for pagination (use value 10 if you want to skip 10 first datas, by default the value is 0) |

> Request example
> `GET /v1/partner/inventory/history?updated_at=2021-02-05T15:04:05Z&offset=0&limit=10`

> The above request returns JSON structured like this: 

```json 
{
   "data": [
        {
           "id": 233,
           "tenant_id": 123, 
           "user_id": 0, 
           "transaction_code": "2a4048b2-bdaf-4d31-922c-58472691f217",
           "action_name": "partner_update_stocks", 
           "upload_file_url": "", 
           "total_sku": 1, 
           "created_at": "2021-02-09T03:18:40.424625Z", 
           "updated_at": "2021-02-09T03:19:20.240855Z", 
           "finished_at": "2021-02-09T03:19:20Z", 
           "update_stock_history_item": [
               {
                   "id": 11701,
                   "update_stock_history_id": 1234,
                   "store_id": 123,  
                   "store_name": "Test Toko", 
                   "warehouse_id": 0,
                   "warehouse_name": "default",
                   "variant_id": 334621, 
                   "sku": "asdfg",
                   "remote_variant": "{\"item_id\": 12346, \"variation_id\": 0}",
                   "row_number": 0, 
                   "channel": "shpe", 
                   "qty": 10,
                   "retrier_count": 1,
                   "progress": false,
                   "client_reponse": "{\"item\":{\"item_id\":12345,\"modified_time\":1612840732}}", 
                   "message": "Successfully Updated",
                   "success": true, 
                   "created_at": "2021-02-09T03:18:40.529807Z",
                   "updated_at": "2021-02-09T03:18:52.879618Z",
                   "finished_at": "2021-02-09T03:18:52Z"
               }
           ]
       }
   ],
   "total_record": 120, 
   "offset": 0,
   "limit": 1,
   "message": "",
   "reference": "591d4ab5-841e-499a-bfa2-99a4fb879e44"
}
```