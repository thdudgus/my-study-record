---
인터페이스:
---
클래스들이 필수로 구현해야 하는 추상 자료형이다. 

interface는 아래 사항들을 제외하고 abstract class와 유사하다.
### 특성
- 인터페이스에 정의된 모든 메소드는 추상적이며, 인터페이스에 implementaion이 포함될 수 없다.
- 인터페이스에는 인스턴스 변수를 포함할 수 없다.
- 그러나 public static final variable은 포함할 수 있다. (예를 들어, 상수)
- 인터페이스가 public인 경우, 반드시 같은 이름을 가진 file에 포함되어야 한다.
- 추상클래스보다 더 추상적이다.
- 인터페이스는 implementaion이라는 키워드를 사용하는 클래스에 의해 구현된다.


![[Pasted image 20240618055153.png]]

## Interfaces as Types
인터페이스도 type의 이름으로 쓸 수 있다.
컴파일러는 인터페이스를 type으로 간주한다.

=> 인터페이스를 변수 또는 메소드 매개 변수를 선언하는 데 사용할 수 있다.


## Abstract Classes VS Interfaces
대부분의 경우에서 interface를 사용한다.

추상 클래스를 사용하는 경우
- subclass - superclass의 관계가 "is a"일 때.
- 추상 클래스가 적절한 추상화 수준에서 구현을 제공할 수 있을 때.

인터페이스를 사용하는 경우
- 정의된 메소드가 클래스의 작은 부분을 나타내는 경우
- subclass가 다른 class에서 상속을 받아야 할 때
-  메소드의 어떤 것도 합리적으로 구현할 수 없을 때 


![[Pasted image 20240618055829.png]]


