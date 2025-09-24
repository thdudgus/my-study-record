---
aliases:
  - 범용 세마포어
  - counting semaphore
  - 카운팅 세마포어
  - 일반 세마포어
---
이진 세마포어와 구분하기 위해 비이진 세마포어를 카운팅 세마포어, 범용 세마포어라고 부른다. 

세마포어의 **increment** 연산: 세마포어 값을 증가시킨다. 만약 값이 0이거나 음수면, semWait연산에 의해 블록되었던 프로세스를 깨울 수 있다. 
	이 세마포어를 카운팅 세마포어(counting semaphore), 일반 세마포어([[general semaphore]])라 한다.  

