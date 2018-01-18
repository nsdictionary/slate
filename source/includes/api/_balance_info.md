## Balance info

프리펀딩으로 사전에 충전된 크레딧 잔량을 조회합니다.

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
