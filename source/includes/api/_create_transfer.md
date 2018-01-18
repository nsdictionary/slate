## Create transfer

송금 프로세스를 진행합니다.

### endpoint
<code>GET: /inbound/create_transfer</code>

### request
Parameter | Requried | Description
--------- | ------- | -----------
user_id |O| user's unique id
recipient_id |O| recipient's unique id
transfer_amount |O| transfer amount
calc_by |O| S: Calculated by Sending Currency <br/> P: Calculated by Payout Currency
send_amount_currency |O| send amount currency
receive_amount_currency |O| receive amount currency('KRW')
external_id |O| partner's transer unique id

> request parameter JSON structured like this:

```json
{
  "user_id": "47",
  "recipient_id": "10",
  "transfer_amount": "100",
  "calc_by": "S",
  "send_amount_currency": "USD",
  "receive_amount_currency": "KRW",
  "external_id": "23"
}
```

### response
Parameter | Description
--------- | -----------
result | response success info(true/false)
data['transfer_id'] | transfer's unique id
data['send_amount'] | send amount
data['send_amount_currency'] | send amount currency
data['receive_amount'] | receive amount
data['receive_amount_currency'] | receive amount currency
data['commission'] | sentbe commission amount
data['commission_currency'] | commission currency('KRW')
data['total_amount'] | amount to be deducted from sentbe credit
data['total_amount_currency'] | total amount currency('KRW')

> response JSON structured like this:

```json
{
  "result": true,
  "data": {
    "transfer_id": 12,
    "send_amount": "100.0",
    "send_amount_currency": "USD",
    "receive_amount": "114500.0",
    "receive_amount_currency": "KRW",
    "commission": "2863.0",
    "commission_currency": "KRW",
    "total_amount": "117363.0",
    "total_amount_currency": "KRW"
  }
}

```

<aside class="notice">
transfer_amount must be intgeger format
</aside>

<aside class="warning">
response의 data['transfer_id']를 디비에 저장해 두어야 나중에 정보를 수정하거나 호출할 수 있습니다.
</aside>
