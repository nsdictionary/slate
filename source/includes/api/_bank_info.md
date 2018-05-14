## bank info

You can view a list of banks that you can use when generating payee information.

### endpoint
<code>GET: /inbound/banks</code>

### request
No params

> response parameter JSON structured like this:

```json
{

  "result": true,
  "data": {
     "10316": {
      "label": "새마을은행"
    },
    "10307": {
      "label": "IBK기업"
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
