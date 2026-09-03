# 기다슬 | Applied AI Engineer

사용자와 현업의 문제를 **데이터 파이프라인과 평가 가능한 AI 시스템**으로 연결합니다.  
모델 성능만 보고 끝내지 않고, 입력 데이터·실패 원인·운영 조건을 분석해 실제로 사용할 수 있는 형태까지 구현합니다.

- **Applied AI** — ML·LLM 모델을 API와 자동화 파이프라인으로 연결
- **Evaluation** — 정확도뿐 아니라 Recall, 비용, 실패 사례와 데이터 품질을 함께 검토
- **Reliable Engineering** — 재현 가능한 실험, 예외 처리, 설명 가능성, CI/CD를 지향

## Featured Work

### 매의 눈 — AI 기반 잠재 매장 발굴 시스템

> 인턴십 · End-to-End Applied AI · 코드 및 원천 데이터 비공개

영업 담당자가 수작업으로 신규 매장을 찾고 평가하던 과정을 데이터 수집, ML·LLM 분류, QC Score, API 호출이 연결된 파이프라인으로 전환했습니다. 개발 전 과정을 단독 수행했으며, 영업팀·QC Center·AI 콘텐츠팀의 검수 기준을 시스템 설계에 반영했습니다.

**담당:** Selenium 기반 멀티소스 수집 · XGBoost/SBERT 실험 · Gemini 의미 기반 분류 · SHAP · FastAPI · Docker · AWS S3  
**핵심 판단:** 기존 제휴 매장과의 유사도만으로는 신규 후보를 발굴하기 어렵다는 한계를 확인하고, 인기도 예측·제휴 가능성·LLM 카테고리 분류를 분리했습니다.  
**증거 범위:** 회사 코드와 데이터는 공개하지 않으며, 공개 가능한 설계·역할·검증 범위만 [Case Study](case-studies/eagle-eye.md)에 정리했습니다.

### [Capstone Pose — 실시간 낙상 감지](https://github.com/gidaseul/capstone_pose)

> Computer Vision · Real-time Pipeline · Team Lead

RGB 카메라에서 YOLO로 사람 영역을 제한하고, MediaPipe의 33개 관절 좌표와 LSTM 시퀀스 모델을 결합한 2단계 낙상 감지 프로토타입입니다. 처리 지연으로 오래된 프레임이 쌓이지 않도록 프로세스 간 큐를 1개로 제한해 최신 프레임을 우선 처리했습니다.

**담당:** 전체 파이프라인 및 멀티프로세싱 구조 설계 · YOLO/MediaPipe/LSTM 연동 · 팀 리딩  
**검증:** `(150, 99)` 키포인트 시퀀스 · 5회 연속 규칙 트리거 · LSTM 임계값 `0.7` · 이벤트 영상 저장  
**한계:** 전체 테스트셋 Precision/Recall/F1은 아직 정리되지 않아 성능 주장에 포함하지 않습니다.

### [Visual Representation Analysis](https://github.com/gidaseul/machine-learning-project)

> Classical ML · Representation Learning · Failure Analysis

MNIST와 배경 잡음이 큰 SportsBall 데이터에 대해 ROI, HOG/PCA/Sobel, SVM/XGBoost와 CNN·Autoencoder·Contrastive Learning을 비교했습니다. 팀 산출물과 개인 실험 로그를 분리하고, 낮은 성능도 숨기지 않은 채 입력 품질과 latent space 관점에서 원인을 분석했습니다.

**개인 탐구:** ROI 추출 · 전처리 순서 · HOG+색상 히스토그램 · 분류기 비교  
**결과:** MNIST `98.0%` · SportsBall base CNN `48.0%`; 표현학습 실패 구간은 t-SNE와 heatmap으로 분석  
**증거:** 실험 노트북 · 개인 로그 · 보고서/PDF · 시각화 자료

### 후판 Scale 불량 예측

> Manufacturing AI · Statistical Analysis · Cost-aware Evaluation

1,000건의 후판 공정 데이터에서 불가능한 센서값과 HSB 조건의 완전분리 문제를 발견하고, 공정 규칙·통계적 설명·예측 모델을 분리했습니다. 5인 팀에서 모델링을 담당했으며, 정확도보다 불량 미탐을 줄이는 Recall을 우선했습니다.

**담당:** EDA · VIF/카이제곱 검정 · 로지스틱 회귀 해석 · 트리 계열 모델 비교 · 임계값 검토  
**팀 결과:** XGBoost 후보 `Precision 100%`, `Recall 95.88%`, `ROC-AUC 0.9883`  
**적용안:** AI 1차 선별 후 의심 제품만 정밀 검사하는 2단계 품질관리 흐름  
**증거 범위:** 교육 데이터와 팀 산출물을 기반으로 하며, 세부 조건은 [Case Study](case-studies/posco-steel-quality.md)에 구분해 기록했습니다.

## Research & Prototypes

- [Brain MRI Research](https://github.com/gidaseul/brain-mri-research) — 3D MRI 입력 표준화와 CAM 해석을 정리한 공개 연구 기록. 팀 baseline 수치와 개인 기여를 분리해 표기합니다.
- [Docent AI Prototype](https://github.com/gidaseul/tts) — RAG·LLM·TTS를 연결한 공개 기술 프로토타입. 외부 API 없는 테스트와 검색 평가를 보강 중입니다.
- [Algorithm Solutions](https://github.com/gidaseul/Algorithm-Solutions) — 여러 알고리즘 플랫폼의 풀이와 통계를 GitHub Actions로 자동 집계합니다.

## Experience

- **텐핑거스(데이트팝), AI 개발 인턴** — 잠재 매장 수집·평가 AI 파이프라인 구축
- **VML Lab, 학부연구생** — Computer Vision 기반 의료 AI 연구와 실험
- **Curiator Studio, 팀장·AI 파트** — 다국어 LLM·TTS 도슨트 파이프라인
- **Syncorbis, Bio & Software Engineer** — 생명과학 실험 자동화 장치·소프트웨어 기획

## Education & Recognition

- 숭실대학교 AI소프트웨어학부 — 인공지능전공 · 빅데이터 융합전공
- LG Aimers 7기 Data Intelligence
- SSAFY 15기
- SQLD
- 2019 대한민국 인재상
- 2024 Soongsil Programming Contest 은상

## Engineering Principles

1. 팀 결과와 개인 기여를 분리해 기록합니다.
2. 재현 방법이나 근거가 없는 수치는 성과로 사용하지 않습니다.
3. 성공한 실험뿐 아니라 실패 원인과 한계도 공개합니다.
4. 민감한 원천 데이터·회사 코드·환자 정보는 공개하지 않습니다.

## Contact

- GitHub: [@gidaseul](https://github.com/gidaseul)
- Email: [rlektmf0328@gmail.com](mailto:rlektmf0328@gmail.com)
