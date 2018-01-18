## balance

View the Sentbe credit balance. (Prefunding)

### endpoint
<code>GET: /inbound/balance</code>

### request
No params

> response parameter JSON structured like this:

```json
{
  "result": true,
  "data": {
    "amount": 12409925.0,
    "currency": "KRW"
  }
}
```

### response
Parameter | Description
--------- | -----------
result | response success info(true/false)
data['amount'] | credit amount
data['currency'] | credit currency('KRW' fixed value)
