# 팔로우

## 유저 팔로우 <a href="#add" id="add"></a>

{% swagger method="post" path="/api/user/follow" baseUrl="https://www.eco-log-backend.kro.kr" summary="유저를 팔로우할 수 있는 API" %}
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

{% swagger-parameter in="body" name="targetId	" type="String" required="true" %}
팔로우하려는 유저 ID
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
{% tabs %}
{% tab title="Schema" %}
| 항목               | 타입     | 설명                                                        |
| ---------------- | ------ | --------------------------------------------------------- |
| message          | String | 요청 결과                                                     |
| badgeAchieveList | List   | <p>팔로우 시점에 유저가 획득한 뱃지 정보<br>- <code>7</code>: 함께 갈 동료</p> |
{% endtab %}
{% endtabs %}

```
{
	"message": "Follow{fromUser=2, toUser=1팔로우 관계를 시작합니다)",
	"badgeAchieveList": [
		7
	]
}

```
{% endswagger-response %}
{% endswagger %}

## 팔로우 취소 <a href="#unfollow" id="unfollow"></a>

{% swagger method="delete" path="/api/user/follow" baseUrl="https://www.eco-log-backend.kro.kr" summary="유저 팔로우를 취소할 수 있는 API" %}
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

{% swagger-parameter in="body" name="target" type="Integer" required="true" %}
팔로우를 취소할 유저 ID
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="팔로우 취소 완료" %}

{% endswagger-response %}
{% endswagger %}

## 팔로워 조회 <a href="#follower" id="follower"></a>

{% swagger method="get" path="/api/user/follower" baseUrl="https://www.eco-log-backend.kro.kr" summary="유저의 팔로워를 조회할 수 있는 API" %}
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

{% swagger-response status="200: OK" description="팔로우 취소 완료" %}
{% tabs %}
{% tab title="Schema" %}
| 항목            | 타입      | 설명       |
| ------------- | ------- | -------- |
| userId        | Integer | 팔로워 ID   |
| userNickName  | String  | 팔로워 닉네임  |
| selfIntroduce | String  | 팔로워 자기소개 |
{% endtab %}
{% endtabs %}
{% endswagger-response %}
{% endswagger %}

## 팔로잉 조회 <a href="#following" id="following"></a>

{% swagger method="get" path="/api/user/following" baseUrl="https://www.eco-log-backend.kro.kr" summary="유저를 팔로우하는 타 유저를 조회할 수 있는 API" %}
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

{% swagger-response status="200: OK" description="팔로우 취소 완료" %}
{% tabs %}
{% tab title="Schema" %}
| 항목            | 타입      | 설명          |
| ------------- | ------- | ----------- |
| userId        | Integer | 팔로잉 유저 ID   |
| userNickName  | String  | 팔로잉 유저 닉네임  |
| selfIntroduce | String  | 팔로잉 유저 자기소개 |
{% endtab %}
{% endtabs %}

```
[
 {
	 "userId": 2,
	 "nickName"": "활기찬 활동가",
	 "selfIntroduce": "간단한 자기소개글을 적어주세요!"
 }
]
```
{% endswagger-response %}
{% endswagger %}

## 팔로워 삭제 <a href="#view" id="view"></a>

{% swagger method="delete" path="/api/user/follower" baseUrl="https://www.eco-log-backend.kro.kr" summary="유저의 팔로워를 삭제하는 API" %}
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

{% swagger-parameter in="body" name="targetId" type="String" required="true" %}
삭제할 팔로워의 유저 ID
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="팔로워 삭제 완료" %}
{% tabs %}
{% tab title="Schema" %}
| 항목            | 타입      | 설명          |
| ------------- | ------- | ----------- |
| userId        | Integer | 팔로잉 유저 ID   |
| userNickName  | String  | 팔로잉 유저 닉네임  |
| selfIntroduce | String  | 팔로잉 유저 자기소개 |
{% endtab %}
{% endtabs %}

```
[
 {
	 "userId": 2,
	 "nickName"": "활기찬 활동가",
	 "selfIntroduce": "간단한 자기소개글을 적어주세요!"
 }
]
```
{% endswagger-response %}
{% endswagger %}

