## 누가 A를 만드나?

아래 조건이 하나 이상 만족하면,
클래스B에게 인스턴스A를 만들 responsibility를 할당.

==B contains or aggregates A==. (B가 A를 포함하거나 집계한다.)
B가 A를 기록한다.
B가 A를 closely 사용한다.
B가 A의 data를 초기화한다.

예시.
![[Pasted image 20240618075503.png]]

**Discussion**
- responsibility 생성을 할당하는 가이드
- Contradiction : 생성에 상당한 복잡성이 필요할 수 있음. (singleton에게 위임하는 경우 있음.)
	성능 이유로 재활용 인스턴스 사용
	비슷한 클래스의 패밀리 중 하나에서 조건부로 인스턴스 생성
	sometimes desired to outsource object wiring (“dependency injection”)

**Benefit**
낮은 coupling

**관련있는 pattern**
- Abstract Factory
- Singleton