[[logical architecture]]를 나타낸다.
- layer, subsystem, package 등..
- ex) UI layer는 UI라고 하는 package로 모델링된다.

UML 패키지는 클래스, 기타 패키지, 사용 사례 등 모든 것을 그룹화할 수 있다.
- nesting package는 매우 일반적.
- UML 패키지는 단순한 Java 패키지나 .NET namespace보다 더 일반적인 개념이지만 UML 패키지는 이를 나타낼 수 있습니다.



## Benefits of Using Layers
- 일반적으로, concern의 separation, high from low level services의 separation, 애플리케이션 별 서비스 분리.
	- 이를 통해 coupling과 dependency를 줄이고 cohesion과 reusability, clarity를 높일 수 있다.

- 관련 complexity은 캡슐화되고 decomposable하다.

- 몇몇 layer는 새로운 implementation으로 대체될 수 있다.
	- 일반적으로 low level의 기술 서비스나 foundation layer에선 불가능하지만 UI, application, domain layer에선 가능하다.

- 일부 layer(주로 domain과 technique service)를 분산시킬 수 있다.

- logical segmentation으로 인해 팀 개발에 맞춰져있다.


## Domain Layer and Domain Objects
![[Pasted image 20240618070941.png]]
![[Pasted image 20240618071007.png]]
![[Pasted image 20240618071042.png]]
tier : a physical processing node
layer : the vertical slices of the system

## Model View Separation Principle
![[Pasted image 20240618071252.png]]
UI 변경이 logic 쪽으로 영향이 가지 않도록 해야 함.