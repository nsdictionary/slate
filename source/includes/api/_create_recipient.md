## Create recipient

### endpoint
<code>/inbound/create_recipient</code>

### request

Parameter | Requried | Description
--------- | ------- | -----------
phone_country_code |O| ISO ALPHA-2 Code
phone_number |O| recipient's phone number
external_id |O| recipient's user unique id
first_name |O| recipient's first name
middle_name |X| recipient's middle name
last_name |O| recipient's last name
country |O| ISO ALPHA-2 Code
birth_date |O| recipient's birst date
user_id |O| 'user_id' on create_user response
email |X| recipient's email
bank_attributes['name'] |O| recipient's bank code
bank_attributes['account_number'] |O| recipient's account number
bank_attributes['account_holder_name'] |O| recipient's account holder name
bank_attributes['branch'] |X| recipient's bank branch

> request parameter JSON structured like this:

```json
{
  "bank_attributes": {
    "name": "002",
    "account_number": "12341234",
    "account_holder_name": "gildong hong"
  },
  "country": "KR",
  "phone_country_code": "KR",
  "birth_date": "19901201",
  "external_id": "1",
  "first_name": "gildong",
  "last_name": "hong",
  "email": "hong@sentbe.com",
  "user_id": "47",
  "phone_number": "010-5678-5678"
}
```

### response
Parameter | Description
--------- | -----------
result | response success info(true/false)
data['id'] | recipient's unique id
data['first_name'] | recipient's firstname
data['last_name'] | recipient's last name
data['email'] | recipient's email
data['created_at'] | recipient created time
data['phone_country_code'] | phone country code
data['phone_number'] | recipient's phone number
data['external_id'] | partner's user unique id
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
    "external_id": "1",
    "bank_attributes": {
      "name": "002",
      "account_number": "12341234",
      "account_holder_name": "gildong hong",
      "branch": null
    }
  }
}
```


<aside class="warning">
response의 data['id']를 디비에 저장해 두어야 나중에 정보를 수정하거나 호출할 수 있습니다.
</aside>
