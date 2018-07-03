# API Reference(others)

## get list data

파라미터 목록 데이터를 조회합니다.

### endpoint
<code>GET: /outbound/data_list/:list_type</code>

### request

Parameter | Requried | Description
--------- | ------- | -----------
list_type |O| often_send_country<br/> occupation</br> transfer_purpose</br> funds_source</br>

### response
Parameter | Description
--------- | -----------
result | 요청 정보에 대한 결과(true/false)
data | 요청한 타입의 데이터 목록

> response JSON structured like this:

```json
{
  "result": true,
  "data": [
    "factory_worker",
    "housewife_husband",
    "student",
    "enterpreneur",
    "company_employee",
    "none"
  ]
}
```