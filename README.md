# EcoLog API 개요

## EcoLog 서비스 소개

<figure><img src=".gitbook/assets/앱 소개.png" alt=""><figcaption></figcaption></figure>

Eco Log는 하루동안 환경을 위해 실천한 사항을 기록하는 웹앱 서비스입니다. 제로웨이스트를 위해 가벼운 실천을 시도해보고자하는 사용자의 꾸준함을 응원하고 지원하기 위해 기획 및 개발하였습니다.

서비스의 주요 기능은 다음과 같습니다.

* 로그인: 카카오, 네이버, 구글 소셜 로그인
* 프로필: 사용자의 실천 현황을 요약해 제공
* 게시물: 실천 카테고리 또는 직접 입력 실천과 하루 소감을 담은 게시물을 발행하고 수정
* 팔로우: 팔로잉, 팔로워를 조회하고 관리
* 게시물 하트: 팔로우 중인 사용자의 실천 게시물에 좋아요 표시
* 뱃지: 특정 행동을 수행할 때마다 제공되는 뱃지를 조회

## API 퀵 레퍼런스 테이블

| 구분     | 메서드                                               | 엔드포인트                                                    | 설명               |
| ------ | ------------------------------------------------- | -------------------------------------------------------- | ---------------- |
| 로그인    | <mark style="background-color:blue;">GET</mark>   | [/api/oauth/kakaotoken](reference/api/login.md#kakao)    | 카카오 소셜 로그인       |
|        | <mark style="background-color:blue;">GET</mark>   | [/api/oauth/navertoken](reference/api/login.md#naver)    | 네이버 소셜 로그인       |
|        | <mark style="background-color:blue;">GET</mark>   | [/api/oauth/googletoken](reference/api/login.md#google)  | 구글 소셜 로그인        |
|        | <mark style="background-color:blue;">GET</mark>   | [/api/me](reference/api/login.md#loginuser)              | 현재 로그인 중인 유저 조회  |
|        | <mark style="background-color:red;">DELETE</mark> | [/api/user](reference/api/login.md#withdraw)             | 유저 탈퇴            |
| 프로필    | <mark style="background-color:blue;">GET</mark>   | [/api/user/profile](reference/api/profile.md#view)       | 프로필(실천 현황) 조회    |
|        | <mark style="background-color:green;">POST</mark> | [/api/user/profile](reference/api/profile.md#edit)       | 프로필 수정           |
|        | <mark style="background-color:blue;">GET</mark>   | [/api/user/summary](reference/api/profile.md#summary)    | 유저 실천 정보 요약 조회   |
|        | <mark style="background-color:blue;">GET</mark>   | [/api/user/search](reference/api/profile.md#search)      | 유저 검색            |
| 게시물    | <mark style="background-color:green;">POST</mark> | [/api/post](reference/api/post.md#save)                  | 게시물 저장           |
|        | <mark style="background-color:orange;">PUT</mark> | [/api/post/change](reference/api/post.md#edit)           | 게시물 수정           |
|        | <mark style="background-color:red;">DELETE</mark> | [/api/post](reference/api/post.md#delete)                | 게시물 삭제           |
|        | <mark style="background-color:blue;">GET</mark>   | [/api/post/daily](reference/api/post.md#feed)            | 피드 조회            |
|        | <mark style="background-color:blue;">GET</mark>   | [/api/post/Monthly](reference/api/post.md#monthly)       | 게시물 월 단위 조회      |
| 실천     | <mark style="background-color:blue;">GET</mark>   | [/api/behavior](reference/api/action.md#view)            | 전체 실천 ID 및 이름 조회 |
| 팔로우    | <mark style="background-color:green;">POST</mark> | [/api/user/follow](reference/api/follow.md#add)          | 유저 팔로우           |
|        | <mark style="background-color:red;">DELETE</mark> | [/api/user/follow](reference/api/follow.md#unfollow)     | 유저 팔로우 취소        |
|        | <mark style="background-color:blue;">GET</mark>   | [/api/user/follower](reference/api/follow.md#follower)   | 팔로워 조회           |
|        | <mark style="background-color:blue;">GET</mark>   | [/api/user/following](reference/api/follow.md#following) | 팔로잉 조회           |
|        | <mark style="background-color:red;">DELETE</mark> | [/api/user/follower](reference/api/follow.md#view)       | 팔로워 삭제           |
| 게시물 하트 | <mark style="background-color:green;">POST</mark> | [/api/post/heart](reference/api/like.md#active)          | 하트 활성화           |
|        | <mark style="background-color:red;">DELETE</mark> | [/api/post/heart](reference/api/like.md#unactive)        | 하트 활성화 취소        |
| 뱃지     | <mark style="background-color:blue;">GET</mark>   | [/api/user/badge](reference/api/badge.md#view)           | 유저 뱃지 획득 정보 조회   |

## Base URL

API 호출 시 base URL은 다음과 같습니다.

| 항목       | URL                                  |
| -------- | ------------------------------------ |
| Base URL | `https://www.eco-log-backend.kro.kr` |

## HTTP 상태 코드

| HTTP 상태 코드 | 설명         |
| ---------- | ---------- |
| 200        | 성공         |
| 400        | 잘못된 요청     |
| 401        | 유효하지 않은 토큰 |
| 444        | 만료된 토큰     |

## 문서 버전

* 2023.02.09. 문서 첫 생성
