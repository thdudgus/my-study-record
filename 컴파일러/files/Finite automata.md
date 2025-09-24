[[token]] 식별을 위한 구현.   
[[Regular expression]]으로 sepecified된 pattern을 기반으로 input을 accept하거나 reject한다.   
<br>   
A finite automata 𝑴 = {𝑸,𝚺,𝜹,𝒒𝟎,𝑭}   
- A finite set of states 𝑄 = {𝑞0,𝑞1,𝑞2,…,𝑞𝑖}    
- An input alphabet Σ = a finite set of input symbols    
- A start state 𝑞0     
- A set of accepting (or final) states 𝐹 which is a subset of 𝑄    
	-> accepting하는 state (or fiinal) 𝐹는 𝑄의 subset이다.    
- A set of state transition functions 𝛿   
	e.g., 𝛿(𝑞0, 𝑎) = 𝑞1 : the state transition from 𝑞0 to 𝑞1 on the input symbol 𝑎   
	-> 𝑞0에서 input 𝑎를 읽어 𝑞1로 transition한다.     
<br>
### [[DFA]] VS [[NFA]]
![[Pasted image 20240414215341.png]]   
<br>

