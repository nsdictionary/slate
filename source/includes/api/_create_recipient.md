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
<a href="#recipient-info">수취인 정보 조회</a>의 response와 동일

<aside class="warning">
response의 <code>data['id']</code>는 다른 request에 사용되기 때문에 파트너사의 데이터베이스에 저장해야합니다.
</aside>