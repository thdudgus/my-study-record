**사용자가 등록한 bean을 읽고 등록하는 annotation.**

@Component를 가진 클래스들을 찾아 bean으로 등록하는 역할.
그렇다고 모든 bean에 @Component만 사용하는 것은 아니다. 
실제 개발을 하면 @Component보다는 용도에 따른 아래의 annotation을 사용한다.

| Anotation                    | 설명       |
| ---------------------------- | -------- |
| @Configuration               | 설정 파일 등록 |
| @Repository                  | ORM 매핑   |
| @Controller, @RestController | [[라우터]]  |
| @Service<br>                 | 비즈니스 로직  |




