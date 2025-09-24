shift-reduce parsing을 하는 동안 나타날 수 있는, acceptable한 input string의 left substring

파싱 과정에서 파서가 아직 입력을 모두 확인하지 않았음에도, 그동안 읽은 입력이 문법적으로 유효한 구문을 형성할 수 있는 접두어.
컴파일러가 소스 코드를 구문 분석할 때, 아직 읽지 않은 나머지 부분에 관계없이 **현재까지 읽은 부분이 잠재적으로 유효한 구문의 시작 부분을 나타낼 때 이를 'viable prefix'라고 한다.**

𝛼|𝛽의 경우, 𝛼 = 𝑝𝑟𝑒𝑓𝑖𝑥1𝑝𝑟𝑒𝑓𝑖𝑥2 … 𝑝𝑟𝑒𝑓𝑖𝑥𝑛이다.(여기서 𝑖번째 𝑝𝑟𝑒𝑓𝑖𝑥가 production의 RHS), 
1 ≤ 𝑘 < 𝑛인 𝑝𝑟𝑒𝑓𝑖𝑥는 handle이 아니고,(production의 불완전한 RHS와 매치) 𝑛번째 𝑝𝑟𝑒𝑓𝑖𝑥가 handle이라면, reduce한다.
𝑛번째 𝑝𝑟𝑒𝑓𝑖𝑥가 [[handle]]이 아니라면,  𝑛번째 𝑝𝑟𝑒𝑓𝑖𝑥는 reduce된 𝑛+1, 𝑛+2, ... 번째 𝑝𝑟𝑒𝑓𝑖𝑥의 output과 concatenate되고 handle이 된다.

![[Pasted image 20240518172326.png|250]]

### left string αβ가 viable prefix인 상황에서, αβ|bω인 경우
X -> β인 production이 있고, αX가 viable prefix면, β는 αβbω의 handle이다. => reduction 진행
αβ가 handle이 아니라면, αβb가 viable prefix이다. => shift 진행
그렇지 않으면 reject

### viable prefix의 set은 regular language이다.
=> viable prefix는 finite automata를 사용해 인식될 수 있다. 