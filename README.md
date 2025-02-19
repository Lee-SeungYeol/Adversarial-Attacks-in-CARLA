# 모방학습 기반 자율주행 자동차에 대한 적대적 공격 및 대응 방안

## 1. 프로젝트의 개요
### 1-1. 프로젝트 개발 배경

&nbsp;&nbsp;&nbsp;&nbsp;최근 자율주행 자동차의 ADAS(Advanced Driver Assistance System)은 다양한 센서 기술들을 통해 주행환경에 대한 실시간 데이터를 분석하여 딥러닝 모델을 통해 상황을 분석하고 차량의 제어를 수행함
그러나 일부 연구에 따르면 딥러닝 모델이 Adversarial attack에 취약하다는 것이 밝혀져 이에 대한 연구 개발은 필수적이다.

&nbsp;&nbsp;&nbsp;&nbsp;따라서 본 프로젝트에서는 자율주행 시뮬레이션인 CARLA(CAR Learning to Act)를 이용하여 모방학습 기반의 딥러닝 모델을 구축한다. 그 후 시뮬레이션에 Adversarial attacks를 적용하여 공격 성공률을 평가한 뒤 차량의 주행 여부를 판단한다. 마지막으로 Adversarial attacks에 대응하기 위해 Feature Squeezing, Adversarial Training, Gradient Sign Inversion을 실험한 후 Gradient Removal Module을 적용하여 공격 성공률을 평가하고 자율주행 자동차가 정상 주행 하도록 도와준다.

### 1-2. 프로젝트 목표 및 주요 기능
### 최종 목표 : 공격 받고 있는 자율주행 자동차를 정상주행 할수 있는 방어 개발
#### 공격 알고리즘

| 알고리즘 | 설명 |
|-------------|-------|
| BIM   | Iterative Fast Gradient Sign Method. FGSM을 반복적으로 적용하여 공격을 수행하는 방법. |
| MI-FGSM  | 모멘텀을 이용하여 적대적 샘플을 생서하는 공격 기법 |
| PGD      | Projected Gradient Descent. BIM과 유사하지만, 각 단계에서 공격이 제한된 범위 내에 있도록 프로젝션을 적용. |
| CW       | Carlini & Wagner Attack. $L_1, L_2, L_\infty$를 이용하여 적대적 샘플과 원본 입력 데이터의 거리를 계산하여 공격을 수행|
| OPT      | Optimization-based Attack. 최적화 기법을 사용하여 공격을 수행하는 방법. |
| BPDA     | Backward Pass Differentiable Approximation. 비차분 가능한 함수를 근사하여 공격을 수행하는 방법. |

## 2. 개발 환경 및 개발 언어

|  | tools |
|-------------|-------|
| 개발 언어   |![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white) |


![Image](https://github.com/user-attachments/assets/845dc385-736e-44a0-a36d-36ef0f296fbc)
