## balance

View the Sentbe credit balance. (Prefunding)

### endpoint
<code>GET: /inbound/balances</code><br/>
<code>GET: /inbound/balances/:currency</code>

### request
No params

### response
Parameter | Description
--------- | -----------
result | response success info(true/false)
data['amount'] | credit amount
data['currency'] | credit currency(currently supported 'USD' and 'KRW')

> response parameter JSON structured like this:

```json
{
  "result": true,
  "data": [
    {
      "amount": 10000.0,
      "currency": "USD"
    },
    {
      "amount": 15000000.0,
      "currency": "KRW"
    }
  ]
}
```
