# 시작하기

Ecolog API를 호출하기에 앞서 아래의 작업이 필요합니다.&#x20;

## 실천 항목 등록하기

1. h2 콘솔화면에 접속하여 실천 항목을 입력합니다.

{% code overflow="wrap" %}
```sql
INSERT INTO BEHAVIORS (NAME)
VALUES
('친환경 상점 이용'),('소비 없는 하루'),('중고거래'),('장바구니 사용'),('기부와 나눔'),
```
{% endcode %}

2. 하단의 API를 실행합니다.

{% code overflow="wrap" %}
```
https://accounts.google.com/o/oauth2/v2/auth?
```
{% endcode %}

{% code overflow="wrap" %}
```
https://nid.naver.com/oauth2.0/authorize?
```
{% endcode %}



{% hint style="info" %}
소셜 로그인 API에서 획득한 JWT 토큰은 로그인 제외 모든 API의 요청 헤더에 입력하시기 바랍니다.
{% endhint %}