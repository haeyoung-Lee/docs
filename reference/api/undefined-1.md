# 프로필

## 프로필 조회

{% swagger method="get" path="/api/user/profile?target={targetId}" baseUrl="https://www.eco-log-backend.kro.kr" summary="실천 현황 화면 조회 시 필요한 정보를 불러오는 API" %}
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

{% swagger-parameter in="path" name="targetId" type="String" required="true" %}
프로필을 조회하려는 유저 ID
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
{% tabs %}
{% tab title="Schema" %}
| 항목                         | 타입      | 설명                                                                                                        |
| -------------------------- | ------- | --------------------------------------------------------------------------------------------------------- |
| userId                     | Integer | 유저 ID                                                                                                     |
| userNickName               | String  | 유저 닉네임                                                                                                    |
| userPostTotalCount         | String  | 유저가 작성한 총 게시물 개수                                                                                          |
| selfIntroduce              | String  | 유저가 작성한 자기소개                                                                                              |
| userSummary                | List    | 유저 실천 정보 요약                                                                                               |
|    behaviorId              | Integer | 실천 ID                                                                                                     |
|    name                    | String  | 실천 이름                                                                                                     |
|    count                   | Integer | 실천 횟수                                                                                                     |
| recentlyCustomBehaviorList | List    | 타 유저 프로필 시 조회하는 최근 직접 입력 실천 3가지                                                                           |
| createAt                   | String  | 유저 계정 생성일자                                                                                                |
| behaviorCount              | Integer | <p>전체 게시물에 입력 총 실천 개수<br>- 기본 실천 + 직접 입력 포함</p>                                                           |
| public                     | Boolean | <p>프로필 공개 설정 여부<br>- <code>true</code>: 공개<br>- <code>false</code>: 비공개</p>                               |
| myProfile                  | Boolean | <p>조회 중인 프로필의 본인 것 여부<br>- <code>true</code>: 본인 프로필<br>- <code>false</code>: 타 유저 프로필</p>                |
| alreadyFollow              | Boolean | <p>조회 중인 (타 유저) 프로필의 팔로우 여부<br>- <code>true</code>: 데이터 조회 시점 팔로우 중<br>- <code>false</code>: 팔로우하지 않음</p> |



**Sample Code. 본인 프로필 조회**

```json
{
	"userId": 1,
	"userNickName": "선행하는 활동가",
	"userPostTotalCount": 2,
	"selfIntroduce": "간단한 자기소개글을 적어주세요!",
	"userSummary": [
		{
			"behaviorId": 1,
			"name": "친환경 상점 이용",
			"count": 2
		},
		{
			"behaviorId": 21,
			"name": "평소 목욕시간의 절반 달성",
			"count": 2
		},
		],
	"recentlyCustomBehaviorList": [
			"물티슈 아닌 행주 쓰기",
			"평소보다 샴푸 덜 쓰기",
			"대중 교통 대신 자전거 타기"
	],
	"createAt": "2022-11-11",
	"behaviorCount": 6,
	"pubilc": true,
	"myprofile": true,
	"alreaydFollow": false
}
```



**Sample Code. 팔로우 하지 않은 타 유저 프로필 조회**

```json
{
	"userId": 1,
	"userNickName": "선행하는 활동가",
	"userPostTotalCount": 2,
	"selfIntroduce": "간단한 자기소개글을 적어주세요!",
	"userSummary": [
		{
			"behaviorId": 1,
			"name": "친환경 상점 이용",
			"count": 2
		},
		{
			"behaviorId": 21,
			"name": "평소 목욕시간의 절반 달성",
			"count": 2
		}, //...
		],
	"recentlyCustomBehaviorList": [
		"물티슈 아닌 행주 쓰기",
		"평소보다 샴푸 덜 쓰기",
		"대중 교통 대신 자전거 타기"
	],
	"createAt": "2022-11-11",
	"behaviorCount": 6,
	"pubilc": true,
	"myprofile": false,
	"alreaydFollow": false
}
```



**Sample Code. 생성 직후 초기 상태의 프로필 조회**

