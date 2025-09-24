---
aliases:
  - 빈
---
쉽게 말해 **스프링 컨테이너에서 관리하는 객체**를 말한다.
= **스프링에서 제공해주고 관리해주는 객체**

```java
public class A {
// A에서 B를 주입받고 있음. (객체를 주입받고 있음.)
	@Autowired
	B b;
}
```
해당 코드에서 B가 bean이다. 

스프링은 bean을 스프링 컨테이너에 등록하기 위해 XML 파일 설정, annotation 추가 등의 방법을 제공한다.


예를 들어,
==MyBean이라는 클래스에 **@Component** annotation을 붙이면 MyBean 클래스가 bean으로 등록된다. 이후 스프링 컨테이너에서 이 클래스를 관리한다.==
이때 bean의 이름은 클래스 이름의 첫글자로 소문자로 바꿔 관리한다. 따라서 MyBean 클래스의 이름은 myBean이 된다.
```java
@Component // 클래스 MyBean을 bean으로 등록
public class MyBean{
}
```
