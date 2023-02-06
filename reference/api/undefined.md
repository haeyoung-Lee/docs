# 로그인

## 소셜 로그인(카카오)

1. 하단의 주소에 접속해 Kakao 로그인을 진행합니다.

| 항목    | URL                                                                                                                                                                                                                                                                                                        |
| ----- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Kakao | [https://kauth.kakao.com/oauth/authorize?client\_id=257ddabd02ec0d494551a5af563b1c9f\&redirect\_uri=http://localhost:3000/oauth\&response\_type=code](https://kauth.kakao.com/oauth/authorize?client\_id=257ddabd02ec0d494551a5af563b1c9f\&redirect\_uri=http://localhost:3000/oauth\&response\_type=code) |

2\. 획득한 OAuth 인증코드를 엔드포인트에 요청 파라미터로 입력합니다.

{% swagger method="get" path="/api/oauth/kakaotoken?code={인증코드}" baseUrl="https://www.eco-log-backend.kro.kr" summary="카카오 소셜 로그인 API" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="인증코드" type="String" required="true" %}
획득한 OAuth 인증 코드
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
복호화는 [JSON Web Tokens](https://jwt.io/) 사이트 참고하여 진행합니다.

```json
{
	"Authorization": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.
			eyJzdWIiOiJ2dzk4MDFAbmF2ZXIuY29tIiwibmlja25hbWUiOiLsnpDsl7DsuZztmZTsoIHsnbgg7Zmc64-Z6rCAIiwiaWQiOjEsImV4cCI6MTY2NDY5NjA5M30.
			2p8fvCjl4yD_rNNEb6sEeKhafTKsBEs7Y0eH7UZSS8ZJYK-lLoypX5jo72WD9F2-uVLLT0icMIAuV59ivcSTA"
}
```
{% endswagger-response %}
{% endswagger %}

## 로그인 중인 사용자 조회

{% swagger method="get" path="/api/me" baseUrl="https://www.eco-log-backend.kro.kr" summary="현재 서비스에 로그인한 사용자를 조회하는 API" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="key" type="String" required="true" %}
Authorization으로 고정
{% endswagger-parameter %}

{% swagger-parameter in="header" name="value" type="String" required="true" %}
로그인 시 획득한 JWT 토큰

\


\- ex. 

`Bearer {토큰}`
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
{% tabs %}
{% tab title="Schema" %}
| 항목       | 타입      | 설명                    |
| -------- | ------- | --------------------- |
| userId   | Integer | 시스템 상에서의 구분을 위한 유저 ID |
| nickName | String  | 유저 닉네임                |
| email    | String  | 유저 가입 이메일             |
{% endtab %}
{% endtabs %}

```json
{
	"userId": 1,
	"nickName": "앞서가는 활동가",
	"email": "mailaddress@naver.com"
}
```
{% endswagger-response %}
{% endswagger %}

##

##

{% swagger src="https://petstore.swagger.io/v2/swagger.json" path="/pet" method="put" %}
[https://petstore.swagger.io/v2/swagger.json](https://petstore.swagger.io/v2/swagger.json)
{% endswagger %}

{% hint style="info" %}
**Good to know:** This API method was auto-generated from an example Swagger file. You'll see that it's not editable – that's because the contents are synced to a URL! Any time the linked file changes, the documentation will change too.
{% endhint %}
