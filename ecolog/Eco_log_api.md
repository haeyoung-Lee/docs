# API 명세서

Eco-log 서비스의 API를 설명하는 문서입니다.

## API 퀵 레퍼런스

| 구분 | 메서드 | API  | 설명 |
| --- | --- | --- | --- |
| 로그인 | GET | [/api/oauth/kakaotoken](#소셜-로그인카카오) | 카카오 소셜 로그인 |
|  | GET | [/api/me](#로그인-중인-사용자-조회) | 현재 로그인 중인 유저 조회 |
| 프로필 | GET | [/api/user/profile](#프로필-조회) | 프로필(실천 현황) 조회 |
|  | POST | [/api/user/profile](#프로필-수정) | 프로필 수정 |
|  | GET | [/api/user/summary](#유저-실천-정보-조회) | 유저 실천 정보 요약 조회 |
|  | GET | [/api/user/search](#유저-검색) | 유저 검색 |
| 게시물 | POST | [/api/post](#게시물-저장) | 게시물 저장 |
|  | PUT | [/api/post/change](#게시물-수정) | 게시물 수정 |
|  | DELETE | [/api/post](#게시물-삭제) | 게시물 삭제 |
|  | GET | [/api/post/daily](#피드-조회) | 피드 조회 |
|  | GET | [/api/post/Monthly](#게시물-월-단위-조회) | 게시물 월 단위 조회 |
| 실천 | GET | [/api/behavior](#실천-조회) | 전체 실천 ID 및 이름 조회 |
| 팔로우 | POST | [/api/user/follow](#유저-팔로우) | 유저 팔로우 |
|  | DELETE | [/api/user/follow](#팔로우-취소) | 유저 팔로우 취소 |
|  | GET | [/api/user/follower](#팔로워-조회) | 팔로워 조회 |
|  | GET | [/api/user/following](#팔로잉-조회) | 팔로잉 조회 |
| 게시물 하트 | POST | [/api/post/heart](#하트-활성화) | 하트 활성화 |
|  | DELETE | [/api/post/heart](#하트-비활성화) | 하트 활성화 취소 |
| 뱃지 | GET | [/api/user/badge](#뱃지-조회) | 유저 뱃지 획득 정보 조회 |

# 로그인

## 소셜 로그인(카카오)

1. 하단의 주소에 접속해 Kakao 로그인을 진행합니다.

	| 항목 | URL |
	| --- | --- |
	| Kakao | `https://kauth.kakao.com/oauth/authorize?client_id=257ddabd02ec0d494551a5af563b1c9f&redirect_uri=http://localhost:3000/oauth&response_type=code` |

2. 획득한 OAuth 인증코드를 엔드포인트에 요청 파라미터로 입력합니다.

	| 메서드 | 엔드포인트 |
	| --- | --- |
	| GET | `/api/oauth/kakaotoken?code={인증코드}` |

### Request

**Path Parameter**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| 인증코드 | 필수 | String | 획득한 OAuth 인증 코드 |

### Response

**Respose Fields**

| 항목 | 타입 | 설명 |
| --- | --- | --- |
| Authorization | String | JWT 토큰 |

**Example Code**

복호화는 [JSON Web Tokens](https://jwt.io/) 사이트 참고하여 진행합니다.

```json
{
	"Authorization": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.
			eyJzdWIiOiJ2dzk4MDFAbmF2ZXIuY29tIiwibmlja25hbWUiOiLsnpDsl7DsuZztmZTsoIHsnbgg7Zmc64-Z6rCAIiwiaWQiOjEsImV4cCI6MTY2NDY5NjA5M30.
			2p8fvCjl4yD_rNNEb6sEeKhafTKsBEs7Y0eH7UZSS8ZJYK-lLoypX5jo72WD9F2-uVLLT0icMIAuV59ivcSTA"
}
```

- **Payload(참고)**

    #### Response fields

    JWT의 payload에 해당합니다.

    | 항목 | 필수 여부 | 타입 | 설명 |
    | --- | --- | --- | --- |
    | sub | 필수 | String | 유저 가입 이메일 |
    | nickname | 필수 | String | 유저 닉네임 |
    | id | 필수 | Integer | 시스템 상에서 구분을 위한 유저 아이디 |
    | exp | 필수 | Integer | 만료 기간 |


## 로그인 중인 사용자 조회

현재 서비스에 로그인한 사용자를 조회하는 API입니다.

| 메서드 | 엔드포인트 |
| --- | --- |
| GET | `/api/me` |

### Request

**Request Header**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| key | 필수 | String | Authorization으로 고정 |
| value | 필수 | String | 로그인 시 획득한 JWT 토큰 <br> - `ex. Bearer {토큰}` |

### Response

**Respose Fields**

| 항목 | 타입 | 설명 |
| --- | --- | --- |
| userId | Integer | 시스템 상에서의 구분을 위한 유저 ID |
| nickName | String | 유저 닉네임 |
| email | String | 유저 가입 이메일 |

**Sample Code**

```json
{
	"userId": 1,
	"nickName": "앞서가는 활동가",
	"email": "mailaddress@naver.com"
}
```

# 프로필

## 프로필 조회

실천 현황 화면 조회 시 필요한 정보를 불러오는 API입니다.

| 메서드 | 엔드포인트 |
| --- | --- |
| GET | `/api/user/profile?target={targetId}` |

### Request

**Path Parameters**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| targetId | 필수 | String | 프로필을 조회하려는 유저 ID |

**Request Header**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| key | 필수 | String | Authorization |
| value | 필수 | String | 로그인 시 JWT <br>  - `ex. Bearer {토큰}` |

### Response

**Response Fields**

| 항목 | 타입 | 설명 |
| --- | --- | --- |
| userId | Integer | 유저 ID |
| userNickName | String | 유저 닉네임 |
| userPostTotalCount | String | 유저가 작성한 총 게시물 개수 |
| selfIntroduce | String | 유저가 작성한 자기소개 |
| userSummary | List | 유저 실천 정보 요약 |
| &nbsp;&nbsp; behaviorId | Integer | 실천 ID |
| &nbsp;&nbsp; name | String | 실천 이름 |
| &nbsp;&nbsp; count | Integer | 실천 횟수 |
| recentlyCustomBehaviorList | List | 타 유저 프로필 시 조회하는 최근 직접 입력 실천 3가지 |
| createAt | String | 유저 계정 생성일자 |
| behaviorCount | Integer | 전체 게시물에 입력 총 실천 개수 <br> - 기본 실천 + 직접 입력 포함 |
| public | Boolean | 프로필 공개 설정 여부 <br>  - `true`: 공개 <br>  - `false`: 비공개 |
| myProfile | Boolean | 조회 중인 프로필의 본인 것 여부 <br>  - `true`: 본인 프로필 <br>  - `false`: 타 유저 프로필 |
| alreadyFollow | Boolean | 조회 중인 (타 유저) 프로필의 팔로우 여부 <br>  - `true`: 데이터 조회 시점 팔로우 중 <br>  - `false`: 팔로우하지 않음 |

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

## 프로필 수정

유저의 프로필 정보를 수정할 수 있는 API입니다.

| 메서드 | 엔드포인트 |
| --- | --- |
| POST | `/api/user/profile` |

### Request

**Request Header**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| key | 필수 | String | Authorization |
| value | 필수 | String | 로그인 시 JWT <br>  - `ex. Bearer {토큰}` |

**Request Body**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| nickName | 필수 | String | 수정한 유저 닉네임 |
| selfIntroduce | 필수 | String | 수정한 유저 자기소개 |
| isPublic | 필수 | Integer | 수정한 프로필 공개 여부값 <br>  - `1`: 공개 <br>  - `0`: 비공개 |

**Sample Code**

```json
{
	"nickName": "냠냠냠킴",
	"selfIntroduce": "자기소개 합니다.",
	"isPublic": 0
}
```

### Response

**Response Fields**

| 항목 | 타입 | 설명 |
| --- | --- | --- |
|  |  | 저장된 게시물의 ID |

## 유저 실천 정보 조회

프로필 조회 API의 응답 필드 중 userSummary를 따로 조회할 수 있는 API입니다.

| 메서드 | 엔드포인트 |
| --- | --- |
| GET | `/api/user/summary` |

### Request

**Request Header**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| key | 필수 | String | Authorization |
| value | 필수 | String | 로그인 시 JWT <br>  - `ex. Bearer {토큰}` |

### Response

**Response Fields**

실천 횟수 기준 내림차순으로 응답합니다.

| 항목 | 타입 | 설명 |
| --- | --- | --- |
| behaviorId | Integer | 실천 ID |
| name | String | 실천 이름 |
| count | Integer | 실천 횟수 |

**Sample Code**

```json
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

## 유저 검색

| 메서드 | 엔드포인트 |
| --- | --- |
| GET | `/api/user/search?keyword={keyword}` |

### Request

**Request Parameters**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| keyword | 필수 | String | 검색할 유저 닉네임 또는 이메일 |

**Request Header**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| key | 필수 | String | Authorization |
| value | 필수 | String | 로그인 시 JWT <br>  - `ex. Bearer {토큰}` |

### Response

**Response Fields**

실천 횟수 기준 내림차순으로 응답합니다.

| 항목 | 타입 | 설명 |
| --- | --- | --- |
| userId | Integer | 유저 ID |
| nickName | String | 유저 닉네임 |
| selfIntroduce | String | 유저가 작성한 자기소개 |
| userSummary | List | 유저 실천 정보 요약 |
| &nbsp;&nbsp; behaviorId | Integer | 실천 ID |
| &nbsp;&nbsp; name | String | 실천 이름 |
| &nbsp;&nbsp; count | Integer | 실천 횟수 |
| alreadyFollow | Boolean | 조회 중인 (타 유저) 프로필의 팔로우 여부 <br>  - `true`: 데이터 조회 시점 팔로우 중 <br>  - `false`: 팔로우하지 않음 |


# 게시물

## 게시물 저장

사용자가 작성한 게시물을 저장하는 API입니다. 특정 일자에 이미 발행한 게시물이 있을 경우, 400 에러 메시지를 반환합니다.

| 메서드 | 엔드포인트 |
| --- | --- |
| POST | `/api/post` |

### Request

**Request Header**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| key | 필수 | String | Authorization |
| value | 필수 | String | 로그인 시 JWT <br>  - `ex. Bearer {토큰}` |

**Request Body**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| comment | 필수 | String | 유저가 입력한 오늘의 한마디 (소감) |
| doingDay | 필수 | String | 게시물을 저장한 일자 |
| customizedBehaviors | 필수 | List | 사용자가 직접 입력한 실천 |
| behaviorList | 필수 | List | 사용자가 선택한 실천 ID  |

**Sample Code**

```json
{
	"comment": "오늘도 수고했어",
	"doingDay": "2022-05-16",
	"customizedBehaviors": ["customized 친환경 상점 이용"," customized소비 없는 하루","customized중고거래","customized 대중교통 이용"],
	"behaviorList": ["1", "2", "4"]
}
```

### Response

**Response Fields**

| 항목 | 타입 | 설명 |
| --- | --- | --- |
| PostId | Integer | 저장된 게시물의 ID |
| badgeAchieveList | List | 게시물 발행 시점 유저가 획득한 뱃지 정보<br>- 각 뱃지를 번호로 맵핑함<br>- `0`: 작심삼일이 모이면<br>- `1`: 꾸준함의 재능<br>- `2`: 왕발자국<br>- `3`: 실천가<br>- `4`: 제로웨이스트 고수<br>- `5`: 나만의 실천<br>- `6`: 웰컴 백<br>- `7`: 함께 갈 동료<br>- `8`: 작은 마음<br>- `9`: 치어 업 |

**Sample Code. 게시물 저장 성공한 경우**

```json
{
	"postId": 2,
	"badgeAchieveList": [
		5
	]
}
```

**Error Code. 게시물을 이미 발행한 경우**

```json
{
	"message": "해당 날짜에 이미 게시물이 있습니다."
}
```

## 게시물 수정

게시물을 수정할 수 있는 API입니다.

| 메서드 | 엔드포인트 |
| --- | --- |
| PUT | `/api/post/change` |

### Request

**Request Header**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| key | 필수 | String | Authorization |
| value | 필수 | String | 로그인 시 JWT <br>  - `ex. Bearer {토큰}` |

**Request Body**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| postId | 필수 | Integer | 수정하려는 게시물 ID |
| comment | 필수 | String | 수정한 유저 닉네임 |
| customizedBehaviors | 필수 | List | 사용자가 직접 입력한 실천 |
| behaviorList | 필수 | List | 사용자가 선택한 실천 ID  |

### Response

**Response Fields**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
|  | 필수 |  | 수정된 게시물의 ID |

## 게시물 삭제

게시물을 삭제할 수 있는 API입니다.

| 메서드 | 엔드포인트 |
| --- | --- |
| DELETE | `/api/post` |

### Request

**Request Header**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| key | 필수 | String | Authorization |
| value | 필수 | String | 로그인 시 JWT <br>  - `ex. Bearer {토큰}` |

**Request Body**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| postId | 필수 | String | 삭제하려는 게시물의 ID |

### Response

**Response Fields**

| 항목 | 타입 | 설명 |
| --- | --- | --- |
|  |  | 삭제된 게시물의 ID |

## 피드 조회

특정 일자에 저장된 유저 및 팔로워의 일간 게시물을 조회할 수 있는 API입니다.

| 메서드 | 엔드포인트 |
| --- | --- |
| GET | `/api/post/daily?={day}` |

### Request

**Path Parameters**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| day | 필수 | String | 조회하려는 일자 |

**Request Header**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| key | 필수 | String | Authorization |
| value | 필수 | String | 로그인 시 JWT <br>  - `ex. Bearer {토큰}` |

### Response

**Response Fields**

| 항목 | 타입 | 설명 |
| --- | --- | --- |
| postId | Integer | 조회하려는 게시물 ID |
| userInfo | String | 게시물을 작성한 유저 정보 |
| &nbsp;&nbsp; userId | Integer | 유저 ID |
| &nbsp;&nbsp; userNickname | String | 유저 닉네임 |
| &nbsp;&nbsp; selfIntroduce | String | 유저 자기소개 |
| customerBehaviorList | List | 유저가 직접 입력한 실천 |
| behaviorList | List | 유저가 선택한 실천 |
| comment | String | 오늘의 한마디 |
| heartCount | Integer | 해당 게시물의 좋아요 개수 |
| alreadyHeart | Boolean | 게시물을 조회하는 사용자가 좋아요를 눌렀는지 여부 <br>  - `true`: 좋아요 활성화 <br>  - `false`: 좋아요 비활성화 |

**Sample Code**

```json
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

## 게시물 월 단위 조회

피드 캘린더에 기록 표시바 마킹을 위해 월 단위 게시물을 조회할 수 있는 API입니다.

| 메서드 | 엔드포인트 |
| --- | --- |
| GET | `/api/post/Monthly?month={month}` |

### Request

**Path Parameters**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| month | 필수 | String | 조회하려는 월 <br>  - `yyyy-mm` 형식으로 입력 |

**Request Header**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| key | 필수 | String | Authorization |
| value | 필수 | String | 로그인 시 JWT <br>  - `ex. Bearer {토큰}` |

### Response

**Response Fields**

| 항목 | 타입 | 설명 |
| --- | --- | --- |
|    | List | 해당 월에 작성된 게시글의 일자 |

**Sample Code**

```json
[
	"2022-08-26",
	"2022-08-27",
	"2022-08-30"
]
```

# 실천

## 실천 조회

전체 실천의 이름과 ID를 조회할 수 있는 API입니다.

| 메서드 | 엔드포인트 |
| --- | --- |
| GET | `/api/behavior` |

### Request

**Request Header**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| key | 필수 | String | Authorization |
| value | 필수 | String | 로그인 시 JWT <br>  - `ex. Bearer {토큰}` |

### Response

**Response Fields**

| 항목 | 타입 | 설명 |
| --- | --- | --- |
| behaviorId | String | 실천 ID |
| name | String | 실천 이름 |

# 팔로우

## 유저 팔로우

유저를 팔로우할 수 있는 API입니다.

| 메서드 | 엔드포인트 |
| --- | --- |
| POST | `/api/user/follow` |

### Request

**Request Header**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| key | 필수 | String | Authorization |
| value | 필수 | String | 로그인 시 JWT <br>  - `ex. Bearer {토큰}` |

**Request Body**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| targetId | 필수 | Integer | 팔로우하려는 유저 ID |

**Sample Code**

```json
{
	"targetId": "1"
}
```

### Response

**Response Fields**

| 항목 | 타입 | 설명 |
| --- | --- | --- |
| message | String | 요청 결과 |
| badgeAchieveList | List | 팔로우 시점에 유저가 획득한 뱃지 정보<br> - `7`: 함께 갈 동료 |

**Sample code**

``` json
{
	"message": "Follow{fromUser=2, toUser=1팔로우 관계를 시작합니다)",
	"badgeAchieveList": [
		7
	]
}

```

## 팔로우 취소

유저 팔로우를 취소할 수 있는 API입니다.

| 메서드 | 엔드포인트 |
| --- | --- |
| DELETE | `/api/user/follow` |

### Request

**Request Header**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| key | 필수 | String | Authorization |
| value | 필수 | String | 로그인 시 JWT <br>  - ``ex. Bearer {토큰}`` |

**Request Body**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| target | 필수 | Integer | 팔로우를 취소할 유저 ID |

### Response

| 항목 | 타입 | 설명 |
| --- | --- | --- |
| message | String | 팔로우 취소 안내 |

## 팔로워 조회

유저의 팔로워를 조회할 수 있는 API입니다.

| 메서드 | 엔드포인트 |
| --- | --- |
| GET | `/api/user/follower` |

### Request

**Request Header**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| key | 필수 | String | Authorization |
| value | 필수 | String | 로그인 시 JWT <br>  - `ex. Bearer {토큰}` |

### Response

**Respose Fields**

| 항목 | 타입 | 설명 |
| --- | --- | --- |
| userId | Integer | 팔로워 ID |
| userNickName | String | 팔로워 닉네임 |
| selfIntroduce | String | 팔로워 자기소개 |

## 팔로잉 조회

유저를 팔로우하는 타 유저를 조회할 수 있는 API입니다.

| 메서드 | 엔드포인트 |
| --- | --- |
| GET | `/api/user/following` |

### Request

**Request Header**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| key | 필수 | String | Authorization |
| value | 필수 | String | 로그인 시 JWT <br>  - `ex. Bearer {토큰}` |

### Response

**Respose Fields**

| 항목 | 타입 | 설명 |
| --- | --- | --- |
| userId | Integer | 팔로잉 유저 ID |
| userNickName | String | 팔로잉 유저 닉네임 |
| selfIntroduce | String | 팔로잉 유저 자기소개 |

**Sample Code**

```json
[
 {
	 "userId": 2,
	 "nickName"": "활기찬 활동가",
	 "selfIntroduce": "간단한 자기소개글을 적어주세요!"
 }
]
```

# 게시물 하트

## 하트 활성화

게시물에 좋아요를 누를 수 있는 API입니다.

| 메서드 | 엔드포인트 |
| --- | --- |
| POST | `/api/post/heart` |

### Request

**Request Header**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| key | 필수 | String | Authorization |
| value | 필수 | String | 로그인 시 JWT <br>  - `ex. Bearer {토큰}` |

**Request Body**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| targetPostId | 필수 | Integer | 좋아요를 선택하려는 게시물 ID |

### Response

**Response Fields**

| 항목 | 타입 | 설명 |
| --- | --- | --- |
|  |  | 요청 결과 |

## 하트 비활성화

게시물에 눌렀던 좋아요를 취소할 수 있는 API입니다.

| 메서드 | 엔드포인트 |
| --- | --- |
| DELETE | `/api/post/heart` |

### Request

**Request Header**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| key | 필수 | String | Authorization |
| value | 필수 | String | 로그인 시 JWT <br>  - `ex. Bearer {토큰}` |

**Request Body**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| targetPostId | 필수 | Integer | 좋아요를 취소하려는 게시물 ID |

### Response

**Response Fields**

| 항목 | 타입 | 설명 |
| --- | --- | --- |
|  |  | 요청 결과 |

# 뱃지

## 뱃지 조회

유저가 획득한 뱃지를 조회할 수 있는 API입니다.

| 메서드 | 엔드포인트 |
| --- | --- |
| GET | `/api/user/badge` |

### Request

**Request Header**

| 항목 | 필수 여부 | 타입 | 설명 |
| --- | --- | --- | --- |
| key | 필수 | String | Authorization |
| value | 필수 | String | 로그인 시 JWT <br>  - `ex. Bearer {토큰}` |

### Response

**Response Fields**

| 항목 | 타입 | 설명 |
| --- | --- | --- |
| userId | Integer | 유저 아이디 |
| badgeStateList | List | 유저가 획득한 뱃지 정보<br>- 각 뱃지를 번호로 맵핑함<br>- `0`: 작심삼일이 모이면<br>- `1`: 꾸준함의 재능<br>- `2`: 왕발자국<br>- `3`: 실천가<br>- `4`: 제로웨이스트 고수<br>- `5`: 나만의 실천<br>- `6`: 웰컴 백<br>- `7`: 함께 갈 동료<br>- `8`: 작은 마음<br>- `9`: 치어 업 |

**Sample Code**

```json
{
	"userId": 2,
	"badgeStateList": [
		"0",
		"1",
		"5"
	]
}
```
