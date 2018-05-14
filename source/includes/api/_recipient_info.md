## recipient info

View your payee information.

### endpoint
<code>GET: /inbound/recipients/:id</code>

### request
No params

### response
Parameter | Description
--------- | -----------
result | response success info(true/false)
data['id'] | recipient's unique id
data['first_name'] | recipient's first name
data['last_name'] | recipient's last name
data['email'] | recipient's email
data['created_at'] | recipient created time
data['phone_country_code'] | phone country code
data['phone_number'] | recipient's phone number
data['bank_attributes']['name'] | recipient's bank code
data['bank_attributes']['account_number'] | recipient's account number
data['bank_attributes']['account_holder_name'] | recipient's account holder name
data['bank_attributes']['branch'] | recipient's bank branch

> response JSON structured like this:

```json
{
  "result": true,
  "data": {
    "id": 10,
    "email": "hong@sentbe.com",
    "created_at": "2017-12-12T15:30:39.000+09:00",
    "phone_country_code": "KR",
    "phone_number": "010-5678-5678",
    "birth_date": "19901201",
    "bank_attributes": {
      "name": "002",
      "account_number": "12341234",
      "account_holder_name": "gildong hong",
      "branch": null
    }
  }
}
```
