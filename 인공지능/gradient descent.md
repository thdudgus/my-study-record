training loss를 최소화
1. 랜덤으로 𝐰를 initialize
2. 아래 equation을 기반으로 𝐰를 반복적으로 업데이트
	𝐰 = 𝐰 − 𝜂 ∇_𝐰 𝑇𝑟𝑎𝑖𝑛𝐿𝑜𝑠𝑠 (𝐰)
		∇_𝐰 𝑇𝑟𝑎𝑖𝑛𝐿𝑜𝑠𝑠 (𝐰) : gradient(loss가 increase하는 방향)
			우리가 weight의 변화를 줄 때 loss function은 얼마나 변하나? 
		𝜂 : learninf rate (step size)
		![[스크린샷 2024-10-10 오후 12.43.13.png]]

### Discussion
각 iteration에서 total training loss는 감소한다. (이전의 gradient와 비교해서)
=> **그렇다면 모든 점에서 각 gradient step 후에 happy한가?**
	어떤 점에선 업데이트 하기 전에 이미 가까운데, GD 후에 멀어지기도 함.
	(모델의 예측이 전체 data에 대해 더 나은 방향으로 나아가도록 weight를 업데이트 하지만 **개별 data point의 loss가 항상 감소하는 것은 아님. 오히려 loss가 증가하기도 함.**)
	![[스크린샷 2024-10-10 오후 2.15.24.png|350]]
	우리는 모든 iteration에서 모든 data를 고려해야한다.
	=> 시간과 비용이 많이 듦. 특히 데이터가 많을 때.


### stochastic gradient descent
gradient descent는 한번으로 업데이트 되는 모델이 아니다.
각 data point(x, y)에서, 모델을 업데이트한다. (모든 data point 아님.)
![[스크린샷 2024-10-10 오후 2.24.11.png]]

#### stochastic gradient descent의 한계
- **느린 progress :** steep(가파른) 방향으로 흐트러질 수 있음.
- **local minima :**  local minima에 도달할 수도 있음. (매번의 업데이트가 랜덤으로 이루어지기 때문에 loss function의 복잡한 형태에 따라 logical minima에 빠질 수 있다. logical minima은 global minimum과 달리 loss function가 충분히 낮지 않은 지점일 수 있음.)![[스크린샷 2024-10-10 오후 2.48.18.png]]
=> **이러한 한계를 극복하기 위해 momentum을 이용한다.**
	gradient의 running mean을 "velocity"라고 build up
	=> velocity를 기울기의 이동 평균으로 누적하는 것.
	기울기 정보 뿐 아니라 이전 단계의 업데이트 방향을 함께 고려하여 가중치 조정
	![[스크린샷 2024-10-10 오후 3.06.58.png]]
	여기서 학습률 𝜂 (= learning rate)은 매 iteration마다 loss function의 최솟값을 향해 이동할 때 step size의 크기를 결정한다.
	learning rate는 너무 작아도 커도 문제일 수 있어서 적절한 값을 찾아야 한다.
	![[스크린샷 2024-10-10 오후 3.41.13.png]]
	