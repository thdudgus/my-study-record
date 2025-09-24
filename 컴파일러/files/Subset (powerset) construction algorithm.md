Basic Idea : 어떤 input string이 들어오면, 도달 가능한 NFA state들의 집합으로 grouping   
	어떤 input string이 나왔을 때 나올 수 있는 NFA의 요소들로 적절한 DFA state를 찾는 것.   

ε-closure(A) : A state로부터 ε-move로 transition할 수 있는 모든 set   
![[Pasted image 20240414234730.png]]  
Step1   
	𝜖-𝒄𝒍𝒐𝒔𝒖𝒓𝒆(𝒒𝟎)을 계산한다. -> T0   
Step2   
	input symbol s in Σ마다 𝜖-𝒄𝒍𝒐𝒔𝒖𝒓𝒆 𝜹(𝑻𝟎,𝒔)를 계산한다.   
Step3   
	더 이상 새로운 결과가 나오지 않을 때까지, 각 NFA state Ti의 새로운 집합마다 Step2를 반복한다.   

![[Pasted image 20240414235303.png]]
![[Pasted image 20240414235225.png]]
![[Pasted image 20240414235238.png]]

위 표를 이용하여 input string을 효과적으로 구별할 수 있다.   
![[Pasted image 20240414235533.png]]   
COMPARE를 나누고 sIdentifier로 classify할 수 있다.   
![[Pasted image 20240414235700.png]]   
![[Pasted image 20240414235714.png]]