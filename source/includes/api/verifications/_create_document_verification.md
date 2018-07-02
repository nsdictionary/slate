## create document verification

신분증 인증 을 위한 유저의 신분증 사진을 등록합니다. __(파라미터 암호화 X)__

### endpoint
<code>POST: /outbound/verifications/document</code><br/>

### request
Parameter | Requried | Description
--------- | ------- | -----------
user_id |O| 센트비 유저 고유 id
document_type |O| **korean_registration**</br> **korean_driver_license**</br> **alien_registration**</br> **passport**
document |O| 신분증 사진 파일 **(multipart/form-data)**

> request parameter JSON structured like this:

```json
{
  "user_id": "15",
  "document_type": "korean_registration",
  "document": 
}
```

### response
Parameter | Description
--------- | -----------
result | 요청 정보에 대한 결과(true/false)
data['id'] | 신분증 사진에 대한 고유 id


> response JSON structured like this:

```json
{
  "result" : true,
  "data" : {
    "id: "10"
  }
}
```

<aside class="warning">
신분증 사진 등록 api는 파라미터를 암호화 하지않고 요청해야 합니다.
</aside>