## cancel trasnfer

신청한 거래를 취소합니다.

### endpoint
<code>POST: /outbound/transfers/cancel</code>

### request

Parameter | Requried | Description
--------- | ------- | -----------
transfer_id |O| 센트비 거래 고유 id

> request parameter JSON structured like this:

```json
{
  "transfer_id": "49"
}
```

### response
<a href="#check-transfer-status">거래 신청 정보 조회</a>의 response와 동일