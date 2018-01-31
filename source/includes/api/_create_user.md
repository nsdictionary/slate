## create_user

Send the sender information to create the model.

### endpoint
<code>POST: /inbound/create_user</code>

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
birth_date |O| sender's birth date
email |X| sender's email

> request parameter JSON structured like this:

```json
{
  "phone_country_code": "US",
  "birth_date": "19890101",
  "external_id": "1",
  "last_name": "ryu",
  "email": "sanghyun.ryu@sentbe.com",
  "nationality": "US",
  "phone_number": "010-1234-1234",
  "first_name": "sanghyun"
}
```

### response
Parameter | Description
--------- | -----------
result | response success info(true/false)
data['id'] | user's unique id
data['first_name'] | user's first name
data['last_name'] | user's last name
data['email'] | user's email
data['created_at'] | user created time
data['phone_country_code'] | phone country code
data['phone_number'] | user's phone number
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


<aside class="warning">
The <code>data ['id']</code> of the response must be stored in the database before you can modify or invoke the information.
</aside>