```json
{
	"userId": 1,
	"userNickName": "지구방위본부 사령관",
	"userPostTotalCount": 0,
	"selfIntroduce": "안녕하세요!",
	"userSummary": [],
	"recentlyCustomBehaviorList": [],
	"createAt": "2022-11-11",
	"behaviorCount": 0,
	"pubilc": false,
	"myprofile": true,
	"alreaydFollow": false
}
```
{% endtab %}
{% endtabs %}
{% endswagger-response %}
{% endswagger %}

## 프로필 수정

{% swagger method="post" path="/api/user/profile" baseUrl="https://www.eco-log-backend.kro.kr" summary="유저의 프로필 정보를 수정할 수 있는 API" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="key	" type="String" required="true" %}
Authorization
{% endswagger-parameter %}

{% swagger-parameter in="header" name="value" type="String" required="true" %}
로그인 시 JWT

\


\- ex. 

`Bearer {토큰}`
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
{% tabs %}
{% tab title="Schema" %}
| 항목         | 타입      | 설명    |
| ---------- | ------- | ----- |
| behaviorId | Integer | 실천 ID |
| name       | String  | 실천 이름 |
| count      | Integer | 실천 횟수 |
{% endtab %}
{% endtabs %}

```javascript
[
	{
		"behaviorId" : 1,
		"name": "친환경 상점 이용",
		"count": 3
	},
	{
		"behaviorId" : 2,
		"name": "소비 없는 하루",
		"count": 3
	},
	{
		"behaviorId" : 3,
		"name": "중고거래",
		"count": 3
	},
	... // 전체 실천 List
]
```
{% endswagger-response %}
{% endswagger %}

## 유저 실천 정보 요약 조회

{% swagger method="get" path="/api/user/summary" baseUrl="https://www.eco-log-backend.kro.kr" summary="프로필 조회 API의 응답 필드 중 userSummary를 따로 조회할 수 있는 API" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="key	" type="String" required="true" %}
Authorization
{% endswagger-parameter %}

{% swagger-parameter in="header" name="value" type="String" required="true" %}
로그인 시 JWT

\


\- ex. 

`Bearer {토큰}`
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
{% tabs %}
{% tab title="Schema" %}
| 항목         | 타입      | 설명    |
| ---------- | ------- | ----- |
| behaviorId | Integer | 실천 ID |
| name       | String  | 실천 이름 |
| count      | Integer | 실천 횟수 |
{% endtab %}
{% endtabs %}

```javascript
[
	{
		"behaviorId" : 1,
		"name": "친환경 상점 이용",
		"count": 3
	},
	{
		"behaviorId" : 2,
		"name": "소비 없는 하루",
		"count": 3
	},
	{
		"behaviorId" : 3,
		"name": "중고거래",
		"count": 3
	},
	... // 전체 실천 List
]
```
{% endswagger-response %}
{% endswagger %}

## 유저 검색

{% swagger method="get" path="/api/user/search?keyword={keyword}" baseUrl="https://www.eco-log-backend.kro.kr" summary="유저의 프로필 정보를 수정할 수 있는 API" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="key	" type="String" required="true" %}
Authorization
{% endswagger-parameter %}

{% swagger-parameter in="header" name="value" type="String" required="true" %}
로그인 시 JWT

\


\- ex. 

`Bearer {토큰}`
{% endswagger-parameter %}

{% swagger-parameter in="path" name="keyword" type="String" required="true" %}
검색할 유저 닉네임 또는 이메일
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
{% tabs %}
{% tab title="Schema" %}
| 항목            | 타입      | 설명                                                                                                            |
| ------------- | ------- | ------------------------------------------------------------------------------------------------------------- |
| userId        | Integer | 유저 ID                                                                                                         |
| nickName      | String  | 유저 닉네임                                                                                                        |
| selfIntroduce | String  | 유저가 작성한 자기소개                                                                                                  |
| userSummary   | List    | 유저 실천 정보 요약                                                                                                   |
|    behaviorId | Integer | 실천 ID                                                                                                         |
|    name       | String  | 실천 이름                                                                                                         |
|    count      | Integer | 실천 횟수                                                                                                         |
| alreadyFollow | Boolean | <p>조회 중인 (타 유저) 프로필의 팔로우 여부<br>  - <code>true</code>: 데이터 조회 시점 팔로우 중<br>  - <code>false</code>: 팔로우하지 않음</p> |
{% endtab %}
{% endtabs %}
{% endswagger-response %}
{% endswagger %}

