# Curiator · 박물관 도슨트 AI

숭실대 캡스톤 팀 프로젝트에서 맡았던 AI 파트를 정리한 저장소입니다. 작품 정보를 입력하면 어린이·일반·전문가 수준에 맞춰 다섯 언어 중 하나로 해설을 생성합니다. [프로젝트 저장소](https://github.com/gidaseul/Curiator)

<img src="https://raw.githubusercontent.com/gidaseul/Curiator/b0a6f03ca08b627fecc50dbbe443024755787ed3/docs/screens/03-level.jpg" width="720" alt="Curiator에서 해설 언어, 관람객 수준, 관련 전시 자료 검색, 해설 유형을 고르는 화면">

## 해설을 먼저 고치고 음성을 만드는 흐름

1. 작품이나 챕터 JSON을 입력하면 FastAPI가 공통 형식으로 변환합니다. 전시 자료 검색을 켜면 관련 작품과 챕터를 함께 찾아 Gemini에 전달합니다.
2. `POST /generate-text`가 이야기 중심 해설과 역사·정석 해설을 반환합니다. 웹 화면에 검색한 참고 자료도 표시합니다.
3. 관람객은 한 해설을 골라 문장을 편집합니다. `POST /generate-audio`는 편집한 문장만 받아 Gemini TTS로 읽어 줍니다. 글을 고친 뒤 음성을 만들 수 있도록 두 요청을 분리했습니다.

```text
Curiator/
├── frontend/src/steps/   작품 입력, 수준 선택, 해설 편집, 오디오 재생
├── main.py              해설·오디오·전시 질문 API
├── museum_source.py     작품·챕터 데이터를 공통 형식으로 변환
├── llm/generate_docent.py  해설과 질문 답변 프롬프트
├── rag/store.py         검색 점수, 결과 선별, 어휘 검색 대체 경로
├── tts/generate_tts.py  Gemini 음성 생성
└── tests/              외부 API 없이 검증하는 입력·검색·응답 테스트
```

## 검색 근거를 어디까지 믿을 수 있나

`/ask`는 검색 기준을 넘는 참고 자료가 없으면 모델을 부르지 않고 안내 문구를 돌려줍니다. `grounded: true`는 참고 자료를 찾아 프롬프트에 전달했다는 뜻입니다. 답변의 개별 문장이 자료와 일치하는지 확인하는 검증 단계는 별도입니다.

[화면에서 요청 보내는 코드](https://github.com/gidaseul/Curiator/blob/main/frontend/src/App.tsx) · [백엔드 요청 처리](https://github.com/gidaseul/Curiator/blob/main/main.py) · [실행 방법](https://github.com/gidaseul/Curiator#실행) · [검증 범위](https://github.com/gidaseul/Curiator#확인한-것과-확인하지-않은-것)

[프로필의 더 살펴볼 프로젝트로 돌아가기](../README.md#더-살펴볼-프로젝트)
