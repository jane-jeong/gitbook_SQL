# 최적화  - Optimizer Join

## Nested Loop 조인 

Nested Loop 조인은 하나의 테이블에서 데이터를 먼저 찾고 그 다음 테이블을 조인하는 방식으로 실행된다. 네스티드 룹 조인에서 먼저 조회되는 테이블을 외부 테이블\(Outer Table\)이라 하고 그 다음 조회되는 테이블을 내부 테이블\(Inner Table\)이라고 한다. 네스티드 조인에서는 외부 테이블\(선행 테이블\)의 크기가 작은 것을 먼저 찾는 것이 중요하다. 그래야 데이터가 스캔되는 범위를 줄일 수 있기 때문이다. 네스티드 룹 조인은 RANDOM ACCESS가 발생하는데 랜덤 엑세스가 많이 발생하면 성능이 저하된다. 그러므로 네스티드 룹 조인을 할 때는 랜덤 엑세스의 양을 줄여야 성능이 향상된다. 

![](.gitbook/assets/image%20%2818%29.png)

### 힌트를 사용한 NESTED LOOP JOIN 예시 

아래에서 `use_nl` 힌트를 사용해서 의도적으로 NL 조인을 실행한다. 실행계획을 보면 employees 테이블을 먼저 full scan하고 그 다음 departments 테이블을 full scan해서 NL 조인을 수행한다. 

`ordered` 힌트는 FROM 절에 나오는 테이블 순서대로 조인을 하게 하는 것이다. ordered 힌트는 단독으로 사용하지 않 u`se_nl,`  `use_merge`, `use _hash` 힌트와 함께 사용한다.

```sql
SELECT /*+ ordered use_nl(d) */ * 
FROM employees e, departments d 
WHERE e.department_id = d.department_id 
AND e.department_id = 10 ; 
```

## SORT MERGE 조인 

SORT MERGE 조인은 두 개의 테이블을 SORT\_AREA라는 메모리 공간에 모두 로딩하고 SORT를 수행한다. 두 개의 테이블에 대해서 SORT가 완료되면 두 개의 테이블을 병합\(merge\)한다. sort merge 조인은 sort가 발생하기 때문에 데이터 양이 많아지면 성능이 저하된다. 또한, 정렬 데이터 양이 너무 많으면 정렬은 임시 영역에서 수행되는데, 임시 영역은 디스크에 있기 때문에 성능이 급격히 저하되게 된다. 

### 힌트를 사용한 SORT MERGE JOIN 예시 

아래에서 `use_merge` 힌트를 사용해서 의도적으로 SORT MERGE 조인을 실행한다. 실행계획을 확인해보면 SORT와 MERGE  단계로 실행하는 것을 확인할 수 있다. 

```sql
SELECT /*+ ordered use_merge(d) */ * 
FROM employees e, departments d 
WHERE e.department_id = d.department_id 
AND e.department_id = 10 ; 
```

## HASH 조

HASH 조인은 두 개의 테이블 중에서 작은 테이블을 HASH 메모리에 로딩하고 두 개의 테이블의 조인 키를 사용해서 해시 테이블을 생성한다. 해시 조인은 해시함수를 사용해서 주소를 계산하고 해당 주소를 사용해서 테이블을 조인하기 때문에 CPU 연산을 많이 한다. 특히 해시 조인 시에는 선행 테이블의 크기가 충분히 작아서 메모리에 로딩될 수 있어야 한다.

### 힌트를 사용한 HASH JOIN 예시 

아래에서 `use_hash` 힌트를 사용해서 의도적으로 HASH JOIN을 실행한다. 

```sql
SELECT /*+ ordered use_hash(d) */ * 
FROM employees e, departments d 
WHERE e.department_id = d.department_id 
AND e.department_id = 10 ; 
```

