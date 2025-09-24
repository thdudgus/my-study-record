## UI layer 너머 system operation을 수신하고 coordinate("control")하는 첫번째 object는 무엇인가?

다음 옵션 중 하나를 나타내는 object에 responsibility 할당
옵션 1 : 전체 system, root object, 소프트웨어가 실행 중인 device 또는 주요 subsystem (facade controller)
옵션 2 : system operation이 발생하는 use case scenario (use case or session controller)

**Discussion**
너무 많은 responsibility를 가져 overload되면, controller class는 bloated된다.
- 컨트롤러 추가(Facade -> Use-Case 컨트롤러)
- 다른 object에 위임.

**Benefit**
- GUI에 애플리케이션 로직이 없음. -> 재사용 가능한 component 증가의 가능성
- use case의 상태에 대한 이유
	- operation이 특정 순서로 실행되어야 useful.
	예) EndSale이 발생할 때까지 MakePay가 발생할 수 없다.

