### [☕️ 커피 사주기](https://toss.im/_m/ZLAYjZ2q)

# 토스 송금 링크 만들기 가이드

|parameter|설명|
|----|----|
|`apiKey`|발급받은 api key|
|`bankName`|은행명(한글)|
|`bankAccountNo`|입금 받을 계좌번호|
|`amount`|(선택) 입금 받을 금액|
|`message`|(선택) 입금시 전달할 메시지|

`POST`로 요청됨.

|result|설명|
|----|----|
|`type`|`SUCCESS` or `FAIL`|
|`success`|`link` 입금 링크. toss 앱이 없는 경우 market 이동<br> `scheme` 앱을 바로 실행하는 App Scheme|
|`fail`|실패 사유|

## 생성하는 순서

1. `apiKey` 만들기
    [https://toss.im/transfer-web/linkgen/request-apikey](https://toss.im/transfer-web/linkgen/request-apikey)에 접속해서 API Key 발급
1. 송금 받을 API Key, 은행명, 계좌번호, 금액, 메시지를 아래 코드의 `values`에 넣어 `python2`로 실행하기
    ```python
    #-*- coding: utf-8 -*-

    from urllib2 import Request, urlopen

    values = """
      {
        "apiKey": "",
        "bankName": "",
        "bankAccountNo": "",
        "amount": 1000,
        "message": ""
      }
    """

    headers = {
      'Content-Type': 'application/json'
    }
    request = Request('https://toss.im/transfer-web/linkgen-api/link', data=values, headers=headers)

    print request

    response_body = urlopen(request).read()
    print response_body
    ```
1. 반환되는 값에서 `link` 값이 송금 링크.
