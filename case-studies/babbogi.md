# 밥보기 — 섭취 기반 영양소 관리 앱

> 숭실대학교 소프트웨어프로젝트 수업 · 4인 팀 · 2024 소프트웨어공모전 은상

팀은 Android 앱에서 식사를 기록하고 하루 영양소 섭취량을 확인할 수 있도록 구현했습니다. 저는 Spring Boot 백엔드에서 음식 이름 검색과 영양정보 상세 조회를 맡았습니다. [Android 클라이언트](https://github.com/gidaseul/babbogi) · [팀 백엔드](https://github.com/BabBogi/BabBogi-backend)

## 목차

1. [문제와 담당 범위](#문제와-담당-범위)
1. [화면에서 데이터까지](#화면에서-데이터까지)
1. [검색에서 영양정보까지](#검색에서-영양정보까지)
1. [이름이 같은 검색 결과를 처리하는 예시](#이름이-같은-검색-결과를-처리하는-예시)
1. [중량 환산 예시와 예외 처리](#중량-환산-예시와-예외-처리)
1. [팀 기능과 확인 범위](#팀-기능과-확인-범위)

## 문제와 담당 범위

앱에서 ‘김치’를 검색하면 비슷한 음식명이 여러 개 나옵니다. 사용자가 그중 한 음식을 고르면, 선택한 항목의 영양정보를 일관되게 가져와야 합니다. 저는 검색 결과에 식품 코드를 포함하고, 상세 조회가 이 코드를 사용하도록 백엔드를 변경했습니다. Android 화면과 식사 기록 전체는 팀의 작업입니다.

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

## 이름이 같은 검색 결과를 처리하는 예시

예를 들어 ‘김치’를 검색했을 때 같은 음식명이 두 번 표시되더라도 제조사와 식품 코드가 다를 수 있습니다. 검색 API는 이름으로 후보를 모으고, 상세 API는 앱에서 선택한 코드에 해당하는 레코드를 조회합니다.

| 사용자 동작 | 앱과 서버에서 유지하는 정보 |
| --- | --- |
| ‘김치’를 입력해 검색 | 서버가 이름이 포함된 행을 찾고, 이름과 제조사 정보 옆에 각 행의 식품 코드를 함께 돌려줍니다. |
| 두 후보 중 두 번째 항목을 선택 | 화면에 같은 이름이 보이더라도 상세 API에는 두 번째 항목의 코드만 전달합니다. |
| 상세 화면에서 영양 성분 확인 | 서버는 그 코드에 해당하는 중량과 영양 성분을 읽어, 코드와 중량이 맞는 한 건의 정보를 표시할 수 있게 합니다. |

이 흐름에서 검색어는 결과를 찾기 위한 도구이고, 코드는 선택한 식품을 다시 찾기 위한 식별자입니다. 앱에서 표시 문구를 바꾸거나 유사한 이름을 추가하더라도 두 API를 연결하는 기준은 식품 코드입니다.

## 중량 환산 예시와 예외 처리

상세 조회는 데이터에 등록된 중량을 사용합니다. 100g 기준 영양 함량에 `저장 중량 ÷ 100`을 곱하고, 탄수화물·단백질·지방 등에도 같은 방식을 적용합니다.

| 데이터 상태 | 공개 구현의 처리 |
| --- | --- |
| 식품 중량이 비어 있음 | 100g으로 계산합니다. |
| 영양 성분이 비어 있음 | 해당 성분을 0으로 돌려줍니다. |
| 유효한 식품 코드가 조회되지 않음 | 서비스가 상세 데이터를 반환하지 않습니다. |

환산값을 확인할 때는 다음 세 상황을 구분할 수 있습니다. 100g 기준 50kcal가 등록돼 있고 저장 중량이 150g이면 75.0kcal입니다. 같은 데이터에서 중량만 비어 있으면 100g을 적용해 50.0kcal가 됩니다. 열량 자체가 비어 있으면 공개 구현은 0으로 응답합니다. 결측을 의미하는 0과 실제 0kcal가 같은 값으로 표시되는 한계가 있어, 데이터 품질을 확인하려면 원본 레코드도 함께 살펴야 합니다.

## 팀 기능과 확인 범위

팀 서비스의 범위에는 식사 기록, 일일 영양 리포트, 알림이 포함됐습니다. 앱의 화면과 팀 기능 전체는 공동 산출물입니다. [식사 기록 API](https://github.com/BabBogi/BabBogi-backend/blob/4a0be2e32efc1a38347ec2b97ce72c97cbf0761e/src/main/java/BobBogi/BobBogispring/controller/ConsumptionController.java) · [일일 리포트 API](https://github.com/BabBogi/BabBogi-backend/blob/4a0be2e32efc1a38347ec2b97ce72c97cbf0761e/src/main/java/BobBogi/BobBogispring/controller/UserController.java)

수상은 팀 성과이며 실제 이용률과 영양 개선 효과를 측정한 자료는 없습니다. 다음 검증에서는 이름이 같은 두 식품을 각각 선택해 코드와 상세 정보가 맞게 돌아오는지 확인하고, 결측 영양 성분을 사용자에게 어떻게 표시할지도 정해야 합니다. 현재 구현에서는 결측을 실제 측정값 0과 구분할 수 없습니다. [클라이언트 README의 수상 기록](https://github.com/gidaseul/babbogi#readme)

[프로필의 더 살펴볼 프로젝트로 돌아가기](../README.md#더-살펴볼-프로젝트)
