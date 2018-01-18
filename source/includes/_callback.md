# Callback transfer status

## 1. Set callback user
사전에 Sentbe 서버에 Trnasfer 상태를 받을 callback url 정보를 등록해야 합니다.

<aside class="notice">
e.g. http://example.com/setnbe_callback
</aside>

## 2. Set callback receiver
Sentbe에서 보내는 Trasnsfer status 정보를 받을수 있도록 파트너사의 웹서버에 callback reqeust를 받을수 있게 작업을 해두어야 합니다. 센트비에서 발행하는 request 정보는 우측 json포맷과 같습니다.

### request
Parameter | Description
--------- | -----------
token | partner's access_id
external_id | partner's transer unique id
status | transfer status

> request parameter JSON structured like this:

```json
{
  "token": "partner_access_id",
  "external_id": "23",
  "status": "Waiting verification"
}
```

<aside class="notice">
보안상 필요하다면 token정보로 파트너사의 access_id와 대조해서 validation을 하는것도 좋습니다.
</aside>

<aside class="notice">
response는 http status code 200으로 하면 됩니다.
</aside>

## 3. Transfer status

- <code>Waiting verification</code>
: 수취인의 인증을 기다리는중
- <code>Processing</code>
: 은행에 송금 요청 진행중
- <code>AML filtered</code>
: AML 대상에 걸려서 검토중
- <code>Complete</code>
: 거래 완료
- <code>Canceled</code>
: 거래 취소됨
- <code>Expired</code>
: 시간 만료
- <code>Refunded</code>
: 환불 완료
