# 이미지 분류와 표현학습

숭실대 머신러닝 수업 팀 프로젝트. MNIST 손글씨와 SportsBall 사진에 고전적 분류와 CNN 기반 표현학습을 적용했습니다. 저는 SportsBall의 관심 영역(ROI) 추출, 전처리 순서, HOG·색상 특징 조합을 별도로 실험했습니다. [프로젝트 저장소](https://github.com/gidaseul/machine-learning-project)

## 어디부터 읽으면 되나

```text
machine-learning-project/
├── ML_1/                           고전적 분류 팀 보고서와 결과
├── ML_1(개인적으로 진행한 실험과정)/   SportsBall 전처리와 모델 비교 기록
├── ML_2/                           CNN·표현학습 팀 보고서와 평가 범위
├── datas/                          MNIST·SportsBall의 수업용 데이터 분할
├── mnist/mnist_latent_feature.ipynb  손글씨 특징 추출과 시각화
└── sportsball/
    ├── sportsball.ipynb             CNN 기준 모델 학습
    ├── sportsball_latent_feature.ipynb  특징 벡터 추출과 t-SNE
    └── vae_latent.ipynb             복원·분류·대조 손실을 섞은 실험
```

## 공을 잘라내는 단계에서 생긴 문제

SportsBall은 화면에서 공의 위치와 배경이 제각각입니다. 윤곽과 바운딩 박스로 공이 있을 영역을 자른 뒤, HOG와 색상 히스토그램을 추출해 분류기에 전달했습니다. 공 대신 배경이 잘리면 두 특징 모두 엉뚱한 영역을 요약합니다. 팀 보고서는 이런 오분류를 확인했고, XGBoost의 교차검증 정확도와 별도 테스트 정확도를 각각 약 65%, 약 37%로 기록했습니다.

![SportsBall 원본과 전처리 결과, 선택된 관심 영역](https://raw.githubusercontent.com/gidaseul/machine-learning-project/60abed6f6827e83f1399edec7c21b424351dcb33/assets/images/classical-roi-evidence.png)

[ROI 처리와 모델 비교 기록](https://github.com/gidaseul/machine-learning-project/blob/main/ML_1/README.md)

## CNN이 배운 특징을 확인하는 방법

CNN의 중간 특징을 뽑아 t-SNE로 2차원에 투영하고 정답 클래스에 따라 색을 입혔습니다. MNIST에서는 같은 색이 모이는 구간이 뚜렷했고, SportsBall에서는 클래스가 더 많이 섞였습니다. 그림으로 어느 클래스가 겹치는지 살피고, 성능 비교는 별도 평가 수치로 읽었습니다.

공개 CNN 노트북 일부에서는 테스트 손실로 체크포인트를 선택했습니다. 독립 성능을 다시 측정하려면 학습에서 검증 세트를 분리하고, 테스트 세트는 모델 선택이 끝난 뒤 평가합니다. [실험 노트북과 t-SNE 그림](https://github.com/gidaseul/machine-learning-project/blob/main/ML_2/README.md#evidence) · [재현 시 유의점](https://github.com/gidaseul/machine-learning-project/blob/main/ML_2/README.md#notes-before-reproducing)

[프로필의 더 살펴볼 프로젝트로 돌아가기](../README.md#더-살펴볼-프로젝트)
