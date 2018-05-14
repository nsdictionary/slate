## check commission

Inquire the receive amount, and the commission information.

### endpoint
<code>POST: /inbound/check_commission</code>

### request
Parameter | Requried | Description
--------- | ------- | -----------
transfer_info['send_amount'] |O| transfer amount
transfer_info['send_amount_currency'] |O| send amount currency('KRW' fixed value)
wallet_info['transfer_currency'] |O| wallet currency for transfer
wallet_info['fee_currency'] |O| wallet currency for payment fee

> request parameter JSON structured like this:

```json
{
  "transfer_info": {
    "send_amount": "1000000",
    "send_amount_currency": "KRW"
  },
  "wallet_info": {
    "transfer_currency": "KRW",
    "fee_currency": "USD"
  }
}
```

### response
Parameter | Description
--------- | -----------
result | response success info(true/false)
data['transfer_info']['receive_amount'] | receive amount
data['transfer_info']['receive_amount_currency'] | receive amount currency
data['billing_info']['amount'] | amount to be deducted from wallet
data['billing_info']['currency'] | wallet currency
data['billing_info']['desc'] | transfer / distribution cost

> response JSON structured like this:

```json
{
  "result": true,
  "data": {
    "transfer_info": {
      "receive_amount": 1000000.0,
      "receive_amount_currency": "KRW"
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

<aside class="notice">
transfer_amount['send_amount'] must be in integer format
</aside>
