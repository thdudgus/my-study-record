뒤에 parser로부터 인식되지 않은 string을 배제하더라도 기존에 인식된 string만 가지고 그 root node를 찾아나갈 수 있도록 함.

α|ω라는 input string이 있다.
α는 parser가 보았고, reduce될 수 있으며, terminal과 non-terminal을 포함하고 있다.
ω는 parser가 아직 보지 않았고, 오직 terminal만 포함하고 있다.

input string이 있으면 ω를 parser가 인지하지 않을 상태에서 처리를 수행하는 것.
이 때 α를 viable prefix이다. (선행자)

viable prefix는 regular expression으로 표현할 수 있는 regular language의 범주에 들어간다.
finite automata를 사용할 수 있다.
=> handle을 어떻게 판단하는지에 대한 답은 viable prefix가 regular language이기 때문에 finite automata를 적용할 수 있고, 그중에서도 확실한 답을 찾기 위해 deterministic finite automata를 쓰면 된다.




DFA를 구하기 위해서는 답이라고 생각할 수 있는 집합군이 바탕에 있어야 가능하다.
이걸 구해주는 건 DFA의 전 단계인 NFA이다. 이 NFA를 구하기 위해선 말 그대로 정답의 후보군을 나열해야 한다. 지금 수행하는 과정에선 grammar들의 production이다.
이걸 구하는 것은 LR(0)인데, 현재 LL(1)에서 나왔다시피 Lookahead를 나타내는 level이 0인 것이다. 즉, 선행으로 인식하는 과정 없이 현재 상태에서 item을 뽑는다는 것이다. 

예를 들어 ![[Pasted image 20240519001542.png|200]]
이걸로 파생될 수 있는 모든 item들을 바로 LR(0)로 뽑아낼 수 있다는 것이고, 보통 T -> T+E와 T -> (E)로 나누겠지만, LR(0)이 인식할 수 있는 모든 substring을 나열해야 되기 때문에 다음과 같이 구할 수 있다.
![[Pasted image 20240519001731.png|150]]
여기서 · 가 나타내는 것은 이전까지 LR(0)로 인식한 것이다. shift-reduce parsing에서 indicator가 움직이는 것과 비슷하다. 
결국 이 모든 것이 다 T를 표현하는 production이자 item인 것이다. 
여기에 special case인 X-> ε 이면 X-> · 라는 것을 포함시키면 LR(0)에 대한 item을 모두 구할 수 있고, 곧 이것이 다 grammar라 할 수 있을 것이다.

실례에서 적용시키면, 
![[Pasted image 20240519003848.png|300]]
위와 같은 production이 주어져 있는 상태에서 input으로 (int)가 들어왔다고 가정한다.
그러면 (int)에 대한 shift reduce parsing을 수행할 수 있는데 (int| )까지 shift를 수행하게 되면 여기서 (E| )로 reduction을 취할 수 있다. 
하지만, 우리가 shift reduce parsing을 마치려면, 정확히 close [[bracket]]인 ) 까지 읽어야 한다. 그런데 이 과정을 앞에서 언급한 viable prefix로 찾자는 의미이다. 그러면 앞에서 언급한 대로라면, 전체 (E)에서 (E는 T->(E)의 viable prefix라고 할 수 있다. 이렇게 앞에서 언급한 T에 대한 LR(0) item wnddptj (E에 해당하는 요소가 있는지를 찾아보는 것이다. 그러면 마지막 쯤에 T->(E.)가 있는 것을 볼 수 있고, 이걸 통해 DFA를 구하는 게 최종 결과물이 된다.

다른 예를 더 살펴보면,
위와 같이 정의되어 있는 item들이 있는데 input으로 (int\*int)가 들어왔다고 가정한다. 그러면 끝까지 다 parsing할 필요 없이 viable prefix를 사용하여 (int*|int)까지 하면 된다. 
그런 후 각각의 stirng에 대한 prefix를 정의해보면 맨 처음에 나오는 open bracket은 T->(E)에 대한 prefix라고 할 수 있고, 우리 눈엔 안 보이지만 (와 int 사이에 empty string도 존재한다. 앞의 정의에 따르면 empty string은 그냥 .에 대한 prefix라고 보면 된다. 이처럼 순차적으로 적용하면 다음과 같다.![[Pasted image 20240519153032.png|500]]
