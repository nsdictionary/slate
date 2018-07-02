# API Reference(user)

## create user

송금인 정보를 바탕으로 송금인 모델을 생성합니다.

### endpoint
<code>POST: /outbound/users</code>

### request

Parameter | Requried | Description
--------- | ------- | -----------
external_id |O| 파트너사 유저 고유 ID
nationality |O| 국적 국가 코드 (ISO ALPHA-2 Code)
phone_number |O| 휴대폰 번호
phone_country_code |O| 휴대폰 번호 국가 코드 (ISO ALPHA-2 Code)
birth_date |O| 생년월일 (YYYYMMDD)
funds_source |O| <a href="#get-list-data">목록 조회 api</a>
occupation |O| <a href="#get-list-data">목록 조회 api</a>
often_send_country |O| <a href="#get-list-data">목록 조회 api</a>
transfer_purpose |O| <a href="#get-list-data">목록 조회 api</a>
password |O| 유저가 사용할 비밀번호
first_name |O| 이름
middle_name |X| 가운데 이름
last_name |O| 성
identification_number |X| 주민식별번호
passport |X| 여권번호
email |O| 이메일
gender |O| 성별 (M/F)
**address_attributes** |O| **주소정보 hash (아래 sub parameter 참조)**
**agreements_attributes** |O| **동의정보 hash (아래 sub parameter 참조)**

### address_attributes
Parameter | Requried | Description
--------- | ------- | -----------
region |O| 지역
country |O| 국가 코드 (ISO ALPHA-2 Code)
line_1 |O| 상세주소 1
line_2 |X| 상세주소 2
city |O| 도시
postal_code |O| 우편번호

### agreements_attributes
Parameter | Requried | Description
--------- | ------- | -----------
unique_id_info |O| 고유식별정보 수집
third_party_info |O| 개인정보의 제3자 제공
electronic_financial_transactions |O| 전자금융거래이용약관
privacy_info |O| 개인정보 처리방침
small_sum_foreign |O| 소액해외송금서비스 이용약관


> request parameter JSON structured like this:

```json
{
  "external_id": "3",
  "nationality": "KR",
  "phone_number": "010-3333-4445",
  "birth_date": "19880101",
  "funds_source": "business_earnings",
  "occupation": "company_employee",
  "often_send_country": "PH",
  "phone_country_code": "KR",
  "password": "1234qwer!@",
  "first_name": "firsrt",
  "transfer_purpose": "saving",
  "identification_number": "88010112345677",
  "last_name": "last",
  "email": "test@outbound.com",
  "gender": "M",
  "address_attributes": {
    "region": "seoul",
    "country": "KR",
    "line_1": "gangnamgu 111",
    "city": "seoul",
    "postal_code": "12345"
  },
  "agreements_attributes": {
    "unique_id_info": "true",
    "third_party_info": "true",
    "electronic_financial_transactions": "true",
    "privacy_info": "true",
    "small_sum_foreign": "true"
  }
}
```

### response
<a href="#user-info">송금인 정보 조회</a>의 response와 동일

<aside class="warning">
response의 <code>data['id']</code>는 다른 request에 사용되기 때문에 파트너사의 데이터베이스에 저장해야합니다.
</aside>

<aside class="notice">
request할때 <code>identification_number</code> <code>passport</code> 둘중 하나는 필수로 보내야 합니다
</aside>

<aside class="notice">
유저를 생성할 경우 자동으로 휴대폰으로 인증번호가 발송됩니다.
</aside>