# 기다슬 · Applied AI Engineer

**[POSTECH 인공지능연구원(PIAI)](https://piai.postech.ac.kr/english) 연구원**

컴퓨터비전과 LLM을 커머스, 안전, 의료영상 문제에 적용해 왔습니다. 모델을 검증하고 그 결과를 대시보드나 API로 구현합니다.

[이메일](mailto:hye0328@postech.ac.kr)

## 대표 프로젝트

### 매의 눈 · AI 기반 신규 매장 발굴

- 텐핑거스 인턴으로 매장 데이터를 수집하고, XGBoost로 제휴 가능성을 예측해 결과를 API로 제공하는 기능을 개발했습니다.
- 메뉴와 리뷰를 바탕으로 LLM이 업종을 해석하도록 개선했습니다. ICT 학점연계 프로젝트 인턴십 우수성과전에서 개인 장려상을 받았습니다.

```mermaid
flowchart TB
    A["네이버 매장 수집 · 카카오 평점 병합"] --> B["매장 레코드 정리 · 수집 실패 상태 보존"]
    B -->|"정형 특성"| C["XGBoost 제휴 점수<br/>SHAP으로 특성 기여도 설명"]
    B -->|"메뉴·리뷰"| D["Gemini 업종 분류"]
    D --> E["허용 라벨 검증<br/>파싱 실패 시 대체 처리"]
    C --> F["결과 정리 · QC 점수 · 저장"]
    E --> F
    F --> G["FastAPI로 결과 조회"]
```

**설계 판단** · 제휴 가능성 점수와 업종 라벨을 따로 산출했습니다. 정형 특성의 점수 기여도는 SHAP으로 확인하고, LLM 출력은 허용된 업종 라벨로 제한했습니다. 그림은 공개 사례의 구성 요소를 개략화했습니다.

[개발 사례 읽기](case-studies/eagle-eye.md)

### 사과 잎 병해 진단 · 설명 가능한 AI 플랫폼

- 5인 팀에서 병해 진단 결과와 모델의 판단 근거를 보여주는 대시보드를 구현하고 배포했습니다.
- 청년 AI·BigData 아카데미 팀 프로젝트 최우수상을 받았습니다. 팀은 34명을 대상으로 리포트 평가 설문을 진행했습니다.

```mermaid
flowchart TB
    A["사과 잎 이미지"] --> B["EfficientNet-B0 · 멀티라벨 분류"]
    B --> C["DINOv2 · 유사 사례 검색"]
    C --> D{"단일 병해이며<br/>분류와 유사 사례가 일치하는가?"}
    D -->|"강한 일치"| F["RAG·LLM · 병해 지식 기반 리포트"]
    D -->|"근거 불일치 또는 복합 병해"| E["VLM · 병반의 색·형태 추가 관찰"]
    E --> F
    B --> H["Grad-CAM · 모델 주목 영역을 잎 마스크와 비교"]
    H --> G["결과 대시보드<br/>근거와 리포트 표시"]
    F --> G
    style G stroke-width:3px
```

**팀 설계와 개인 기여** · 팀 파이프라인은 복합 병해나 근거가 엇갈리는 경우에 VLM으로 추가 관찰합니다. 제가 구현·배포한 부분은 굵은 테두리의 결과 대시보드입니다.

<details>
<summary>공개 데모의 Grad-CAM 예시 보기</summary>

<p>
  <img src="https://applecare-orchard.vercel.app/images/survey/88ddbc939596a5a4.jpg" height="180" alt="병해 진단에 사용한 사과 잎 원본 사진">
  <img src="https://applecare-orchard.vercel.app/images/survey/cam/88ddbc939596a5a4.png" height="180" alt="같은 사과 잎에서 모델이 주목한 영역을 표시한 Grad-CAM 히트맵">
</p>

왼쪽은 사과 잎 원본입니다. 오른쪽은 같은 샘플에서 분류 모델이 주목한 영역입니다.

</details>

[라이브 데모](https://applecare-orchard.vercel.app/)

### 실시간 낙상 감지

- RGB 영상에서 YOLO로 사람을 찾고, MediaPipe로 자세를 추정한 뒤 LSTM으로 낙상 여부를 판정했습니다.
- 카메라 처리와 LSTM 추론을 별도 프로세스로 나누고, 두 프로세스 사이에 대기 항목 하나를 담는 큐를 뒀습니다.

```mermaid
flowchart TB
    A["카메라 · YOLO11n 사람 검출"] --> B["사람 영역 · MediaPipe 관절 33개 × 3좌표"]
    B --> C{"자세 규칙 3개 중 2개 이상 충족<br/>의심 판정이 5회 누적됐나?"}
    C -->|"예"| D["프레임·관절 버퍼 스냅샷<br/>프로세스 간 큐 최대 1건"]
    C -->|"아니오"| A
    D --> E["LSTM · 관절 시퀀스 150 × 99"]
    E -->|"점수 0.7 초과"| F["로컬 MP4 저장 · LSTM 워커 30초 대기"]
```

**설계 판단** · 엉덩이·발·코의 상대 위치로 의심 구간을 먼저 골라냅니다. 큐가 가득 차면 기존 대기 항목의 교체를 시도합니다. LSTM 워커는 관절 좌표 150개 시점이 갖춰졌을 때 추론합니다.

[카메라와 자세 규칙](https://github.com/gidaseul/capstone_pose/blob/49a0ad8620eb1c05e7e772ec47ac1bfca14539e9/process/CameraProcess.py#L31-L126) · [프로세스 간 큐](https://github.com/gidaseul/capstone_pose/blob/49a0ad8620eb1c05e7e772ec47ac1bfca14539e9/PipedProcess.py#L12-L45) · [LSTM과 영상 저장](https://github.com/gidaseul/capstone_pose/blob/49a0ad8620eb1c05e7e772ec47ac1bfca14539e9/process/LSTMProcess.py#L19-L69)

<details>
<summary>다른 프로젝트 보기</summary>

- [후판 Scale 불량 예측](case-studies/posco-steel-quality.md) — 공정 변수에서 파생변수를 설계했습니다. 교육 데이터에서 팀의 최종 XGBoost 후보가 불량 97건 중 93건을 검출했습니다.
- **신용카드 사기 탐지** — 샘플링과 모델의 144개 조합을 비교하고 미탐·오탐 비용으로 모델을 선정했습니다.
- [이미지 분류와 표현학습](https://github.com/gidaseul/machine-learning-project) — MNIST와 SportsBall에서 분류 모델과 표현학습을 비교하고 잠재 공간을 분석했습니다. [t-SNE 분석 그림](https://raw.githubusercontent.com/gidaseul/machine-learning-project/main/assets/images/representation-latent-evidence.png)
- [밥보기](case-studies/babbogi.md) — 영양소 관리 앱의 백엔드에서 음식 검색·상세 조회를 담당했습니다. 팀으로 숭실대 소프트웨어공모전 은상을 받았습니다.
- [Docent AI](https://github.com/gidaseul/tts) — 관람객 수준에 맞춰 전시를 설명하는 RAG·LLM·TTS 프로토타입입니다.

</details>

## 🛠 Languages & Tools

| 분야와 도구 | 적용한 곳 |
| --- | --- |
| **영상·시계열**<br>Python · OpenCV · YOLO · MediaPipe · TensorFlow/Keras | [실시간 낙상 감지](https://github.com/gidaseul/capstone_pose)에서 사람 검출과 자세 추정을 분리하고, 관절 시퀀스를 LSTM에 전달했습니다. |
| **모델 학습·분석**<br>PyTorch · scikit-learn · t-SNE | [이미지 분류와 표현학습](https://github.com/gidaseul/machine-learning-project)에서 Autoencoder와 대조학습을 실험하고, t-SNE로 두 데이터셋의 잠재 표현을 비교했습니다. |
| **ML·LLM 응용**<br>XGBoost · SHAP · Gemini | [매의 눈](case-studies/eagle-eye.md)에서 제휴 점수의 특성별 기여도를 설명하고, 메뉴와 리뷰를 바탕으로 업종을 분류했습니다. |
| **API·데이터 처리**<br>FastAPI · Docker · AWS S3 · Java/Spring Boot | [매의 눈](case-studies/eagle-eye.md)에서 수집기를 패키징하고 수집 결과를 저장해 API로 제공했습니다. [밥보기](case-studies/babbogi.md)에서는 음식 검색·상세 조회를 구현했습니다. |
| **결과 시각화**<br>Next.js · React | [사과 잎 병해 진단](https://applecare-orchard.vercel.app/)에서 팀 모델의 분류 결과, Grad-CAM, 진단 리포트를 보여주는 대시보드를 구현·배포했습니다. |

## Career Path

- **현재** · [POSTECH 인공지능연구원(PIAI)](https://piai.postech.ac.kr/english) 연구원
- **2026** · 청년 AI·BigData 아카데미 33기 수료. 제조 품질 예측과 병해 진단 프로젝트에 참여했고, 개인 우수상과 협력상을 받았습니다.
- **2025** · 텐핑거스 ICT 학점연계 프로젝트 인턴. 신규 제휴 매장 발굴 시스템 개발을 담당했습니다.
- **2024–2025** · 숭실대 Vision & Machine Learning Lab 학부연구생. PointNet++ 치아 3D 분할을 재현하고 CT 골밀도 데이터를 전처리했습니다.

<details>
<summary><b>Background & other milestones</b></summary>
<br>

**AWARDS**
- **2019** · 대한민국 인재상 — 부총리 겸 교육부장관상 · [기사](https://www.dmorning.kr/news/articleView.html?idxno=41872)
- **2021–25** · 전라남도 으뜸인재 발탁 — 4학년 재능계발비 지원

**EDUCATION & CERTIFICATION**
- **2020–26** · 숭실대학교 AI소프트웨어학부 · 인공지능 및 빅데이터 전공
- **2022** · SQLD 취득
- **2026** · SSAFY 15기 합격 (서울)

**EARLIER EXPERIENCE & ACTIVITIES**
- **2021–22** · Syncorbis Bio & SW Engineer — [생명과학 실험 자동화 장치 설계·특허](https://doi.org/10.8080/1020210123255)
- **2025** · LG Aimers 7기 수요 예측 · GDG Soongsil 5기 Member · Curiator AI 도슨트
</details>

<details>
<summary>소개 영상 보기</summary>

<div align="center">
  <img src="https://github.com/gidaseul/gidaseul/assets/61573303/9415ba69-057a-4c22-ab50-7ac430cff445" alt="소개 영상" width="560" />
</div>

</details>

## 👯 Communities

<table>
<tr>
<td align="center" width="33%">
<img src="https://github.com/user-attachments/assets/0547901c-ed69-4d81-a020-4dd6072572f9" width="140"><br>
<a href="https://www.boostcourse.org">부스트코스 DATA SCIENCE 코칭스터디 수료</a>
</td>
<td align="center" width="33%">
<img src="https://github.com/user-attachments/assets/6274866d-57de-4e6e-98c5-63d715be8edc" width="140"><br>
<a href="https://fastcampus.co.kr/">MLOps : 추천 시스템 구축부터 최적화까지</a>
</td>
<td align="center" width="33%">
<img src="https://github.com/user-attachments/assets/e8e54742-c576-4ed1-abfc-d4fd64200ca7" width="140"><br>
<a href="https://lgaimers.ai/">LG Aimers 7기 수료</a>
</td>
</tr>
</table>

## 🧠 Algorithm Solutions

자동 집계되는 [Algorithm-Solutions](https://github.com/gidaseul/Algorithm-Solutions) 레포와 연결 (GitHub Actions 자동 동기화).

<p align="center">
  <a href="https://solved.ac/hye0328"><img src="http://mazassumnida.wtf/api/v2/generate_badge?boj=hye0328" alt="Solved.ac Profile" /></a>
</p>

<p align="center">
  <a href="https://github.com/gidaseul/Algorithm-Solutions#-platform-progress">
    <img src="https://raw.githubusercontent.com/gidaseul/Algorithm-Solutions/main/assets/bj_progress.svg" width="560" alt="Baekjoon Progress" />
  </a>
</p>

<details>
  <summary>플랫폼별 진행 더 보기</summary>
  <br>
  <p align="center">
    <img src="https://raw.githubusercontent.com/gidaseul/Algorithm-Solutions/main/assets/programmers_progress.svg" width="560" alt="Programmers" /><br><br>
    <img src="https://raw.githubusercontent.com/gidaseul/Algorithm-Solutions/main/assets/swea_progress.svg" width="560" alt="SWEA" /><br><br>
    <img src="https://raw.githubusercontent.com/gidaseul/Algorithm-Solutions/main/assets/codetree_progress.svg" width="560" alt="Codetree" /><br><br>
    <img src="https://raw.githubusercontent.com/gidaseul/Algorithm-Solutions/main/assets/leetcode_progress.svg" width="560" alt="LeetCode" />
  </p>
</details>
