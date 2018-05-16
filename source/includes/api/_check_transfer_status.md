## check transfer status

View the remit process progress information.

### endpoint
<code>GET: /inbound/transfers</code><br/>
<code>GET: /inbound/transfers/:id</code>

### request
Parameter | Requried | Description
--------- | ------- | -----------
page |X| default: 1, offset: 5

> request parameter JSON structured like this:

```json
{
  "page": "2"
}
```

### response
Parameter | Description
--------- | -----------
result | response success info(true/false)
data['transfer_info']['user_id'] | user's unique id
data['transfer_info']['recipient_id'] | recipient's unique id
data['transfer_info']['transfer_id'] | transfer's unique id
data['transfer_info']['sender_country'] | user's nationality
data['transfer_info']['receive_amount'] | receive amount
data['transfer_info']['receive_amount_currency'] | receive amount currency
data['transfer_info']['status'] | Waiting verification<br/> Processing<br/> AML filtered<br/> Complete<br/> Canceled<br/> Expired<br/> Refunded<br/><a href="#3-transfer-status">See transfer status</a>
data['transfer_info']['created_at'] | transfer created time
data['billing_info']['amount'] | amount to be deducted from wallet
data['billing_info']['currency'] | wallet currency
data['billing_info']['desc'] | transfer / distribution cost

> response JSON structured like this:

```json
{
  "result": true,
  "data": {
    "transfer_info": {
      "user_id": 47,
      "recipient_id": 10,
      "transfer_id": 23,
      "sender_country": "KR",
      "receive_amount": 1000000.0,
      "receive_amount_currency": "KRW",
      "status": "Processing",
      "created_at": "2018-05-14T13:23:09.000+09:00"
    },
    "billing_info": [
      {
        "amount": 1000000.0,
        "currency": "KRW",
        "desc": "transfer"
      },
      {
        "amount": 2.5,
        "currency": "USD",
        "desc": "distribution cost"
      }
    ]
  }
}
```
