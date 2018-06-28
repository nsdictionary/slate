## create recipient

수취인 정보를 바탕으로 수취인 모델을 생성합니다.

### endpoint
<code>POST: /outbound/recipients</code>

### request
<a href="#recipient-params">recipient_params api</a>를 통해 파라미터 정보 조회

> request parameter JSON structured like this:

```json
{
  "user_id": "15",
  "first_name": "firsrt",
  "last_name": "last",
  "country": "PH",
  "receive_method": "bank",
  "external_id": "2",
  "phone_number": "010-3333-4442",
  "phone_country_code": "KR",
  "address_attributes": {
    "region": "seoul",
    "city": "seoul",
    "country": "KR"
  },
  "bank_attributes": {
    "account_type": "Savings",
    "branch": "123",
    "account_number": "1234567890123456",
    "account_holder_name": "홍길동테스트",
    "name": "10305"
  }
}
```

### response
Parameter | Description
--------- | -----------
result | 요청 정보에 대한 결과(true/false)
data | 수취인 정보 Hash
data['receive_method_info'] | 생성된 수취방법에 대한 정보

### data
Parameter | Description
--------- | -----------
id | 센트비 수취인 고유 ID
first_name | 이름
last_name | 성
email | 이메일
created_at | 수취인 생성 일시
phone_number | 휴대폰 번호
phone_country_code | 휴대폰 번호 국가 코드 (ISO ALPHA-2 Code)
birth_date | 수취인 생년월일
receive_method | 수취방법 (Bank / Pickup / DebitCard / HomeDelivery)


> response JSON structured like this:

```json
{
  "result": true,
  "data": {
    "id": 53,
    "first_name": "firsrt",
    "last_name": "last",
    "email": null,
    "created_at": "2018-06-19T13:45:33.000+09:00",
    "phone_country_code": "KR",
    "phone_number": "010-3333-4442",
    "birth_date": null,
    "receive_method": "Bank",
    "receive_method_info": {
      "name": "10305",
      "account_number": "1234567890123456",
      "account_holder_name": "홍길동테스트",
      "branch": "123"
    }
  }
}
```

<aside class="warning">
response의 <code>data['id']</code>는 다른 request에 사용되기 때문에 파트너사의 데이터베이스에 저장해야합니다.
</aside>