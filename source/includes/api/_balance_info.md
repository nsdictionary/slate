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
    "amount": 10000.0,
    "currency": "USD"
  }
}
```

### response
Parameter | Description
--------- | -----------
result | response success info(true/false)
data['amount'] | credit amount
data['currency'] | credit currency('USD' fixed value)
