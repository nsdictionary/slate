# Callback transfer status

## 1. Set callback user
사전에 Sentbe에 Trnasfer 상태를 받을 callback url 정보를 등록해야 합니다.

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

## 3. Transfer status

- <code>Waiting verification</code>
- <code>Processing</code>
- <code>AML filtered</code>
- <code>Complete</code>
- <code>Canceled</code>
- <code>Expired</code>
- <code>Refunded</code> <code>secret_key</code>
