## object에 responsibility를 부여하는 기본 원칙은 무엇인가?

fulfill(이행)에 필요한 information을 가지고 있는 class에 responsibility를 부여한다.

예시.
![[Pasted image 20240618080402.png]]
sale ------ saleslineitem -------discription
총판매 가격을 구하는 건 누가 해야하는가 + GRASP을 이용하여 설명
Sale : Due to its low complexity, the corresponding operation can be performed with one method.

**Discussion**
responsibility를 할당하는 데 있어서 가장 많이 사용되는 원칙.
- information이 여러 object에 걸쳐서 퍼진다. => interact가 필요하게 됨.
- Caution : separation of concern과 conflict가 생길 수 있다. ![[Pasted image 20240618080803.png]]

**Benefit**
information 캡슐화로 coupling이 낮아진다.