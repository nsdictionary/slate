## bank_info

수취인 정보를 생성할때 사용할수 있는 은행 리스트를 조회할 수 있습니다.

### endpoint
<code>GET: /inbound/bank_info</code>

### request
No params

> response parameter JSON structured like this:

```json
{
  "result": true,
  "data": {
    "002": {
      "label": "KDB산업"
    },
    "032": {
      "label": "부산은행"
    },...{}
  }
}
```

### response
Parameter | Description
--------- | -----------
result | response success info(true/false)
data.keys | bank codes
data[key]['label'] | bank display name
