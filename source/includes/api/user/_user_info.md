## user info

송금인(유저) 정보를 조회합니다.

### endpoint
<code>GET: /outbound/users</code><br/>
<code>GET: /outbound/users/:id</code>

### request
Parameter | Requried | Description
--------- | ------- | -----------
page |X| default: 1, offset: 5
id |X| 센트비 유저 고유 id

> request parameter JSON structured like this:

```json
{
  "page": "2"
}
```

### response
Parameter | Description
--------- | -----------
result | 요청 정보에 대한 결과(true/false)
**data** | **유저정보 Hash**

### data
Parameter | Description
--------- | -----------
id | 센트비 유저 고유 id
first_name | 이름
last_name | 성
email | 이메일
created_at | 유저 생성 일시
phone_number | 휴대폰 번호
phone_country_code | 휴대폰 국가 코드
external_id | 파트너사 유저 고유 id

### data['verifications_status']
Parameter | Description
--------- | -----------
mobile | standby / completed
documents | standby / processing / rejected / pending / completed
bank | standby / processing / rejected / pending / completed

> response JSON structured like this:

```json
{
  "result": true,
  "data": {
    "id": 15,
    "first_name": "firsrt",
    "last_name": "last",
    "email": "test@outbound.com",
    "created_at": "2018-06-14T10:29:20.000+09:00",
    "phone_country_code": "KR",
    "phone_number": "010-3333-4442",
    "external_id": "3",
    "verifications_status": {
      "mobile": "completed",
      "documents": "standby",
      "bank": "standby"
    }
  }
}
```
