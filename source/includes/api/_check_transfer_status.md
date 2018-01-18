## Check transfer status

송금 프로세스 진행 정보를 조회합니다.

### endpoint
<code>GET: /inbound/check_transfer_status</code>

### request
Parameter | Requried | Description
--------- | ------- | -----------
transfer_id |O| transfer's unique id

> request parameter JSON structured like this:

```json
{
  "transfer_id": "12"
}
```

### response
Parameter | Description
--------- | -----------
result | response success info(true/false)
data['id'] | transfer's unique id
data['user_id'] | user's unique id
data['recipient_id'] | recipient's unique id
data['sender_country'] | user's nationality
data['send_amount'] | send amount
data['send_amount_currency'] | send amount currency
data['receive_amount'] | receive amount
data['receive_amount_currency'] | receive amount currency
data['commission'] | sentbe commission amount
data['commission_currency'] | commission currency('KRW')
data['status'] | Waiting verification<br/> Processing<br/> AML filtered<br/> Complete<br/> Canceled<br/> Expired<br/> Refunded<br/>
data['created_at'] | transfer created time

> response JSON structured like this:

```json
{
  "result": true,
  "data": {
    "id": 12,
    "user_id": 47,
    "recipient_id": 10,
    "sender_country": "US",
    "send_amount": 100.0,
    "send_amount_currency": "USD",
    "commission": 2863.0,
    "commission_currency": "KRW",
    "receive_amount": 114500.0,
    "receive_amount_currency": "KRW",
    "status": "Processing",
    "created_at": "2017-12-12T15:31:47.000+09:00"
  }
}
```
