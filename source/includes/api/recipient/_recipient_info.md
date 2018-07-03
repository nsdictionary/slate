## recipient info

수취인 정보를 조회합니다.

### endpoint
<code>GET: /outbound/recipients</code><br/>
<code>GET: /outbound/recipients/:id</code>

### request
Parameter | Requried | Description
--------- | ------- | -----------
page |X| default: 1, offset: 5
id |X| 센트비 수취인 고유 id

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
**data** | **수취인 정보 Hash**

### data
Parameter | Description
--------- | -----------
id | 센트비 수취인 고유 id
first_name | 이름
last_name | 성
email | 이메일
created_at | 수취인 생성 일시
phone_number | 휴대폰 번호
phone_country_code | 휴대폰 번호 국가 코드 (ISO ALPHA-2 Code)
birth_date | 수취인 생년월일
receive_method | 수취방법 (Bank / Pickup / DebitCard / HomeDelivery)
**receive_method_info** | **생성된 수취방법에 대한 정보**

### receive_method_info(Bank) 
Parameter | Description
--------- | ----------- 
name | <a href="#remittance-code-info">코드 목록 조회 api</a>
account_number | 계좌번호
account_holder_name | 계좌주명
branch | <a href="#remittance-code-info"> 코드 목록 조회 api</a>

### receive_method_info(Pickup)
Parameter | Description
--------- | -----------
name | <a href="#remittance-code-info">코드 목록 조회 api</a>
branch | <a href="#remittance-code-info"> 코드 목록 조회 api</a>

### receive_method_info(DebitCard)
Parameter | Description
--------- | -----------
name | <a href="#remittance-code-info">코드 목록 조회 api</a>
card_number | 카드번호
card_holder_name | 카드 소유자 성명

### receive_method_info(HomeDelivery)
Parameter | Description
--------- | -----------
name | <a href="#remittance-code-info">코드 목록 조회 api</a>


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

