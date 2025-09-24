---
aliases:
  - 다형성
---
operation(typically virtual)을 다른 클래스에서 다른 방식으로 수행할 수 있는 객체 지향 소프트웨어의 특성.

동일한 이름의 메소드가 여러개 있어야 한다.
실행할 걸 선택하는 것은 변수에 있는 객체에 따라 달라진다.
프로그래머가 많은 조건문을 사용할 필요가 줄어든다.

# 종류
### Runtime Polymorphism
dynamic polymorphism으로 method overriding 방식
![[Pasted image 20240618052716.png]]

polymorphism variable은 자신의 클래스와 자신의 클래스의 자식 클래스의 오브젝트를 참조할 수 있다.

소프트웨어 시스템을 개발 및 유지보수 중에 보다 쉽게 확장할 수 있다.
### Compile time Polymorphism
static polymorphism으로 method overloading 방식
![[Pasted image 20240618052702.png]]


# Abstract Class and Abstract Method (in Java)
### Abstract Method
정의를 포함하지 않은 메소드. 오직 프로토콜만 포함함.

abstract method가 하나라도 있는 class는 abstract class이지만, 
abstract class라고 해서 abstract method가 있는 것은 아니다.

추상 클래스는 인스턴스화할 수 없다.
그러나 abstract class type의 variable는 자신의 후손 객체를 참조할 수 있다. (그러나 자기와 같은 타입의 객체는 참조 불가.)
abstract class 타입의 변수는 가능.
![[Pasted image 20240618053746.png]]


# 함수 실행 결정 순서
1. operation에 대한 concrete method가 현재 class안에 있다면 method 실행.
2. 그렇지 않다면, 볼 수 있는 super class를 확인하고, 거기에 method가 있다면 실행.
3. method가 발견될 때까지 higher super class를 계속 보며 2를 반복한 후 실행.
4. 만약 메소드가 발견되지 않았으면 에러가 있는 것. 