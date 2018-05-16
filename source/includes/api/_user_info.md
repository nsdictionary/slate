## user info

View the sender information.

### endpoint
<code>GET: /inbound/users</code><br/>
<code>GET: /inbound/users/:id</code>

### request
Parameter | Requried | Description
--------- | ------- | -----------
page |X| default: 1, offset: 5

> request parameter JSON structured like this:

```json
{
  "page": "2"
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
    "phone_number": "010-1234-1234"
  }
}
```
