# 모방학습 기반 자율주행 자동차에 대한 적대적 공격 및 대응 방안

## 1. 프로젝트의 개요
### 1-1. 프로젝트 개발 배경


&nbsp;*8최근 자율주행 자동차의 ADAS(Advanced Driver Assistance System)은 다양한 센서 기술들을 통해 주행환경에 대한 실시간 데이터를 분석하여 딥러닝 모델을 통해 상황을 분석하고 차량의 제어를 수행함
그러나 일부 연구에 따르면 딥러닝 모델이 Adversarial attack에 취약하다는 것이 밝혀져 이에 대한 연구 개발은 필수적이다.

>  따라서 본 프로젝트에서는 자율주행 시뮬레이션인 CARLA(CAR Learning to Act)를 이용하여 모방학습 기반의 딥러닝 모델을 구축한다. 그 후 시뮬레이션에 Adversarial attacks를 적용하여 공격 성공률을 평가한 뒤 차량의 주행 여부를 판단한다. 마지막으로 Adversarial attacks에 대응하기 위해 Feature Squeezing, Adversarial Training, Gradient Sign Inversion을 실험한 후 Gradient Removal Module을 적용하여 공격 성공률을 평가하고 자율주행 자동차가 정상 주행 하도록 도와준다.


![Image](https://github.com/user-attachments/assets/845dc385-736e-44a0-a36d-36ef0f296fbc)
