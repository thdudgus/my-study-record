---
aliases:
  - 회귀
---
supervised setting에서 **연속적인 input data**에 fitting되는 함수를 예측
![[Pasted image 20240510124350.png|400]]
**정의역과 치역의 관계를 정의하는 것.**

### 목표
independent variable과 dependent variable 사이의 관계를 모델링

### 알고리즘 : linear regression
best fits the data인 linear equation을 찾는 것.
![[Pasted image 20241009215907.png|300]]
 ŷ : dependent variable의 continuous prediction value
 x_i : independent value
 w_i : 각 independent value에 할당된 weight
##### 예시 : House price prediction
input : 새 집의 정보 (위치, 크기, 건설 연도, 방의 개수 등)
opuput : 새 집의 예측 가격

### 학습 과정 (learning process)
1. input으로 data D_train
	data point(x, y) 는 y를 x에 대한 [[ground-truth]] output이라고 specify한다.
	x = {x_1 : location, x_2 : hose size, ...}
	y : 실제 집의 가격

2. output ŷ (= ƒ_w(x))에 input을 mapping하는 predictor ƒ를 학습시킨다.![[스크린샷 2024-10-09 오후 10.39.31.png]]
##### 답에 대한 자연적 의문
1. **x의 어떤 feature들이 y를 예측하는 데에 중요할까?**
	example : house price prediction
		house x의 가격을 예측하기 위해서 x는 다양한 feature을 가질 수 있음.
		x의 어떤 feature가 실제 y를 예측할 때 중요할까?
		**feature extraction**
		input x가 주어졌을 때 [feature name : feature value] pair의 set을 extract![[스크린샷 2024-10-09 오후 11.03.21.png]]
		feature는 vector로 나타낼 수 있음 ~= high-dimensional space의 point
		각 feature_i에 대해서, 우리는 y 예측에 contributiion을 나타내는 실수 w_i를 가질 수 있음.![[스크린샷 2024-10-09 오후 11.08.27.png]]
2. **모델을 어떻게 평가하고 최적화할 것인가?** 
	**(예측한 값이 실제 값과 얼마나 가까운지 어떻게 알 수 있을까?)**
![[스크린샷 2024-10-09 오후 10.41.53.png]]
1) best feature를 extract
2) best wight을 assign

- **Loss Function** 𝐿 (𝑥, 𝑦, 𝐰)
	input (x, y)와 weight vector **𝐰**가 주어졌을 때, x에 대한 예측이 얼마나 불만족스러운지 정량화 => ==모델의 예측 output과 실제 output의 차이를 측정하는 함수==
	
	일반적인 loss fuctions 
	- Least squared
		![[스크린샷 2024-10-10 오전 12.02.21.png|200]]
	- logistic
	- hinge
	- cross-entropy, … 
![[스크린샷 2024-10-10 오전 12.05.40.png|400]]

- **Training loss**
	모델의 성능을 평가하기 위함.
	![[스크린샷 2024-10-10 오전 12.07.29.png|400]]
	어떻게 **training loss를 최소화**하는 weight vector **w**를 찾을 수 있을까?
		=> **최적화 알고리즘**을 사용하는 것. 
			예를 들어 **[[gradient descent]]**와 같은 방법을 통해 loss function의 기울기를 계산하고, 이를 기반으로 weight를 반복적으로 업데이트하여 loss를 줄여나간다.

