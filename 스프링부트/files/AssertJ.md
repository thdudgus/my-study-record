**AssertJ는 JUnit과 함께 사용해 검증문의 가독성을 높여주는 라이브러리.**

##### 예시
```java
Assertions.assertEquals(sum, a + b); 
```
위 코드는 기댓값과 비교값이 잘 구분되지 않아, 아래와 같이 AssertJ를 적용해 바꿀 수 있다.
```java
assertThat(a + b).isEqualTo(sum);
```
AssertJ에는 `isEqualTo()`와 같은 다양한 메서드를 제공한다. 

| 메서드이름             | 설명               |
|-------------------|------------------|
| **isEqualTo(A)**      | A 값과 같은지 검증      |
| **isNotEqualTo(A)**   | A 값과 다른지 검증      |
| **contains(A)**       | A 값과 포함하는지 검증    |
| **doesNotContain(A)** | A 값과 포함하지 않는지 검증 |
| **startsWith(A)**     | 접두사가 A인지 검증      |
| **endsWith(A)**       | 접미사가 A인지 검증      |
| **isEmpty()**         | 비어 있는 값인지 검증     |
| **isNotEmpty()**      | 비어 있지 않은 값인지 검증  |
| **isPositive()**      | 양수인지 검증          |
| **isNegative()**      | 음수인지 검증          |
| **isGreaterThan(1)**  | 1보다 큰 값인지 검증     |
| **isLessThan(1)**     | 1보다 작은 값인지 검증    |
