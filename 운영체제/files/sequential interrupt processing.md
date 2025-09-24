---
aliases:
  - 순차적 인터럽트 처리
---

일반적으로 interrupt [[disable]] 기간 동안 발생한 interrupt는 처리되지 않은 채 남겨져 있게 되고 processor가 interrupt 발생을 허용한 후에 처리된다.    
**따라서 사용자 프로그램이 수행 중일 때 하나의 interrupt가 발생한 경우 다른 interrupt는 즉시 disable된다.** interrupt processor 루틴이 완료된 후, 사용자 프로그램이 재개 되기 전에  interrupt가 허용되고, 이때 다른 interrupt가 발생했는지 점검한다. (interrupt가 엄격히 순차적으로 처리 된다.)    
![[Pasted image 20240402062710.png]] 
<br>
**단점**   
- 상대적인 우선순위나 time-critical 요구를 고려하지 않고 있음.   
