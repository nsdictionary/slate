## User info

송금인 정보를 조회합니다.

### endpoint
<code>POST: /inbound/user_info</code>

### request

Parameter | Requried | Description
--------- | ------- | -----------
user_id |O| user's unique id

> request parameter JSON structured like this:

```json
{
  "user_id": "47"
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
    "email": "sanghyun.ryu@sentbe.com",
    "created_at": "2017-12-12T15:30:30.000+09:00",
    "phone_country_code": "US",
    "phone_number": "010-1234-1234",
    "external_id": "1"
  }
}
```
