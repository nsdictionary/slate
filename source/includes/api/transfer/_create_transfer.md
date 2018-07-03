## create transfer

송금을 신청하고 송금을 진행하니다.

### endpoint
<code>POST: /outbound/transfers</code>

### request
Parameter | Requried | Description
--------- | ------- | -----------
user_id |O| 센트비 유저 고유 id
recipient_id |O| 센트비 수취인 고유 id
recieve_amount |O| 수취 금액
recieve_amount_currency |O| 수취 통화 (KRW 제외)
exchange_rate_list_id |O| <a href="#check-commission">check_commssion</a>에서 받은 환율값 고유 id
external_id |O| 파트너사 거래정보 고유 id

> request parameter JSON structured like this:

```json
{
  "user_id": "15",
  "recipient_id": "53",
  "recieve_amount": "4000",
  "recieve_amount_currency": "PHP",
  "exchange_rate_list_id": "1",
  "external_id": "2"
}
```

### response
<a href="#check-transfer-status">거래 신청 정보 조회</a>의 response와 동일

<aside class="warning">
<a href="#check-commission">송금 금액 조회 api</a>에서 response로 받은 exchange_rate_list_id request 파라미터로 동일하게 보내야 합니다.
다른 값을보내면 신청이 안되거나, 금액에 차이가 생길 수 있습니다.
</aside>

<aside class="notice">
reqeust 파리미터중 recieve_amount 는 integer포맷 으로 세팅해야 합니다.
</aside>

<aside class="notice">
response의 transfer_id는 추후 거래정보 조회 등을 요청할때 사용되므로 파트너사의 DB에 저장해 두는게 좋습니다.
</aside>

