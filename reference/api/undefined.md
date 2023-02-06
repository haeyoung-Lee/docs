# 로그인

## 소셜 로그인

플랫폼 별 소셜 로그인 시 파라미터로 입력할 인증코드를 획득하는 방법은 다음과 같습니다.

{% tabs %}
{% tab title="카카오" %}
1. 하단의 주소에 접속해 카카오 로그인을 진행합니다.
   * Kakao(배포용): `https://kauth.kakao.com/oauth/authorize?client_id=257ddabd02ec0d494551a5af563b1c9f&redirect_uri=https://peppy-bonbonea3a7a.netlify.app/oauth&response_type=code`
2. 획득한 OAuth 인증코드를 요청 파라미터로 입력합니다.
{% endtab %}

{% tab title="네이버" %}
1. 하단의 주소에 접속해 네이버 로그인을 진행합니다.
   * Naver(배포용): `https://nid.naver.com/oauth2.0/authorize?response_type=code&client_id=g_LUAeAaNdoi3o5xfqWB&redirect_uri=https://peppybonbon-ea3a7a.netlify.app/oauth&state=%ec%97%90%ec%bd%94%ec%97%90%ec%bd%94`
2.  획득한 code값과 state값을 요청 파라미터로 입력합니다.

    <figure><img src="../../.gitbook/assets/스크린샷 2023-02-06 오후 10.03.31.png" alt=""><figcaption><p>code값과 state값</p></figcaption></figure>
{% endtab %}

{% tab title="구글" %}
1. 하단의 주소에 접속합니다.
   * Google(배포용): `https://accounts.google.com/o/oauth2/v2/auth? scope=https%3A//www.googleapis.com/auth/userinfo.profile https://www.googleapis.com/auth/userinfo.email&access_type=offline&include_granted_scopes=true&response_type=code&state=state_parameter_passthrough_value&redire ct_uri=https://peppy-bonbon-ea3a7a.netlify.app/oauth&client_id=476852619689-daci8ob3qd5jppn4u8eo79flnf8c0uf2.apps.googleusercontent.com`
2. 획득한 OAuth 인증코드를 요청 파라미터로 입력합니다.&#x20;
{% endtab %}
{% endtabs %}

### 카카오

{% swagger method="get" path="/api/oauth/kakaotoken?code={인증코드}" baseUrl="https://www.eco-log-backend.kro.kr" summary="카카오 소셜 로그인 API" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="인증코드" type="String" required="true" %}
획득한 OAuth 인증 코드
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="JWT 토큰" %}
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

### 네이버

{% swagger method="get" path="/api/oauth/navertoken?code={코드값}&state={state값}" baseUrl="https://www.eco-log-backend.kro.kr" summary="네이버 소셜 로그인 API" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="코드값" required="true" %}
인가코드

\


  \- 

`AJuAagNCaGkmdUVDdx`

 입력
{% endswagger-parameter %}

{% swagger-parameter in="path" name="state값" required="true" %}
`에코에코`

 입력
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="JWT 토큰" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

### 구글

{% swagger method="get" path="/api/oauth/googletoken?={인증코드}" baseUrl="https://www.eco-log-backend.kro.kr" summary="구글 소셜 로그인 API " %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="인증코드" required="true" %}
획득한 OAuth 인증 코드
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="JWT 토큰" %}
```javascript
{
    // Response
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

## 사용자 탈퇴

{% swagger method="delete" path=" /api/user" baseUrl="https://www.eco-log-backend.kro.kr" summary="사용자 탈퇴 API" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

##
