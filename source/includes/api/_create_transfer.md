## create_transfer

Proceed the remit process.

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

<aside class="notice">
If the recipient did not proceed with the verification process, the verification link will be sent by SMS, and the remittance will proceed when the verification is completed.
</aside>

<aside class="warning">
You must save the response's <code>data['transfer_id']</code> in the database before you can modify or invoke the information.
</aside>

