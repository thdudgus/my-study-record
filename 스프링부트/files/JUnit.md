자바 언어를 위한 [[단위 테스트]] 프레임워크

JUnit을 사용하면 단위 테스트를 작성하고 테스트하는 데 도움을 준다.

### 특징
- 테스트 방식을 구분할 수 있는 annotation을 제공
- @Test annotation으로 메서드를 호출할 때마다 새 인스턴스를 생성, 독립 테스트 가능
- 예상 결과를 검증하는 assertion 메서드를 제공
- 단순한 사용 방법 (테스트 코드 작성 시간이 적음)
- 자동 실행, 자체 결과를 확인하고 즉각적 피드백 제공


#### JUnit으로 단위 테스트 코드 만들기
```java
import org.junit.jupiter.api.Assertions;  
import org.junit.jupiter.api.DisplayName;  
import org.junit.jupiter.api.Test;  
  
public class jUnitTest {  
    @DisplayName("1 + 2는 3이다.")  // 테스트 이름 명시
    @Test // 테스트를 수행하는 메서드  
    public void JUnitTest() {  
        int a = 1;  
        int b = 2;  
        int sum = 3;  
  
        Assertions.assertEquals(sum, a + b);  // 값이 같은지 확인  
    }  
}
```
==JUnit은 테스트끼리 영향을 주지 않도록 각 테스트를 실행할 때마다 테스트를 위한 실행 객체를 만들고 테스트가 종료되면 실행 객체를 삭제한다.==
`assertEquals(기댓값, 실제 검증할 값)` 는 JUnit이 제공하는 검증 메서드.
위 테스트는 성공한 테스트이다.

아래 테스트는 실패했을 때의 경우이다.
```java
@DisplayName("1 + 3는 4이다.")  // 테스트 이름  
@Test // 테스트 메서드  
public void jUnitFailTest() {  
    int a = 1;  
    int b = 3;  
    int sum = 3;  
  
    Assertions.assertEquals(sum, a + b);  // 값이 같은지 확인  
}
```

실패용 테스트 케이스를 실행하면 테스트가 실패했다는 표시와 함께 기댓값과 실제로 받은 값을 비교해서 알려준다.
![[Pasted image 20241106012056.png|350]]
테스트 케이스가 하나라도 실패하면 전체 테스트를 실패한 것으로 보여준다.

다음 진행을 위해, 위 실패 케이스를 삭제 후 아래 파일 추가.
JUnitCycleTest.java
==테스트는 annotation에 따라 실행 순서가 정해진다.==
```java
import org.junit.jupiter.api.AfterAll;  
import org.junit.jupiter.api.AfterEach;  
import org.junit.jupiter.api.BeforeAll;  
import org.junit.jupiter.api.BeforeEach;  
import org.junit.jupiter.api.Test;  
  
public class JUnitCycleTest {  
    @BeforeAll // 전체 테스트를 실행하기 전에 1회 실행하므로 메서드를 static으로 선언  
    static void beforeAll(){  
        System.out.println("@BeforeAll");  
    }  
      
    @BeforeEach  // 테스트 케이스를 시작하기 전마다 실행  
    public void beforeEach(){  
        System.out.println("@BeforeEach");  
    }  
      
    @Test  
    public void test1(){  
        System.out.println("test1");  
    }  
  
    @Test  
    public void test2(){  
        System.out.println("test2");  
    }  
  
    @Test  
    public void test3(){  
        System.out.println("test3");  
    }  
      
    @AfterAll  // 전체 테스트를 마치고 종료하기 전에 1회 실행하므로 메서드는 static    static void afterAll(){  
        System.out.println("@AfterAll");  
    }  
      
    @AfterEach  // 테스트 케이스를 종료하기 전마다 실행  
    public void afterEach(){  
        System.out.println("@AfterEach");  
    }  
}
```

##### 위 코드에서 사용된 annotation

| **Annotation**  | 설명                                             | 예시                                            |
| --------------- | ---------------------------------------------- | --------------------------------------------- |
| **@BeforeAll**  | 전체 테스트를 실행하기 전에 1회 실행하므로 메서드를 static으로 선언.     | DB를 연결해야 하거나 테스트 환경을 초기화할 때                   |
| **@BeforeEach** | 테스트 케이스를 시작하기 전마다 실행.<br>static이 아니어야 함.       | 테스트 메서드에서 사용하는 객체를 초기화하거나 테스트에 필요한 값을 미리 넣을 때 |
| **@AfterAll**   | 전체 테스트를 마치고 종료하기 전에 1회 실행하므로 메서드는 static으로 선언. | DB 연결을 종료하거나 고통적으로 사용하는 자원을 해제할 때             |
| **AfterEach**   | 테스트 케이스를 종료하기 전마다 실행.<br>static이 아니어야 함.       | 테스트 이후에 특정 테이터를 삭제해야 하는 경우                    |
![[Pasted image 20241106013551.png|500]]
@BeforeAll -----> ==@BeforeEach -----> @Test -----> @AfterEeach== -----> @AfterAll
	==테스트의 개수만큼 위 생명주기로 반복됨.==

