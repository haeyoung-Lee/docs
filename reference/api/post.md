# 게시물

## 게시물 저장 <a href="#save" id="save"></a>

{% swagger method="post" path="/api/post" baseUrl="https://www.eco-log-backend.kro.kr" summary="사용자가 작성한 게시물을 저장하는 API" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="comment	" type="String" required="true" %}
유저가 입력한 오늘의 한마디 (소감)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="doingDay" type="String" required="true" %}
게시물을 저장한 일자
{% endswagger-parameter %}

{% swagger-parameter in="header" name="key" type="String" required="true" %}
Authorization
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customizedBehaviors" type="List" required="true" %}
사용자가 직접 입력한 실천
{% endswagger-parameter %}

{% swagger-parameter in="header" name="value" type="String" required="true" %}
로그인 시 JWT

\


  \- ex. 

`Bearer {토큰}`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="behaviorList" type="List" required="true" %}
사용자가 선택한 실천 ID
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
{% tabs %}
{% tab title="Schema" %}
| 항목               | 타입      | 설명                                                                                                                                                                                                                                                                                                                                                            |
| ---------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| PostId           | Integer | 저장된 게시물의 ID                                                                                                                                                                                                                                                                                                                                                   |
| badgeAchieveList | List    | <p>게시물 발행 시점 유저가 획득한 뱃지 정보<br>  - 각 뱃지를 번호로 맵핑함<br>  - <code>0</code>: 작심삼일이 모이면<br>  - <code>1</code>: 꾸준함의 재능<br>  - <code>2</code>: 왕발자국<br>  - <code>3</code>: 실천가<br>  - <code>4</code>: 제로웨이스트 고수<br>  - <code>5</code>: 나만의 실천<br>  - <code>6</code>: 웰컴 백<br>  - <code>7</code>: 함께 갈 동료<br>  - <code>8</code>: 작은 마음<br>  - <code>9</code>: 치어 업</p> |

****

**Sample code. 게시물 저장 성공한 경우**

```json
{
	"postId": 2,
	"badgeAchieveList": [
		5
	]
}
```
{% endtab %}
{% endtabs %}
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="해당 일자에 이미 발행한 게시물이 존재" %}
```json
{
	"message": "해당 날짜에 이미 게시물이 있습니다."
}
```
{% endswagger-response %}
{% endswagger %}

## 게시물 수정 <a href="#edit" id="edit"></a>

{% swagger method="put" path="/api/post/change" baseUrl="https://www.eco-log-backend.kro.kr" summary="게시물을 수정할 수 있는 API" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="postId	" type="Integer" required="true" %}
수정하려는 게시물 ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="comment" type="String" required="true" %}
수정한 유저 닉네임
{% endswagger-parameter %}

{% swagger-parameter in="header" name="key" type="String" required="true" %}
Authorization
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customizedBehaviors" type="List" required="true" %}
사용자가 직접 입력한 실천
{% endswagger-parameter %}

{% swagger-parameter in="header" name="value" type="String" required="true" %}
로그인 시 JWT

\


  \- ex. 

`Bearer {토큰}`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="behaviorList" type="List" required="true" %}
사용자가 선택한 실천 ID
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="수정된 게시물의 ID" %}

{% endswagger-response %}
{% endswagger %}

## 게시물 삭제 <a href="#delete" id="delete"></a>

{% swagger method="delete" path="/api/post" baseUrl="https://www.eco-log-backend.kro.kr" summary="게시물을 삭제할 수 있는 API" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="postId	" type="Integer" required="true" %}
삭제하려는 게시물 ID
{% endswagger-parameter %}

{% swagger-parameter in="header" name="key" type="String" required="true" %}
Authorization
{% endswagger-parameter %}

{% swagger-parameter in="header" name="value" type="String" required="true" %}
로그인 시 JWT

\


  \- ex. 

`Bearer {토큰}`
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="삭제한 게시물의 ID" %}

{% endswagger-response %}
{% endswagger %}

## 피드 조회 <a href="#feed" id="feed"></a>

{% swagger method="get" path="/api/post/daily?={day}" baseUrl="https://www.eco-log-backend.kro.kr" summary="특정 일자에 저장된 유저 및 팔로워의 일간 게시물을 조회할 수 있는 API" %}
{% swagger-description %}
특정 일자에 저장된 유저 및 팔로워의 일간 게시물(피드)을 조회할 수 있는 API
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

{% swagger-parameter in="path" name="day" type="String" required="true" %}
조회하려는 일자
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
{% tabs %}
{% tab title="Schema" %}
| 항목                   | 타입      | 설명                                                                                                       |
| -------------------- | ------- | -------------------------------------------------------------------------------------------------------- |
| postId               | Integer | 조회하려는 게시물 ID                                                                                             |
| userInfo             | String  | 게시물을 작성한 유저 정보                                                                                           |
|    userId            | Integer | 유저 ID                                                                                                    |
|    userNickname      | String  | 유저 닉네임                                                                                                   |
|    selfIntroduce     | String  | 유저 자기소개                                                                                                  |
| customerBehaviorList | List    | 유저가 직접 입력한 실천                                                                                            |
| behaviorList         | List    | 유저가 선택한 실천                                                                                               |
| comment              | String  | 오늘의 한마디                                                                                                  |
| heartCount           | Integer | 해당 게시물의 좋아요 개수                                                                                           |
| alreadyHeart         | Boolean | <p>게시물을 조회하는 사용자가 좋아요를 눌렀는지 여부<br>  - <code>true</code>: 좋아요 활성화<br>  - <code>false</code>: 좋아요 비활성화</p> |
{% endtab %}
{% endtabs %}

```
{
	"postId": 4,
	"userInfo": {
		"userId": 2,
		"userNickname": "앞서가는 활동가",
		"selfIntroduce": "간단한 자기소개글을 적어주세요."
	},
	"customerBehaviorList": [
		"customized 친환경 상점 이용",
		"customized 소비 없는 하루",
		"customized 중고 거래"
	],
	"behaviorList": [
		"친환경 상점 이용",
		"기부와 나눔",
		"손수건 사용"
		"생분해 제품 사용"
	],
	"comment": "한번 팔로우 해보겠습니다.",
	"heartCount": 0,
	"alreadyHeart": false
},
{
	... // 이하 생략
}
```
{% endswagger-response %}
{% endswagger %}

## 게시물 월 단위 조회 <a href="#monthly" id="monthly"></a>

{% swagger method="get" path="/api/post/Monthly?month={month}" baseUrl="https://www.eco-log-backend.kro.kr" summary="피드 캘린더에 기록 표시바 마킹을 위해 월 단위 게시물을 조회할 수 있는 API" %}
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

{% swagger-parameter in="path" name="month" type="String" required="true" %}
조회하려는 월

\


  \- 

`yyyy-mm`

 형식으로 입력
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="해당월에 작성된 게시글의 일자" %}
```
[
	"2022-08-26",
	"2022-08-27",
	"2022-08-30"
]
```
{% endswagger-response %}
{% endswagger %}
