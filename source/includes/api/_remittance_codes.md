# API Reference(recipient)

## remittance code info

송금 수단별 정보를 조회할 수 있습니다.

### endpoint
<code>GET: /inbound/remittance_codes/:method</code>
<code>GET: /inbound/remittance_codes/:method/:country</code>

### request
Parameter | Requried | Description
--------- | ------- | -----------
page |X| default: 1, offset: 5
method |O| **bank** <br> **pickup** <br> **debit_card** <br> **home_delivery** <br>
country |X| 수취국가 국가코드(ISO ALPHA-2 Code)

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
**data** | **수취방법 정보 list**

### data
Parameter | Description | Optional
--------- | ----------- | --------
label | 수취 국가 언어 label |X|
label_ko | 한국어 label |O|
label_en | 영어 label |O|
value | 수취방법 코드 |X|



> response parameter JSON structured like this:

```json
{
  "result": true,
  "data": [
    {
      "label": "中国银联",
      "label_ko": "중국은련",
      "label_en": "중국은련",
      "value": "100001"
    },...{}
  ]
}
```