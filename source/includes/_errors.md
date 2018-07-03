# Errors

<aside class="notice">
response의 result가 false일경우 에러코드와 함께 예외 상황 메시지가 출력됩니다.
</aside>

Sentbe outbound api에서는 아래와 같은 에러코드가 사용됩니다:

Error Code | Meaning
---------- | -------
E0000 | Global error (아래 정의되지 않은 여러가지 예와상황들)
E0001 | Authentication error -- (partner_id, ip 등)
E0002 | 잘못된 모델 id (user, recipient, transfer 등)
E0003 | 잘못된 파트너사 access_id
E0004 | 잘못된 포맷의 암호화된 reqeust body
E0005 | 유효하지 않는 request 파라미터 정보 
E0006 | 지원하지 않는 url format
E0009 | 유효하지 않은 거래 상태
E0011 | 유효하지 않은 국가 코드
E0012 | 지원하지 않는 은행 및 수취방법
E0013 | Invalid external id
E0101 | 파트너사에 등록되지 않은 유저일 경우
E0102 | 리스트에 없는 값을 사용했을 경우
E0103 | 주민식별번호 포맷 에러
E0104 | 이미 존재하는 모델이 있음
E0105 | 해당 모델이 존재하지 않음
E0106 | 이미 파트너사에 등록된 유저일 경우
E0107 | 동일한 유저가 이미 존재함
E0108 | 오픈플랫폼 접속 에러
E0109 | 유효하지 않은 external user 파라미터 정보
E0110 | 송금 금액 계산기 서버 접속 에러
E0111 | 유저정보 업데이트 필요
E0112 | 인증되지 않은 유저
E0113 | 동의 정보 부족 유저
E0114 | 이미 동의된 verification
E0115 | 거래 생성 실패


> error response parameter JSON structured like this:

```json
{
  "result": false,
  "errors": [
    {
      "message": "Invalid transfer id",
      "error_code": "E0002"
    }
  ]
}
```
