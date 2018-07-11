## create bank verification

은행 인증을 위한 유저의 은행정보를 등록합니다.

### endpoint
<code>POST: /outbound/banks</code><br/>

### request
Parameter | Requried | Description
--------- | ------- | -----------
user_id |O| 센트비 유저 고유 id
name |O| <a href="#remittance-code-info">코드 목록 조회 api</a>
account_number |O| 계좌번호
account_holder_name |O| 계좌주명

> request parameter JSON structured like this:

```json
{
  "user_id": "15",
  "name": "10305",
  "account_number": "1234567890123456",
  "account_holder_name": "홍길동테스트"
}
```

### response
Parameter | Description
--------- | -----------
result | 요청 정보에 대한 결과(true/false)
data | true


> response JSON structured like this:

```json
{
  "result" : true,
  "data" : true 
}
```


<aside class="warning">
유저 생성시 등록한 생년월일, 국적, 성별을 포함한 계좌정보를 통해서 오픈플랫폼 실명조회api를 호출하게 됩니다.
정확한 정보가 아닐경우 은행 생성이 reject 될 수 있습니다.
</aside>





