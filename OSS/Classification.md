---
aliases:
  - 클래시피케이션
  - 분류
---

supervised setting에서 training data set의 분포와 label에 따른 **결정 영역(decision boundary) 생성**
![[Pasted image 20240510124213.png|300]]    ![[스크린샷 2024-09-26 오후 3.51.49.png|200]]

### Algorithm : logistic regression
classification의 알고리즘 중 하나. (이름에 regression이 들어간 것 뿐)
- regression for binary classification 
	- sigmoid 함수를 사용해서 주어진 input이 particular class에 속해있는지에 대한 확률을 계산한다.
		=> binary/categorical(discrete) outcome을 확률을 기반으로 예측
- 수학적인 관점에서 **data를 best classify하는 boundary를 찾는 것.**
![[스크린샷 2024-10-10 오후 4.29.44.png]]
##### email spam filter 예시
input : email information (IP address, title, body, sender,...)
output : a particular class (spam인지 아닌지)
	email이 spam인지 아닌지 예측하기 위해 모델 ƒ를 훈련
	ŷ = 𝑓_𝐰(𝑥) = 𝐬𝐢𝐠𝐧(𝑝(𝑦 = 1|𝑥; 𝐰)) =
	- +1 (if 𝑝 ≥ 𝜃)
	- −1 (if 𝑝 < 𝜃 , e.g., (𝜃 = 0.5))
		input 𝑥 = {email, message, sender, receiver, ...}, 𝑦 ∈ {spam (1), not−spam (−1)}
		output ŷ ∈ {spam(1), not-spam(-1)} (i.e., labels)
![[스크린샷 2024-10-10 오후 4.37.14.png|250]]


### loss function 𝐿(𝑥, 𝑦, 𝐰)
logistic regression에서는 binary cross-entropy loss를 사용하여 모델의 예측 오류를 측정한다.
![[스크린샷 2024-10-10 오후 8.56.53.png]]
실제 label인 y_i가 1인 경우엔 log(ŷ_i)가 중요해지고
실제 label인 y_i가 0인 경우에는 log(1-ŷ_i)가 중요해짐 => 0인지 1인지에 따라 다른 부분이 활성화 됨.

![[스크린샷 2024-10-10 오후 10.52.21.png]]
	<노란 그래프>
	실제 label인 y_i가 1인 경우 loss function은 y_i\*log(ŷ_i)항만 남게 된다. 
	모델이 예측한 확률 ŷ_i이 1에 가까울수록 log(ŷ_i)은 0에 가까워져 loss가 감소한다.
	 반면 모델이 예측한 확률 ŷ_i이 0에 가까울수록 log(ŷ_i)은 음의 무한대로 발산하며 loss가 증가한다.
	 <파란 그래프>
	 실제 label인 y_i가 0인 경우 loss function은 (1-y_i)\*log(1-ŷ_i)항만 남게 된다. 
	모델이 예측한 확률 ŷ_i이 1에 가까울수록 log(1-ŷ_i)은 음의 무한대로 발산하며 loss가 증가한다.
	 반면 모델이 예측한 확률 ŷ_i이 0에 가까울수록 log(1-ŷ_i)은 0에 가까워져 loss가 감소한다.

