## Create user

### endpoint
<code>/inbound/user_info</code>

### request

Parameter | Requried | Description
--------- | ------- | -----------
phone_country_code |O| ISO ALPHA-2 Code
phone_number |O| sender's phone number
external_id |O| partner's user unique id
first_name |O| sender's first name
middle_name |X| sender's middle name
last_name |O| sender's last name
nationality |O| ISO ALPHA-2 Code
birth_date |O| sender's birst date
email |X| sender's email

> request parameter JSON structured like this:

```json
{
  "phone_country_code": "ID",
  "birth_date": "19890101",
  "external_id": "1",
  "last_name": "ryu",
  "email": "sanghyun.ryu@sentbe.com",
  "nationality": "KR",
  "phone_number": "010-1234-1234",
  "first_name": "sanghyun"
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
    "phone_country_code": "ID",
    "phone_number": "010-1234-1234",
    "external_id": "1"
  }
}
```


<aside class="warning">
response의 data['id']를 디비에 저장해 두어야 나중에 정보를 수정하거나 호출할 수 있습니다.
</aside>
