# Physics-Informed Neural Networks (PINN) Study

Physics-Informed Neural Networks(PINN)를 이해하기 위해 기존 예제를 따라 구현하고, 제 학습 흐름에 맞게 수정·정리한 저장소입니다.

이 저장소는 Ben Tapley의 [PINN-example](https://github.com/bentaps/PINN-example)을 참고했습니다. 원본 예제는 감쇠 질량-스프링 시스템을 대상으로 PINN을 구성하고, 소수의 noisy data point와 물리 잔차 손실을 함께 사용해 시스템 파라미터를 학습하는 구조입니다.

저는 해당 예제를 바탕으로 PINN의 핵심 아이디어를 기계 시스템 관점에서 이해하고, 코드 흐름과 물리적 의미를 직접 따라가며 정리하는 데 목적을 두었습니다.

## Motivation

기계공학 문제에서는 운동방정식, 진동, 열전달, 유체역학처럼 물리 법칙이 명확한 경우가 많습니다. 하지만 실제 시스템에서는 측정 데이터가 부족하거나 노이즈가 포함되어 있고, 모든 조건을 해석적으로 모델링하기 어려운 경우도 많습니다.

PINN은 신경망 학습 과정에 물리 법칙을 직접 포함시켜, 데이터 기반 모델과 물리 기반 모델을 연결하는 방법입니다. 이 저장소는 향후 기계 시스템 해석, 진동 기반 고장 진단, PHM(Prognostics and Health Management), 물리 기반 머신러닝 연구로 확장하기 위한 기초 학습 기록입니다.

## Current Contents

- `mass_spring_system_solutions.ipynb`  
  감쇠 질량-스프링 시스템 예제를 바탕으로 PINN 구조를 학습한 노트북입니다.
  - 문제 설정
  - 질량-스프링-댐퍼 시스템의 지배방정식 이해
  - 신경망 모델 구성
  - 데이터 손실과 물리 잔차 손실 정의
  - 자동미분을 이용한 미분항 계산
  - 학습 결과 확인 및 해석

- `PINN.pdf`  
  PINN 개념과 예제 내용을 이해하기 위해 정리한 자료입니다.

- `requirements.txt`  
  노트북 실행에 필요한 Python 패키지 목록입니다.

## What I Focused On

이 저장소에서 중점적으로 이해하려고 한 부분은 다음과 같습니다.

1. PINN에서 물리 법칙이 손실 함수에 어떻게 들어가는지
2. 신경망 출력으로부터 자동미분을 통해 속도와 가속도를 계산하는 방식
3. 데이터 손실과 물리 잔차 손실의 역할 차이
4. 감쇠 질량-스프링 시스템의 미분방정식과 PINN 학습 과정의 연결
5. 기계 시스템 문제에 PINN을 적용할 때 어떤 확장이 가능한지

## Method

예제 시스템은 감쇠 질량-스프링 시스템입니다.

```text
x'' + μx' + kx = 0
```

PINN 학습에서는 다음 두 가지 손실을 함께 사용합니다.

1. 데이터 손실  
   관측 데이터와 신경망 예측값의 차이를 줄입니다.

2. 물리 잔차 손실  
   신경망 출력이 질량-스프링-댐퍼 시스템의 운동방정식을 만족하도록 합니다.

이를 통해 신경망이 단순히 데이터에 맞춰지는 것이 아니라, 주어진 물리 법칙을 따르는 해를 학습하도록 구성됩니다.

## Original Reference

This repository is based on the following open-source PINN example:

- Ben Tapley, [PINN-example](https://github.com/bentaps/PINN-example)
- Original notebook: [`mass-spring-system-solutions.ipynb`](https://github.com/bentaps/PINN-example/blob/main/mass-spring-system-solutions.ipynb)
- License: MIT License

## Planned Extensions

- 원본 예제의 코드 구조를 더 명확히 정리
- 감쇠계와 비감쇠계의 차이 비교
- 노이즈 수준에 따른 학습 결과 변화 확인
- 데이터 손실과 물리 손실의 가중치 변화 실험
- 진동 데이터 기반 시스템 식별 문제로 확장
- NASA Bearing Dataset 등 PHM 데이터셋 적용 검토

## Note

이 저장소는 개인 학습 및 연구 준비를 위한 프로젝트입니다. 원본 예제를 참고해 PINN의 구조를 이해하고, 기계공학 문제에 어떻게 확장할 수 있을지 탐색하는 과정으로 정리하고 있습니다.

