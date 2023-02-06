# 게시물 하트

## 하트 활성화

{% swagger method="post" path="/api/post/heart" baseUrl="https://www.eco-log-backend.kro.kr" summary="게시물에 좋아요를 누를 수 있는 API" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="key" type="String" required="true" %}
Authorization
{% endswagger-parameter %}

{% swagger-parameter in="header" name="value" type="String" required="true" %}
로그인 시 JWT

\


  \- ex. 

`Bearer {토큰}`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="targetPostId" type="Integer" required="true" %}
좋아요를 선택하려는 게시물 ID
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="요청 결과" %}

{% endswagger-response %}
{% endswagger %}

## 하트 비활성화

{% swagger method="delete" path="/api/post/heart" baseUrl="https://www.eco-log-backend.kro.kr" summary="게시물에 눌렀던 좋아요를 취소하는 API" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="key" type="String" required="true" %}
Authorization
{% endswagger-parameter %}

{% swagger-parameter in="header" name="value" type="String" required="true" %}
로그인 시 JWT

\


  \- ex. 

`Bearer {토큰}`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="targetPostId" type="Integer" %}
좋아요를 취소할 게시물 ID
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="요청 결과" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}
