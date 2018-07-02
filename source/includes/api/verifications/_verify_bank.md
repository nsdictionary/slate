## verify bank

등록된 은행의 계좌에 1원을 송금하여 인증번호를 세팅합니다.

### endpoint
<code>POST: /outbound/verifications/bank/verify</code><br/>

### request
Parameter | Requried | Description
--------- | ------- | -----------
user_id |O| 센트비 유저 고유 id
token |O| 문자로 받은 인증번호 4자리

> request parameter JSON structured like this:

```json
{
  "user_id": "15",
  "token": "0321"
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
<aside class="notice">
유저가 해당 계좌의 거래내역 조회시 인증번호를 확인 할 수 있습니다.
</aside>