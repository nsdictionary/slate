# API Reference(transfer)

## check commission

송금금액으로 수취금액(KRW) 및 수수료를 조회 합니다.

### endpoint
<code>POST: /outbound/check_commission</code>

### request
Parameter | Requried | Description
--------- | ------- | -----------
user_id |O| 센트비 유저 고유 id
recipient_id |O| 센트비 수취인 고유 id
recieve_amount |O| 수취금액
recieve_amount_currency |O| 수취통화 (KRW 제외)

> request parameter JSON structured like this:

```json
{
  "user_id": "15",
  "recipient_id": "53",
  "recieve_amount": "5000",
  "recieve_amount_currency": "PHP"
}
```


### response
Parameter | Description
--------- | -----------
result | 요청 정보에 대한 결과(true/false)
**data** | **수취금액 정보 hash**

### data
Parameter | Description
--------- | -----------
send_amount | 송금금액 (가상계좌로 입금할 최종 금액)
send_amount_currency | 송금금액 통화 (KRW 고정)
receive_amount | 수취금액
receive_amount_currency | 수취금액 통화
commission | 수수료
commission_currency | 수수료 통화 (KRW 고정)
credit_usage_amount | 유저 크레딧 사용 내역
total_commission | 수수료 합계
exchange_rate_list_id | 환율값 고유 id

> response JSON structured like this:

```json
{
  "result": true,
  "data": {
    "send_amount": 119090,
    "send_amount_currency": "KRW",
    "receive_amount": 5000.0,
    "receive_amount_currency": "PHP",
    "commission": 5000,
    "commission_currency": "KRW",
    "credit_usage_amount": 0,
    "total_commission": 5000,
    "exchange_rate_list_id": 1
  }
}
```

<aside class="notice">
reqeust 파리미터중 recieve_amount 는 integer포맷 으로 세팅해야 합니다.
</aside>
