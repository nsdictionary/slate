## create mobile verification

모바일 인증을 위해 가입된 휴대폰 번호로 인증번호를 발송합니다.

### endpoint
<code>POST: /outbound/verifications/mobile</code><br/>

### request
Parameter | Requried | Description
--------- | ------- | -----------
user_id |O| 센트비 유저 고유 id

> request parameter JSON structured like this:

```json
{
  "user_id": "15"
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













