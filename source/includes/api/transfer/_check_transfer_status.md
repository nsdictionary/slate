## check transfer status

신청한 거래의 정보를 조회할 수 있습니다.

### endpoint
<code>GET: /outbound/transfers</code><br/>
<code>GET: /outbound/transfers/:transfer_id</code>
<code>GET: /outbound/transfers/user/:user_id</code>

### request
Parameter | Requried | Description
--------- | ------- | -----------
page |X| default: 1, offset: 5
transfer_id |X| 센트비 거래정보 고유 id
user_id |X| 센트비 유저 고유 id

> request parameter JSON structured like this:

```json
{
  "page": "2"
}
```

### response
Parameter | Description
--------- | -----------
result | 요청 정보에 대한 결과(true/false)
**data** | **거래 정보 hash**

### data
Parameter | Description
--------- | -----------
transfer_id | 센트비 거래 고유 id
user_id | 센트비 유저 고유 id
recipient_id | 수취인 고유 id
sender_country | 수취인 국적 국가코드 (ISO ALPHA-2 Code)
send_amount | 송금 금액 (가상계좌로 입금할 최종 금액)
send_amount_currency | 송금 통화 (KRW 고정)
receive_amount | 수취 금액
receive_amount_currency | 수취 통화
commission | 수수료
commission_currency | 수수료 통화 (KRW 고정)
status | **Transfer Requested**(입금대기중)<br/> **Processing**(송금 진행중)<br/> **AML filtered**(AML 필터링 대상)<br/> **Complete**(송금 완료)<br/> **Canceled**(취소됨)<br/> **Expired**(만료됨)<br/> **Refunded**(환불됨)
virtual_account | 입금 가상 계좌 정보
created_at | 거래 생성 일시

> response JSON structured like this:

```json
{
  "result": true,
  "data": {
    "transfer_id": 49,
    "user_id": 15,
    "recipient_id": 53,
    "sender_country": "KR",
    "send_amount": 96630.0,
    "send_amount_currency": "KRW",
    "receive_amount": 4000.0,
    "receive_amount_currency": "PHP",
    "commission": 5000.0,
    "commission_currency": "KRW",
    "status": "Transfer Requested",
    "virtual_account": "상호저축은행(Bank code 50) | 066-40-15-072113-4 | (주)센트비",
    "created_at": "2018-06-22T14:13:05.000+09:00"
  }
}
```
