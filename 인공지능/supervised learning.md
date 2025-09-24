---
aliases:
  - 지도학습
  - 지도 학습
---
### labeld data로 훈련된 모델
각 data point는 corresponding label이나 outcome을 갖는다.

### 목표
input data를 기반으로 output을 예측하는 것.

### application
- [[regression]]
- [[classification]]
- etc..

### 활용
- spam filtering
- image classification
- news recommendation
- medical diagnosis
- etc..
![[스크린샷 2024-09-26 오후 4.00.28.png]]

### 장점
- data의 복잡한 패턴이나 관계 파악 가능
- Well-established models and algorithms available
- (with lables)model performance을 평가하기에 clear한 객관적 지표(objective metrics)
- 학습된 패턴의 interpretability(해석 가능성)

### 단점
- labed datad에 의존 (실제 세계에 labeld data가 많이 없어서.)
- cost가 크고, time-consuming인 labeling process (even with noise)
- 보이지 않는 data에 대한 제한된 generalization (training data에 [[overfit|overfitting]] 될 수 있음)



### 특징 Summary
![[스크린샷 2024-10-10 오후 11.27.03.png]]


## Supervised Learning의 과정
- [[preparing data]]
- [[designing model]]
- [[defining a loss function]]
- [[model optimization]]

