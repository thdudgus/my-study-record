---
aliases:
  - 엔티티
---
**데이터베이스의 테이블과 매핑되는 객체**
데이터베이스에 영향을 미치는 쿼리를 실행하는 객체임.

##### 상태
1. **detached** : [[persistence context]]가 관리하고 있지 않은 분리 상태.
2. **managed** : persistence context가 관리하는 관리 상태.
3. **transient** : persistence context와 전혀 관계가 없는 비영속 상태.
4. **removed** : 삭제된 상태.
위 상태들은 특정 메서드를 호출해 변경 가능.
필요에 따라 entity의 상태를 조절해 데이터를 올바르게 유지하고 관리 가능.
```java
public clss EntityManageTest {
	@Autowired
	EntityManager em;

	public void example() {
		// 1. entity manager가 entity를 관리하지 않는 상태. (transient 상태)
		Member member = new Member(1L. "홍길동");

		// 2. entity가 관리되는 상태.
		em.persist(member);
		// 3. entity 객체가 분리된 상태.
		em.detach(member);
		// 4. entity 객체가 삭제된 상태.
		em.remove(member);
	}
}
```
1. entity를 처음 만들면 entity는 비영속(transient) 상태가 된다.
2. persist()를 통해 관리 상태로 만들 수 있고, Member 객체는 persistence context에서 상태가 관리된다.
3. 만약 persistence context에서 관리하고 싶지 않다면 detach() 메서드 사용하여 분리 상태로 만든다.
4. 더 이상 객체가 필요 없으면 remove() 메서드로 entity를 persistence context와 데이터베이스에서 삭제한다.