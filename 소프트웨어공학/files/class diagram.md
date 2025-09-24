- instace variable(=attribute) : instance level에서 정의된 attribute
- class variable(=class attribute, static attribute)
- class operation

class variable과 class operation은 밑줄로 표시한다.

![[Pasted image 20240423121914.png]]   


## Abstract Class (추상 클래스)
abstract operation : body가 없는 operation
concrete operation : body가 있음.  

abstract class : 초기화되지 않은 class (instance 생성 x)
concrete class : 초기화됨.   

abstract operation이 있으면 abstract class이다.
abstract opeation이 없으면 abstract class일 수도 있다.

### UML에서의 표기
- class (택1)
	- 이탤릭체
	-  <\<abstract>>
	- {abstract}

- operation (택1)
	- 이탤릭체
	-  {abstract}

![[Pasted image 20240423123136.png]]   



## Interface
![[Pasted image 20240423124332.png]]   
provided interface : 제공자가 ball symbol이랑 connector를 갖고 있음.
requirede interface : timer가 observer를 필요로 해서, timer가 observer쪽으로 뻗고 있음.   


## 클래스 관계의 유형
![[Pasted image 20240423124908.png]]   
표식이 있는 쪽이 큼.

aggregation의 경우 lab ◇0...1----------* stundet : student가 lab의 part이다.
	lab이 사라져도 student가 사라지지 않음.

composition의 경우 building ◆1---------* lecturehall ◆0..1---------* beamer : beamer는 lecturehall의 part, lecturehall은 building의 part이다.
	building이 삭제되면 lecturehall도 삭제된다.



## text를 Class diagram으로 바꾸기
- 명사 -> 클래스 이름
- 형용사 -> attribute
- 동사 -> operaion

두 클래스 간의 ralationship이 하나일 필요 없음.   


## Code Generation
![[Pasted image 20240423144839.png]]   
ralationship 관계에 있는 class의 instance도 적기
\*이면 배열\[ ]로 작성
1이면 instance로 작성

association class는 Hashtable로 작성. (같이 연결된 class는 key, association class는 value : 코드엔 주석으로 나타내면 됨.)