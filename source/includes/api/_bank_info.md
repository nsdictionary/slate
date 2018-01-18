## bank_info

You can view a list of banks that you can use when generating payee information.

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
