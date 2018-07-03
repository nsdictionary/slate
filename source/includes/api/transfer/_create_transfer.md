## create transfer

Proceed the remit process.

### endpoint
<code>POST: /inbound/transfers</code>

### request
Parameter | Requried | Description
--------- | ------- | -----------
user_id |O| user's unique id
recipient_id |O| recipient's unique id
external_id |O| partner's transfer unique id
transfer_info['send_amount'] |O| transfer amount
transfer_info['send_amount_currency'] |O| send amount currency('KRW' fixed value)
wallet_info['transfer_currency'] |O| wallet currency for transfer
wallet_info['fee_currency'] |O| wallet currency for payment fee

> request parameter JSON structured like this:

```json
{
  "user_id": "47",
  "recipient_id": "10",
  "external_id": "23",
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

<aside class="notice">
transfer_amount must be in integer format
</aside>

<aside class="notice">
If the recipient did not proceed with the verification process, a verification link will be sent by SMS, and the remittance will proceed when the verification is completed.
</aside>

<aside class="warning">
You must save the response's <code>data['transfer_id']</code> in the database before you can modify or invoke the information.
</aside>

