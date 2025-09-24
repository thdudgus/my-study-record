---
aliases:
  - 논리적 아키텍처
---
package, subsystem과 layer를 소프트웨어의 class로 한 large-scale organizatioin이다.
- 이러한 요소가 서로 다른 운영체제 프로세스에 걸쳐지거나 네트워크의 물리적 컴퓨터에 어떻게 배치되는지에 따라 이러한 요소들이 배치되는 decision은 없음.
-> deployment architecture (Deployment diagram)
	package diagram으로 표현 가능.


### Layer
layer는 cohesive responsibility를 가진 클래스, 패키지 또는 subsystem의 coarse-grained grouping이다.
- higher layer는 lower layer를 호출하지만 반대는 아니다.
- OO system에서 layer
	- user interface
	- 애플리케이션 로직과 도메인 오브젝트 : 애플리케이션 요구 사항을 충족하는 도메인 개념을 나타내는 software object
	- technical service : db와의 interface, error logging 등.. 이러한 서비스는 일반적으로 애플리케이션에 독립적이며 여러 시스템에 걸쳐 재사용이 가능하다.


## Layer architecture의 종류
### Strict Layer architecture
- 상위 layer는 바로 아래의 하위 layer의 service만 호출.
- 네트워크 프로토콜 시스템에선 일반적이지만 information 시스템에선 그렇지 않다.

### Relaxed Layer architecture
- 상위 layer는 여러 하위 layer를 호출.
- information 시스템에서 흔히 볼 수 있다.

![[Pasted image 20240618064145.png|500]]
focus는 Domain.

**공통적으로 lower layer에서 higher layer call 불가능.**

