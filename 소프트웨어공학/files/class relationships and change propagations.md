---
클래스 관계:
---
## 클래스 관계의 유형
![[Pasted image 20240423124908.png]]   
표식이 있는 쪽이 큼.

aggregation의 경우 lab ◇0...1----------* stundet : student가 lab의 part이다.
	lab이 사라져도 student가 사라지지 않음.

composition의 경우 building ◆1---------* lecturehall ◆0..1---------* beamer : beamer는 lecturehall의 part, lecturehall은 building의 part이다.
	building이 삭제되면 lecturehall도 삭제된다.


![[Pasted image 20240618060800.png|500]]


## Information hiding
internal design decision을 숨기기 위한 설계 원칙
- internal design decision이 변경될 가능성이 높다.
- 따라서 향후 설계의 유지 또는 수정에 따른 부작용을 줄인다. design에서 다른 모듈에 대한 영향을 줄이는 것.
![[Pasted image 20240618061148.png|500]]

