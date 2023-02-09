# 시작하기

Ecolog API를 호출하기에 앞서 아래의 작업이 필요합니다.&#x20;

## 실천 항목 등록하기

1. h2 콘솔화면에 접속하여 실천 항목을 입력합니다.

{% code overflow="wrap" %}
```sql
INSERT INTO BEHAVIORS (NAME)
VALUES
('친환경 상점 이용'),('소비 없는 하루'),('중고거래'),('장바구니 사용'),('기부와 나눔'),('대중교통 이용'),('20분 이하 거리 도보'),('텀블러 소지'),('손수건 사용'),('카페 머그잔사용'),('종이 또는 다회용 빨대 사용'),('빨대 미사용'),('밀랍 랩 사용'),('행주 사용'),('음식물 쓰래기 건조'),('천연 수세미 사용'),('분리수거'),('먹을만큼만 요리'),('비누 사용'),('생분해 제품 사용'),('평소 목욕시간의 절반 달성'),('양치컵 사용'),('한끼 채식'),('식물성 식품 식사'),('배달음식 자제'),('잔반 없음'),('냉난방적정 온도 유지'),('안쓰는 전자기기 플러그 제거'),('거리 쓰래기 수거')
```
{% endcode %}

2. 하단의 API를 실행합니다.

{% code overflow="wrap" %}
```
https://accounts.google.com/o/oauth2/v2/auth?scope=https%3A//www.googleapis.com/auth/userinfo.profilehttps://www.googleapis.com/auth/userinfo.email&access_type=offline&include_granted_scopes=true&response_type=code&state=state_parameter_passthrough_value&redirect_uri=http://localhost:3000/oauth&client_id=476852619689-daci8ob3qd5jppn4u8eo79flnf8c0uf2.apps.googleusercontent.com
```
{% endcode %}

{% code overflow="wrap" %}
```
https://nid.naver.com/oauth2.0/authorize?response_type=code&client_id=g_LUAeAaNdoi3o5xfqWB&redirect_uri=http://localhost:3000/oauth&state=%ec%97%90%ec%bd%94%ec%97%90%ec%bd%94
```
{% endcode %}



{% hint style="info" %}
소셜 로그인 API에서 획득한 JWT 토큰은 로그인 제외 모든 API의 요청 헤더에 입력하시기 바랍니다.
{% endhint %}
