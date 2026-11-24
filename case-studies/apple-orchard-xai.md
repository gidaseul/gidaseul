# 사과 잎 병해 진단 · 설명 가능한 AI 플랫폼

포스코 청년 AI·Big Data 아카데미 5인 팀 프로젝트입니다. 저는 분류 결과, 유사 사례, Grad-CAM과 리포트를 한 화면에서 확인하는 대시보드를 구현하고 배포했습니다. [공개 대시보드](https://applecare-orchard.vercel.app/)

## 대시보드에서 진단 근거를 확인하는 경로

```text
공개 데모
├── /analysis        과수원 구역 위험도, 병해 필터, 대표 잎 목록
├── /report          구역별 검출 결과와 대표 잎 근거 묶음
├── /leaf            선택한 잎의 분류, 유사 사례, Grad-CAM, 리포트
└── /analyze         새 잎 사진을 업로드하는 화면
    └── /api/infer   파일을 분리된 FastAPI 추론 서버로 전달
```

구역을 살피는 화면과 개별 잎을 분석하는 화면은 역할이 다릅니다. 저장된 사례는 구역에서 잎으로 들어가 비교할 수 있습니다. 새 업로드는 웹 서버가 파일을 추론 서버로 전달하고, 응답을 받아 결과를 표시하는 흐름입니다.

대시보드 코드에서 화면은 `app/analysis/page.tsx`, `app/report/page.tsx`, `app/leaf/page.tsx`로 나뉩니다. `lib/orchard-data.ts`에서 구역과 잎을 연결하고, 저장된 진단은 `lib/survey-data.ts`에서 읽습니다. 업로드는 `app/analyze/page.tsx`에서 시작해 `app/api/infer/route.ts`를 거칩니다.

## 분류 점수와 근거를 함께 보여주는 이유

팀 파이프라인은 EfficientNet-B0 분류 뒤 DINOv2로 유사 잎을 찾고, Grad-CAM과 잎 마스크로 모델 반응이 잎에 놓였는지 확인합니다. 근거가 엇갈리는 사례는 추가 관찰 경로로 보낼 수 있도록 설계했습니다. 화면은 분류 점수 옆에 유사 사례 일치도와 종합 확신도를 배치했습니다.

| 잎 원본 | Grad-CAM |
| :---: | :---: |
| <img src="https://applecare-orchard.vercel.app/images/survey/f883d3b65ca8702e.jpg" height="180" alt="검은별무늬병 잎 원본"> | <img src="https://applecare-orchard.vercel.app/images/survey/cam/f883d3b65ca8702e.png" height="180" alt="같은 잎의 Grad-CAM 히트맵"> |

[이 잎의 공개 리포트](https://applecare-orchard.vercel.app/leaf?zone=B&id=b-02)에서 분류 점수는 100%로 표시됐지만, 가장 비슷한 사례 4건 중 같은 병해는 1건이었습니다. 리포트의 종합 확신도는 ‘중상’입니다. Grad-CAM은 모델 반응이 강한 위치를 살펴보는 데 쓰입니다.

팀은 34명에게 리포트 제공 여부에 따른 진단 문항 결과를 비교했습니다. 설문은 팀 결과이며, 위 화면은 저장된 공개 사례를 보여줍니다. 사진을 새로 업로드하는 경로는 추론 서버 연결이 필요합니다. [구역 분석](https://applecare-orchard.vercel.app/analysis) · [새 사진 분석 화면](https://applecare-orchard.vercel.app/analyze)

[프로필의 대표 프로젝트로 돌아가기](../README.md#대표-프로젝트)
