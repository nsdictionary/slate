## check_commission

Inquiry the send amount, receive amount, and the commission information.

### endpoint
<code>GET: /inbound/check_commission</code>

### request
Parameter | Requried | Description
--------- | ------- | -----------
transfer_amount |O| trnasfer amount
send_amount_currency |O| send amount currency
receive_amount_currency |O| receive amount currency('KRW')
calc_by |O| S: Calculated by Sending Currency <br/> P: Calculated by Payout Currency

> request parameter JSON structured like this:

```json
{
  "transfer_amount": "100",
  "calc_by": "S",
  "send_amount_currency": "USD",
  "receive_amount_currency": "KRW"
}
```

### response
Parameter | Description
--------- | -----------
result | response success info(true/false)
send_amount | send amount
send_amount_currency | send amount currency
receive_amount | receive amount
receive_amount_currency | receive amount currency
commission | sentbe commission amount
commission_currency | commission currency('KRW')
total_amount | amount to be deducted from sentbe credit
total_amount_currency | total amount currency('KRW')

> response JSON structured like this:

```json
{
  "send_amount": "100.0",
  "send_amount_currency": "USD",
  "receive_amount": "114271.0",
  "receive_amount_currency": "KRW",
  "commission": "2.5",
  "commission_currency": "USD",
  "total_amount": "102.5",
  "total_amount_currency": "USD"
}
```

<aside class="notice">
transfer_amount must be intgeger format
</aside>
