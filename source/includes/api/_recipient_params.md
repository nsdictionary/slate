## recipient params

수취인을 생성할때 국가/수취 방법별로 필요한 파라미터 정보를 확인.

### endpoint
<code>GET: /outbound/params</code>

<code>GET: /outbound/params/:country</code>

<code>GET: /outbound/params/:country/:receive_method</code>

### request

Parameter | Requried | Description
--------- | ------- | -----------
country |X| 생성하려는 수취인의 국적 국가코드(ISO ALPHA-2 Code)
receive_method |X| 수취방법 (Bank / Pickup / DebitCard / HomeDelivery)

### response
Parameter | Description
--------- | -----------
result | 요청 정보에 대한 결과(true/false)
**data** | **파라미터 정보**

### data
Parameter | Description
--------- | -----------
country | 국적 국가 코드 (ISO ALPHA-2 Code)
receive_method | 수취방법 (Bank / Pickup / DebitCard / HomeDelivery)
user_id | 센트비 유저 고유 ID
first_name | 이름
middle_name | 가운데 이름
last_name | 성
external_id| 파트너사 수취인 고유 ID
phone_country_code | 휴대폰 번호
phone_number | 휴대폰 번호 국가 코드 (ISO ALPHA-2 Code)
identification_number | 수취인 주민식별번호
**address_attributes** | **주소 정보 params**
**bank_attributes** | **은행 계좌 정보 params**
**debit_card_attributes** | **신용카드 정보 params**


### address_attributes
Parameter | Requried | Description
--------- | ------- | -----------
region | 지역
country | 국가 코드 (ISO ALPHA-2 Code)
line_1 | 상세주소 1
line_2 | 상세주소 2
city | 도시
postal_code | 우편번호

### bank_attributes
Parameter | Requried | Description
--------- | ------- | -----------
name | <a href="#">코드 목록 조회 api</a>
account_number | 계좌번호
account_holder_name | 계좌주명
account_type | 계좌 유형 (savings / current)
branch | <a href="#"> 코드 목록 조회 api</a>

### debit_card_attributes
Parameter | Requried | Description
--------- | ------- | -----------
name | <a href="#">코드 목록 조회 api</a>
card_number | 카드번호
card_holder_name | 카드 소유자 성명

> response JSON structured like this:

```json
{
  "result": true,
  "data": {
    "required": [
      "country",
      "receive_method",
      "user_id",
      "first_name",
      "last_name",
      "external_id",
      "phone_country_code",
      "phone_number",
      {
        "address_attributes": [
          "country",
          "city",
          "region"
        ],
        "bank_attributes": [
          "name",
          "account_number",
          "account_holder_name",
          "account_type"
        ]
      }
    ],
    "optional": [
      "middle_name",
      {
        "bank_attributes": [
          "branch"
        ]
      }
    ]
  }
}
```