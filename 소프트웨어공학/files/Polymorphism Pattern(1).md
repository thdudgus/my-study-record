## type에 따라 behavior가 다를 때 누가 responsibility를 할당 받을 것인가?

관련 대안이나 동작이 클래스 별로 다를 경우 polymorphic operations를 사용하여 responsibility를 할당.

**Benefit**
- 명시적인 selection logic을 사용하는 것보다 reliable하고 쉽다.
- 추가적인 behavior를 나중에 추가하기 쉽다.

**Cost**
- 클래스 디자인 수가 증가한다.
- 코드를 따라하기 어렵게 만든다.

**Discussion**
- 아직 알려지지 잠재적인 미래의 변동을 대비하여, future-proofing를 과도하게 사용하지 않도록 한다.
	- Agile approach : 중요한 “upfront design”가 없고, 필요한 경우에만 변동 지점을 추가한다.
