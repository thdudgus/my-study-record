## change의 impact를 어떻게 줄일까?

여러 GRASP pattern이 충돌할 때 유용.

coupling을 낮추도록 responsibility를 할당.
이 pattern을 사용하여 대안을 평가한다.

예시.
![[Pasted image 20240618082034.png]]

**Discussion**
- 낮은 coupling은 디자인을 보다 independent하게 만들어 change에 대한 impact를 줄인다.
- 다른 패턴들과 함께 고려해야 한다.
- 안정적인 global object와의 높은 coupling은 문제가 없음.
	(ex. java.util)