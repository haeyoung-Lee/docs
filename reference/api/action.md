# 실천

## 실천 조회 <a href="#view" id="view"></a>

{% swagger method="post" path="/api/behavior" baseUrl="https://www.eco-log-backend.kro.kr" summary="전체 실천의 이름과 ID를 조회할 수 있는 API" %}
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
| 항목           | 타입      | 설명                                                                                                                |
| ------------ | ------- | ----------------------------------------------------------------------------------------------------------------- |
|              | Array   | <p>실천의 카테고리</p><ul><li>spend: 소비</li><li>outdoor: 외출</li><li>living: 생활</li><li>eat: 식사</li><li>etc: 기타</li></ul> |
|   behaviorId | Integer | 실천 ID                                                                                                             |
|   name       | String  | 실천 이름                                                                                                             |
{% endtab %}
{% endtabs %}

```json
{
	"spend": [
		{
			"behavior": 1,
			"name": "친환경 상점 이용"
		},
		{
			"behavior": 2,
			"name": "소비 없는 하루"
		},
		{
			"behavior": 3,
			"name": "중고 거래"
		},
		...
	],
	"outdoor": [
		{
			"behavior": 6,
			"name" "대중 교통 이용"
		}, 
		...
	],
	...
}
```
{% endswagger-response %}
{% endswagger %}
