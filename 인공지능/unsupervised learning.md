---
aliases:
  - 비지도 학습
  - 비지도학습
---
### unlabeled data로 훈련된 모델
각 data point는 explicit한 label이나 outcome을 가지지 않는다. 

### 목표
data의 보이지 않는(latent) 관계나 패턴을 찾는 것

### application
unlabed data에서 interesting point를 extract
- clustering
- dimension reduction
- association
- etc..

![[스크린샷 2024-09-26 오후 3.52.39.png|200]]
![[Pasted image 20241008142603.png]]

### 장점
- labeld data가 부족하거나 사용할 수 없는 시나리오에 적용 가능
- labeld example 없이 data 안에서 숨어있는 패턴과 구조를 찾아냄
- 다양한 data type과 domain을 다루는 flexibility

### 단점
- 모델 성능을 평가하기 위한 객관적인 metrics(지표)가 비효율적
- 학습된 패턴과 구조를 validating하고 interpreting하는 것이 어려움
- data outliers(데이터 이상치)와 노이즈에 민감함.