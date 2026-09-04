<h2> 𝐇𝐞𝐥𝐥𝐨 𝐭𝐡𝐞𝐫𝐞, 𝐟𝐞𝐥𝐥𝐨𝐰 <𝚌𝚘𝚍𝚎𝚛𝚜/>! <img src="https://raw.githubusercontent.com/ABSphreak/ABSphreak/master/gifs/Hi.gif" width="30px"></h2>

[![Gmail Badge](https://img.shields.io/badge/-rlektmf0328@gmail.com-c14438?style=flat-square&logo=Gmail&logoColor=white&link=mailto:rlektmf0328@gmail.com)](mailto:rlektmf0328@gmail.com)
[![Instagram Badge](https://img.shields.io/badge/-gidaseul-E4405F?style=flat-square&logo=Instagram&logoColor=white&link=https://instagram.com/gidaseul)](https://instagram.com/gidaseul)

### 기다슬 · Applied AI Engineer

**문제를 정의하고 → 모델·LLM 파이프라인으로 구현하고 → 실패 원인까지 분석해 → 실제로 쓰이는 형태로 배포**하는 개발자입니다.
텐핑거스 AI 인턴, VML 학부연구생을 거치며 컴퓨터비전·RAG·LLM 시스템을 직접 만들고 검증했습니다.

<div align="center">
  <img src="https://github.com/gidaseul/gidaseul/assets/61573303/9415ba69-057a-4c22-ab50-7ac430cff445" alt="소개 영상" width="560" />
</div>

---

## 🚀 대표 프로젝트

### 🍎 [AppleCare+ 사과원 병해 진단](https://applecare-orchard.vercel.app/)

![CV](https://img.shields.io/badge/CV-e8722c?style=flat-square) ![VLM](https://img.shields.io/badge/VLM-e8722c?style=flat-square) ![RAG](https://img.shields.io/badge/RAG-e8722c?style=flat-square) ![LIVE](https://img.shields.io/badge/●%20LIVE-1a9c4c?style=flat-square) ![팀프로젝트](https://img.shields.io/badge/POSCO%20AI%20아카데미%20·%205인%20팀-e8722c?style=flat-square)

**Problem** — 사과 잎 병해 진단은 분류 결과만으로는 사용자가 원인과 조치 방향을 이해하기 어렵다.
**Solution** — 분류(EfficientNet-B0) → DINO 유사 이미지 검증 → Grad-CAM → VLM 시각 속성 판정 → RAG·LLM 리포트로 이어지는 5단계 구조를 팀에서 설계.
**Result** — 발표 기준 분류 Complex F1 0.758, DINO 검증 통과 정답률 98.7%, VLM few-shot 적용 후 정확도 65%→75%(+10%p), 사용자 설문에서 고난도 병해 문항 정답률 최대 +55.8%p 개선.
**Role** — 5인 팀 프로젝트로 데이터셋·모델 비교, XAI 검증, 발표 설계에 참여. 위 수치는 팀 발표 결과이며, 개인 단독 모델 성과가 아님.

[**▶ 라이브 데모**](https://applecare-orchard.vercel.app/) · [GitHub](https://github.com/gidaseul/applecare-orchard) *(현재 비공개 저장소)*

<br>

### 🚶 [실시간 낙상 감지](https://github.com/gidaseul/capstone_pose)

![CV](https://img.shields.io/badge/Computer%20Vision-2f6fed?style=flat-square) ![팀리드](https://img.shields.io/badge/캡스톤%20팀%20리드-2f6fed?style=flat-square)

<a href="https://github.com/gidaseul/capstone_pose">
  <img src="https://github.com/user-attachments/assets/e9b5b0ab-ff87-478e-a8c1-96cbd2d7cbf1" width="480" alt="실시간 낙상 감지 데모">
</a>

**Problem** — RGB 카메라만으로 낙상을 감지해야 하는 캡스톤 과제 (웨어러블 없음).
**Solution** — YOLO로 사람 검출 → MediaPipe 관절 추출 → LSTM 시계열 분류의 2단계 구조. 자세 규칙 연속 5회 만족 시에만 LSTM 평가로 전달해 단발성 오탐을 필터링.
**Result** — 오래된 프레임이 쌓이지 않게 프로세스 큐를 1개로 제한해 최신 프레임을 우선 처리. 직접 구축한 280개 영상 데이터셋으로 검증.

[GitHub](https://github.com/gidaseul/capstone_pose)

<br>

### 🦅 매의 눈 — 잠재 매장 발굴

![Applied AI](https://img.shields.io/badge/Applied%20AI-9c6b30?style=flat-square) ![인턴](https://img.shields.io/badge/텐핑거스%20AI%20인턴-9c6b30?style=flat-square) ![단독개발](https://img.shields.io/badge/단독%20개발-9c6b30?style=flat-square)

**Problem** — 영업팀이 수작업으로 하던 신규 매장 발굴을 자동화해야 했다.
**Solution** — 데이터 수집(Selenium 크롤러) → XGBoost 인기도 예측 → SBERT 유사도 → ML+LLM(Gemini) 카테고리 매칭 → QC Score → API로 이어지는 파이프라인. 기획부터 배포까지 개발 전 과정 단독 수행.
**Result** — 제휴점 기준 내부 매칭 검수에서 카테고리 매칭률을 약 15%(ML 단독) → 약 80%(ML+LLM)로 개선. **ICT 학점연계 프로젝트 인턴십 우수성과 개인 부문 장려상** 수상.
**Limitation** — 유사도만으로는 신규 후보를 못 찾는 한계를 확인 → 인기도 예측·제휴 가능성·LLM 카테고리 분류를 분리. 위 수치는 고정 테스트셋 accuracy가 아닌 내부 검수 결과.

> 회사 코드·데이터는 비공개 → [Case Study](case-studies/eagle-eye.md)로 설계·역할만 정리

<br>

### 📊 [이미지 분류 & 표현학습 분석](https://github.com/gidaseul/machine-learning-project)

![ML](https://img.shields.io/badge/Classical%20ML-7b5fd1?style=flat-square) ![Representation](https://img.shields.io/badge/Representation%20Learning-7b5fd1?style=flat-square)

<a href="https://github.com/gidaseul/machine-learning-project">
  <img src="https://raw.githubusercontent.com/gidaseul/machine-learning-project/main/assets/images/representation-latent-evidence.png" width="480" alt="latent space 분석">
</a>

**Problem** — MNIST·SportsBall로 고전적 이미지 분류와 표현학습(Autoencoder/Contrastive)의 실제 성능 차이를 검증.
**Result** — 낮은 성능도 숨기지 않고 latent space·t-SNE로 원인까지 분석해 공개.

[GitHub](https://github.com/gidaseul/machine-learning-project)

<details>
<summary>다른 프로젝트 더 보기</summary>
<br>

- **후판 Scale 불량 예측** *(POSCO 청년 AI·Big Data 아카데미, 5인 팀장)* — 완전분리 문제를 일으킨 HSB 변수를 공정 규칙으로 재해석하고 파생변수를 설계. 팀 최종 XGBoost 후보 Precision 100% · Recall 95.88% · ROC-AUC 0.9883 (불량 97건 중 93건 검출, 팀 결과).
- **신용카드 사기 탐지** *(데이터사이언스 수업, 4인 팀장)* — 사기 비율 0.14%의 극단적 불균형 데이터에 샘플링 6종 × 모델 12종 = 144개 조합을 자동 비교하고, Accuracy 대신 미탐·오탐 비용함수로 최종 모델(ADASYN-BRF)을 선정.
- **[Brain MRI Research](https://github.com/gidaseul/brain-mri-research)** — VML 학부연구생. 3D MRI 볼륨을 `ResNet3D-18`로 학습하고 CAM으로 주목 영역을 시각화 (팀 baseline과 개인 기여 분리 표기).
- **[밥보기](https://github.com/gidaseul/babbogi)** — 섭취 기반 영양소 관리 앱. 5인 팀에서 **백엔드** 담당, `SavedFood` 검색·상세조회 기능을 커밋 단위로 구현 (2024 소프트웨어공모전 은상).
- **[Docent AI](https://github.com/gidaseul/tts)** — 관람객 수준별 RAG·LLM·TTS 도슨트 프로토타입.

</details>

---

## 🕓 Timeline — Experience & Awards

> `💼 경험` → `🧪 프로젝트` → `🏆 수상` 순서로, 활동과 그 결과를 같은 흐름에서 정리했습니다.

<table>
<tr><td width="90"><b>2019</b></td><td>🏆 <b>대한민국 인재상</b> — 부총리 겸 교육부장관상 · <a href="https://www.dmorning.kr/news/articleView.html?idxno=41872">기사</a></td></tr>
<tr><td><b>2020–25</b></td><td>🎓 <b>숭실대학교</b> 소프트웨어학과 · 인공지능·빅데이터융합 전공</td></tr>
<tr><td rowspan="3"><b>2021–22</b></td><td>💼 <b>Syncorbis</b> Bio & SW Engineer — <a href="https://doi.org/10.8080/1020210123255">생명과학 실험 자동화 장치 설계·특허</a></td></tr>
<tr><td>🏆 <b>전라남도 으뜸인재</b> 발탁 — 4학년 재능계발비 지원 (2021–25)</td></tr>
<tr><td>🏅 <b>SQLD</b> 취득 (2022)</td></tr>
<tr><td rowspan="5"><b>2024</b></td><td>💼 <a href="https://sites.google.com/view/vmllab/members"><b>VML Lab</b></a> 학부연구생 시작 — Computer Vision · Medical AI 연구</td></tr>
<tr><td>🧪 <b>밥보기</b> — 맞춤형 영양 관리 서비스, 5인 팀 백엔드 담당</td></tr>
<tr><td>🏆 <b>2024 소프트웨어공모전 은상</b> — 밥보기</td></tr>
<tr><td>🏆 <b>숭실대 프로그래밍대회(2024 SCON) 은상</b></td></tr>
<tr><td>🧪 실시간 낙상 감지 · 신용카드 사기 탐지 · 이미지 분류·표현학습 분석 프로젝트</td></tr>
<tr><td rowspan="6"><b>2025</b></td><td>💼 <b>(주)텐핑거스 ICT 인턴</b> — 매의 눈, 매장 AI 발굴·인기도 예측 파이프라인 단독 개발</td></tr>
<tr><td>🏆 <b>ICT 학점연계 프로젝트 인턴십 우수성과 개인 부문 장려상</b> — 매의 눈</td></tr>
<tr><td>💼 VML Lab 학부연구생 활동 종료 (2024.06–2025.02)</td></tr>
<tr><td>🧪 <b>LG Aimers 7기</b> — 수요 예측 프로젝트</td></tr>
<tr><td>👥 <b>GDG Soongsil 5기</b> Member (AI/ML)</td></tr>
<tr><td>🧪 숭실대 캡스톤 — Curiator AI 도슨트</td></tr>
<tr><td rowspan="6"><b>2026</b></td><td>🎓 <b>SSAFY 15기</b> 합격</td></tr>
<tr><td>💼 <b>POSCO 청년 AI·BigData 아카데미 33기</b> — 5인 팀장, 후판 품질 예측·AppleCare+ 병해 진단 프로젝트 (2026.05–07)</td></tr>
<tr><td>🏆 <b>우수상</b> — 청년 AI·BigData 아카데미 33기 개인 성적 우수</td></tr>
<tr><td>🏆 <b>협력상</b> — 청년 AI·BigData 아카데미 33기</td></tr>
<tr><td>🏆 <b>프로젝트 최우수상</b> — 청년 AI·BigData 아카데미 33기 B분반 3조 팀 수상</td></tr>
<tr><td>💼 <b>PIAI 인공지능 연구원 인턴</b> — 현재 근무 중</td></tr>
</table>

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

---

### 🛠 Languages & Tools

<p align="left">
<img height="28" alt="python" src="https://cdn.jsdelivr.net/gh/devicons/devicon@v2.15.1/icons/python/python-original.svg">
<img height="28" alt="pytorch" src="https://cdn.jsdelivr.net/gh/devicons/devicon@v2.15.1/icons/pytorch/pytorch-original.svg">
<img height="28" alt="tensorflow" src="https://cdn.jsdelivr.net/gh/devicons/devicon@v2.15.1/icons/tensorflow/tensorflow-original.svg">
<img height="28" alt="scikit-learn" src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/05/Scikit_learn_logo_small.svg/1200px-Scikit_learn_logo_small.svg.png">
<img height="28" alt="pandas" src="https://cdn.jsdelivr.net/gh/devicons/devicon@v2.15.1/icons/pandas/pandas-original.svg">
<img height="28" alt="fastapi" src="https://cdn.jsdelivr.net/gh/devicons/devicon@v2.15.1/icons/fastapi/fastapi-original.svg">
<img height="28" alt="docker" src="https://cdn.jsdelivr.net/gh/devicons/devicon@v2.15.1/icons/docker/docker-original-wordmark.svg">
<img height="28" alt="aws" src="https://cdn.jsdelivr.net/gh/devicons/devicon@v2.15.1/icons/amazonwebservices/amazonwebservices-original-wordmark.svg">
<img height="28" alt="java" src="https://cdn.jsdelivr.net/gh/devicons/devicon@v2.15.1/icons/java/java-original.svg">
<img height="28" alt="c" src="https://cdn.jsdelivr.net/gh/devicons/devicon@v2.15.1/icons/c/c-original.svg">
<img height="28" alt="mysql" src="https://cdn.jsdelivr.net/gh/devicons/devicon@v2.15.1/icons/mysql/mysql-original-wordmark.svg">
</p>

📫 [Velog](https://velog.io/@feelgi/posts) · [Tistory](https://feelgi.tistory.com/) · [Portfolio (Notion)](https://fragrant-cloudberry-f69.notion.site/1868017e41ad801fb28bff08bd094789) · [rlektmf0328@gmail.com](mailto:rlektmf0328@gmail.com)
