## update_user_info

생성한 유저의 정보를 변경 합니다.

### endpoint
<code>POST: /outbound/update_user_info</code>

### request
Parameter | Requried | Description
--------- | ------- | -----------
user_id |O| 센트비 유저 고유 id
email |X| 이메일
phone_number |X| 휴대폰 번호
password |X| 유저가 사용할 비밀번호
existing_password |X| 변경하기 전 현재 비밀번호
funds_source |X| <a href="#get-list-data">목록 조회 api</a>
transfer_purpose |X| <a href="#get-list-data">목록 조회 api</a>
occupation |X| <a href="#get-list-data">목록 조회 api</a>
often_send_country |X| <a href="#get-list-data">목록 조회 api</a>
**address_attributes** |X| **주소정보 hash (아래 sub parameter 참조)**

### address_attributes
Parameter | Requried | Description
--------- | ------- | -----------
region |X| 지역
country |X| 국가 코드 (ISO ALPHA-2 Code)
line_1 |X| 상세주소 1
line_2 |X| 상세주소 2
city |X| 도시
postal_code |X| 우편번호


> request parameter JSON structured like this:

```json
{
  "existing_password": "1234qwer!@",
  "password": "asdfzxcv!@",
  "often_send_country": "PH",
  "transfer_purpose": "saving",
  "email": "test3@outbound.com",
  "occupation": "company_employee",
  "address_attributes": {
    "postal_code": "12345",
    "region": "seoul",
    "country": "KR",
    "line_1": "gangnamgu 111",
    "city": "seoul",
    "line_2": "234"
  },
  "funds_source": "business_earnings"
}
```

### response
<a href="#user-info">송금인 정보 조회</a>의 response와 동일
