## register user

센트비에 이미 가입한 유저를 파트너사에서 관리할수 있도록 등록 할 수 있습니다.
유저의 휴대폰 번호로 인증번호가 발송되며 <a href="#verify-mobile">모바일 인증 api</a>를 통해 인증을 완료하면
등록을 완료 할수 있습니다.

### endpoint
<code>POST: /outbound/registrations/mobile</code>

### request

Parameter | Requried | Description
--------- | ------- | -----------
id |O| 센트비 유저 고유 id

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
