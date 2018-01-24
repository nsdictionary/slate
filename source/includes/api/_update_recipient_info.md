## update_recipient_info

Update the payee information.

### endpoint
<code>POST: /inbound/update_recipient_info</code>

### request

Parameter | Requried | Description
--------- | ------- | -----------
recipient_id |O| recipient's unique id
email |X| recipient's email
phone_country_code |X| ISO ALPHA-2 Code
phone_number |X| recipient's phone number
birth_date |X| recipient's birth date
bank_attributes['account_number'] |X| recipient's account number
bank_attributes['account_holder_name'] |X| recipient's account holder name
bank_attributes['branch'] |X| recipient's bank branch

> request parameter JSON structured like this:

```json
{
  "recipient_id": "11",
  "email": "hong2@sentbe.com",
  "bank_attributes": {
    "name": "020",
    "account_number": "56785678"
  },
  "phone_country_code": "KR",
  "phone_number": "010-5566-7788"
}
```

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
    "email": "hong2@sentbe.com",
    "created_at": "2017-12-12T15:30:39.000+09:00",
    "phone_country_code": "KR",
    "phone_number": "010-5566-7788",
    "birth_date": "19901201",
    "external_id": "1",
    "bank_attributes": {
      "name": "020",
      "account_number": "56785678",
      "account_holder_name": "gildong hong",
      "branch": null
    }
  }
}
```

<aside class="warning">
Once the recipient has completed the verification process, the information can not be edited.
</aside>

