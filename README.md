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
| 개발 언어   |![Python](https://img.shields.io/badge/Python-3.8.4-3776AB?logo=python&logoColor=white)|
| 사용 프레임워크| ![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white) |
| 가상 환경      | Carla 시뮬레이션|
| 개발 환경      |Windows 11      |

## 3. 시스템 구조도

&nbsp;&nbsp;&nbsp;&nbsp;가상환경에서 차량에 좌측, 중앙, 우측 카메라를 설치한뒤 주행하여 RGB 형태의 이미지 데이터와 command(좌회전, 우회전, 직진)를 수집하여 throttle, steering angle값을 라벨링 수행. steering angle 값이 0.0이 빈도수가 많아 under sampling과 over sampling을 수행하여 데이터를 조정
![image](https://github.com/user-attachments/assets/4c667e3f-8b27-4413-b43a-d9351cbc8f89)

&nbsp;&nbsp;&nbsp;&nbsp;입력되는 3개의 이미지는 Backbone modules(resnet18, mobilenet, vgg16)를 통해 처리되고 command는 speed modules를 통해 처리된후 각 계산 결과를 통합하여 steering angle과 throttle를 처리

<img src="https://github.com/user-attachments/assets/2d8b2d96-328a-4167-8ddf-7821c936c443"  width="600" height="400"/>

## 4. 정상 주행 확인
![Image](https://github.com/user-attachments/assets/355f8a29-f34b-4c91-b2f2-8b8d3f77aab6)

## 5. 각 방어 기법을 적용하여 공격 수행후 주행 확인



<div align="center">
  <table>
    <tr>
      <td align='Original Model'>
        <p>Original Model</p>
      </td>
      <td align="None Attack">
        <img src="https://github.com/user-attachments/assets/845dc385-736e-44a0-a36d-36ef0f296fbc" alt="Attack 1" width="200"/>
        <p>None Attack</p>
      </td>
      <td align="BIM">
        <img src="https://github.com/user-attachments/assets/a73cec50-3873-468b-8719-fc3b0fd708a1" alt="Attack 2" width="200"/>
        <p>BIM</p>
      </td>
      <td align="PGD">
        <img src="https://github.com/user-attachments/assets/a6226ee1-1b08-42ef-a4bd-7b7d959ce64d" alt="Attack 3" width="200"/>
        <p>PGD</p>
      </td>
      <td align="OPT">
        <img src="https://github.com/user-attachments/assets/2a50dbf5-c7ab-4ab8-8361-5c18efd7d46f" alt="Attack 4" width="200"/>
        <p>OPT</p>
      </td>
    </tr>
    <tr>
      <td align='Original Model'>
        <p>Original Model</p>
      </td>
      <td align="None Attack">
        <img src="https://github.com/user-attachments/assets/845dc385-736e-44a0-a36d-36ef0f296fbc" alt="Attack 1" width="200"/>
        <p>None Attack</p>
      </td>
      <td align="BIM">
        <img src="https://github.com/user-attachments/assets/a73cec50-3873-468b-8719-fc3b0fd708a1" alt="Attack 2" width="200"/>
        <p>BIM</p>
      </td>
      <td align="PGD">
        <img src="https://github.com/user-attachments/assets/a6226ee1-1b08-42ef-a4bd-7b7d959ce64d" alt="Attack 3" width="200"/>
        <p>PGD</p>
      </td>
      <td align="OPT">
        <img src="https://github.com/user-attachments/assets/2a50dbf5-c7ab-4ab8-8361-5c18efd7d46f" alt="Attack 4" width="200"/>
        <p>OPT</p>
      </td>
    </tr>
  </table>
</div>
