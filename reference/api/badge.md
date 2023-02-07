# 뱃지

## 뱃지 조회 <a href="#view" id="view"></a>

{% swagger method="get" path="/api/user/badge" baseUrl="https://www.eco-log-backend.kro.kr" summary="유저가 획득한 뱃지 현황을 조회하는 API" expanded="true" %}
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

{% swagger-response status="200: OK" description="" %}
{% tabs %}
{% tab title="Schema" %}
| 항목             | 타입      | 설명                                                                                                                                                                                                                                                                                                                                                  |
| -------------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| userId         | Integer | 유저 아이디                                                                                                                                                                                                                                                                                                                                              |
| badgeStateList | List    | <p>유저가 획득한 뱃지 정보<br>  - 각 뱃지를 번호로 맵핑함<br>  - <code>0</code>: 작심삼일이 모이면<br>  - <code>1</code>: 꾸준함의 재능<br>  - <code>2</code>: 왕발자국<br>  - <code>3</code>: 실천가<br>  - <code>4</code>: 제로웨이스트 고수<br>  - <code>5</code>: 나만의 실천<br>  - <code>6</code>: 웰컴 백<br>  - <code>7</code>: 함께 갈 동료<br>  - <code>8</code>: 작은 마음<br>  - <code>9</code>: 치어 업</p> |
{% endtab %}
{% endtabs %}

```javascript
{
	"userId": 2,
	"badgeStateList": [
		"0",
		"1",
		"5"
	]
}
```
{% endswagger-response %}
{% endswagger %}
