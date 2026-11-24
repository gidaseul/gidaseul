# 밥보기 — 섭취 기반 영양소 관리 앱

> 숭실대학교 소프트웨어프로젝트 수업 · 4인 팀 · 2024 소프트웨어공모전 은상

팀은 Android 앱에서 식사를 기록하고 하루 영양소 섭취량을 확인할 수 있도록 구현했습니다. 저는 Spring Boot 백엔드에서 음식 이름 검색과 영양정보 상세 조회를 맡았습니다. [Android 클라이언트](https://github.com/gidaseul/babbogi) · [팀 백엔드](https://github.com/BabBogi/BabBogi-backend)

## 화면에서 데이터까지

<img src="https://github.com/user-attachments/assets/82721282-0146-4b85-b7c2-baeabb3dcb0e" width="240" alt="밥보기 앱의 음식 검색 화면">

```text
Android
├── ui/FoodSearchScreen.kt         음식명 입력과 후보 선택
└── network/ServerApiClient.kt    검색과 영양정보 조회 요청
Spring Boot
├── controller/SavedFoodController.java  GET /search, GET /food
├── service/SavedFoodService.java        후보 매핑과 중량별 영양정보 환산
└── repository/SavedFoodRepository.java  이름 검색, 식품 코드 상세 조회
```

[검색 화면 코드](https://github.com/gidaseul/babbogi/blob/main/app/src/main/java/com/example/babbogi/ui/FoodSearchScreen.kt) · [클라이언트 요청 정의](https://github.com/gidaseul/babbogi/blob/main/app/src/main/java/com/example/babbogi/network/ServerApiClient.kt)

## 검색에서 영양정보까지

| 단계 | 요청과 처리 |
| --- | --- |
| 음식 후보 검색 | `GET /search?name=...`에서 음식명에 검색어가 포함된 행을 조회합니다. 검색 결과에 식품 코드, 음식명, 분류, 제조사 정보를 돌려줍니다. |
| 선택한 음식 확인 | `GET /food?foodcode=...`에서 선택한 식품의 코드로 상세 레코드를 조회합니다. 표시명이 같은 음식도 검색 결과의 코드로 구분할 수 있습니다. |
| 영양정보 환산 | 열량과 영양소에 `식품 중량 ÷ 100`을 곱해 상세 응답을 구성합니다. 중량이 없으면 100을 사용하고, 각 영양소는 소수점 첫째 자리까지 반올림합니다. 제조사 정보가 비어 있으면 ‘해당 없음’으로 표시합니다. |

검색에서 사용한 음식명을 상세 조회의 식별자로도 쓰면 이름이 같은 상품을 구별하기 어렵습니다. 상세 조회를 식품 코드로 바꾸고 검색 응답에 이 코드를 포함해, 화면에서 선택한 후보를 같은 식품 레코드에 연결했습니다. [담당 변경 커밋](https://github.com/BabBogi/BabBogi-backend/commit/d4b4a2505c84fde49c82c96ca94ac379f92696bf)

## 팀 기능과 확인 범위

팀 서비스의 범위에는 식사 기록, 일일 영양 리포트, 알림이 포함됐습니다. 앱의 화면과 팀 기능 전체는 공동 산출물입니다. [식사 기록 API](https://github.com/BabBogi/BabBogi-backend/blob/4a0be2e32efc1a38347ec2b97ce72c97cbf0761e/src/main/java/BobBogi/BobBogispring/controller/ConsumptionController.java) · [일일 리포트 API](https://github.com/BabBogi/BabBogi-backend/blob/4a0be2e32efc1a38347ec2b97ce72c97cbf0761e/src/main/java/BobBogi/BobBogispring/controller/UserController.java)

공개 코드의 환산 로직은 영양 성분 결측을 0으로 응답합니다. 이 값은 실제 측정값 0과 구별되지 않습니다. 수상은 팀 성과이며 실제 이용률과 영양 개선 효과를 측정한 자료는 없습니다. [클라이언트 README의 수상 기록](https://github.com/gidaseul/babbogi#readme)

[프로필의 더 살펴볼 프로젝트로 돌아가기](../README.md#더-살펴볼-프로젝트)
