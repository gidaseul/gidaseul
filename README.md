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

![CV](https://img.shields.io/badge/CV-e8722c?style=flat-square) ![VLM](https://img.shields.io/badge/VLM-e8722c?style=flat-square) ![RAG](https://img.shields.io/badge/RAG-e8722c?style=flat-square) ![LIVE](https://img.shields.io/badge/●%20LIVE-1a9c4c?style=flat-square)

**Problem** — 드론 촬영 이미지를 사람이 일일이 보고 병해를 판단해야 했다.
**Solution** — 분류 → DINO → Grad-CAM → VLM → RAG로 이어 구역·나무·잎 단위 병해 리포트를 자동 생성.
**Result** — 화면과 모델을 JSON 계약으로 분리해, 실제 추론 서버를 붙일 때 화면 코드는 건드리지 않도록 설계.

[**▶ 라이브 데모**](https://applecare-orchard.vercel.app/) · [GitHub](https://github.com/gidaseul/applecare-orchard) *(현재 비공개 저장소)*

<br>

### 🚶 [실시간 낙상 감지](https://github.com/gidaseul/capstone_pose)

![CV](https://img.shields.io/badge/Computer%20Vision-2f6fed?style=flat-square) ![팀리드](https://img.shields.io/badge/캡스톤%20팀%20리드-2f6fed?style=flat-square)

<a href="https://github.com/gidaseul/capstone_pose">
  <img src="https://github.com/user-attachments/assets/e9b5b0ab-ff87-478e-a8c1-96cbd2d7cbf1" width="480" alt="실시간 낙상 감지 데모">
</a>

**Problem** — RGB 카메라만으로 낙상을 감지해야 하는 캡스톤 과제 (웨어러블 없음).
**Solution** — YOLO로 사람 검출 → MediaPipe 관절 추출 → LSTM 시계열 분류의 2단계 구조.
**Result** — 오래된 프레임이 쌓이지 않게 프로세스 큐를 1개로 제한해 최신 프레임을 우선 처리.

[GitHub](https://github.com/gidaseul/capstone_pose)

<br>

### 🦅 매의 눈 — 잠재 매장 발굴

![Applied AI](https://img.shields.io/badge/Applied%20AI-9c6b30?style=flat-square) ![인턴](https://img.shields.io/badge/텐핑거스%20AI%20인턴-9c6b30?style=flat-square) ![단독개발](https://img.shields.io/badge/단독%20개발-9c6b30?style=flat-square)

**Problem** — 영업팀이 수작업으로 하던 신규 매장 발굴을 자동화해야 했다.
**Solution** — 데이터 수집 → ML/LLM 분류 → QC Score → API 파이프라인으로 전환.
**Limitation** — 유사도만으로는 신규 후보를 못 찾는 한계를 확인 → 인기도 예측·제휴 가능성·LLM 카테고리 분류를 분리.

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

- **[Brain MRI Research](https://github.com/gidaseul/brain-mri-research)** — VML 학부연구생. 3D MRI 볼륨을 `ResNet3D-18`로 학습하고 CAM으로 주목 영역을 시각화 (팀 baseline과 개인 기여 분리 표기).
- **[밥보기](https://github.com/gidaseul/babbogi)** — 섭취 기반 영양소 관리 앱. 4인 팀에서 **백엔드/서버 연동** 담당 (2024 소프트웨어공모전 은상).
- **[Docent AI](https://github.com/gidaseul/tts)** — 관람객 수준별 RAG·LLM·TTS 도슨트 프로토타입.

</details>

---

## 🏆 Awards

| 대회 | 수상 | 기간 |
| --- | --- | --- |
| 2019 대한민국 인재상 | 부총리 겸 교육부장관상 · [기사](https://www.dmorning.kr/news/articleView.html?idxno=41872) | 2019 |
| 제2회 전라남도 으뜸인재 발탁 | [전남인재평생교육진흥원](https://www.jntle.kr/main/uBusiness9) (4학년 재능계발비 지원) | 2021~2025 |
| 2024 소프트웨어공모전 (밥보기) | 은상 | 2024 |
| 숭실대 프로그래밍대회 (2024 SCON) | 은상 | 2024 |

## 💼 Experience

| 소속 | 활동 | 기간 |
| --- | --- | --- |
| **(주)텐핑거스** ICT 인턴 | 매의 눈 — 매장 AI 발굴·인기도 예측 파이프라인 (단독 개발) | 2025.03~06 |
| **[VML Lab](https://sites.google.com/view/vmllab/members)** 학부연구생 | Computer Vision · Medical AI 연구 | 2024.06~2025.02 |
| **Syncorbis** Bio & SW Engineer | [생명 자동화 실험기기 설계·기획](https://doi.org/10.8080/1020210123255) | 2021.03~2022.03 |
| 숭실대학교 | 소프트웨어학과 · 빅데이터융합 전공 | 2020.03~2025.02 |

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
