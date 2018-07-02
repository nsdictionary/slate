## verify mobile

휴대폰으로 발송된 인증번호를 통해 모바일 인증을 시도합니다.

### endpoint
<code>POST: /outbound/verifications/mobile/verify</code><br/>

### request
Parameter | Requried | Description
--------- | ------- | -----------
user_id |O| 센트비 유저 고유 id
token |O| 문자로 받은 인증번호 4자리
token_type |X| <a href="#register_user">유저 등록 api</a>를 통한 인증일 경우 'external' 로 세팅
external_id |X| <a href="#register_user">유저 등록 api</a>를 통한 인증일 경우 해당 유저의 파트너사 고유 id

> request parameter JSON structured like this:

```json
{
  "user_id": "15",
  "token": "8932"
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
5번이상 실패하거나, 인증번호 발송 3분이 지나면 인증을 할 수 없습니다.
</aside>