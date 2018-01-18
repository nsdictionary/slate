## update_user_info

Update the sender information.

### endpoint
<code>POST: /inbound/update_user_info</code>

### request

Parameter | Requried | Description
--------- | ------- | -----------
user_id |O| user's unique id
email |X| sender's email
phone_country_code |X| ISO ALPHA-2 Code
phone_number |X| sender's phone number
birth_date |X| sender's birst date

> request parameter JSON structured like this:

```json
{
  "user_id": "47",
  "email": "sanghyun.ryu2@sentbe.com",
  "phone_country_code": "US",
  "phone_number": "010-1122-3344",
  "birth_date": "19891212"
}
```

### response
Parameter | Description
--------- | -----------
result | response success info(true/false)
data['id'] | user's unique id
data['first_name'] | user's firstname
data['last_name'] | user's last name
data['email'] | users's email
data['created_at'] | user created time
data['phone_country_code'] | phone country code
data['phone_number'] | users's phone number
data['external_id'] | partner's user unique id

> response JSON structured like this:

```json
{
  "result": true,
  "data": {
    "id": 47,
    "first_name": "sanghyun",
    "last_name": "ryu",
    "email": "sanghyun.ryu2@sentbe.com",
    "created_at": "2017-12-12T15:30:30.000+09:00",
    "phone_country_code": "US",
    "phone_number": "010-1122-3344",
    "external_id": "1"
  }
}
```
