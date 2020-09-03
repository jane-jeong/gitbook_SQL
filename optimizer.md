# 최적화  - Execution Plan

## SQL 실행 계획 읽는 방법 

```sql
SELECT *
FROM employees e, departments d 
WHERE e.department_id = d.dpeartment_id 
AND e.department_id = 10 ; 
```

### 실행 계획 

![](.gitbook/assets/image%20%2819%29.png)

* ALL\_ROWS : 비용 기반 옵티마이저 
* CARDINALITY : 행 수 
* 1번 : departments 테이블에서 인덱스 SYS\_C007959를 유일하게 조회함 \(INDEX UNIQUE SCAN\)
* 2번 : 인덱스에서 departments 테이블의 ROWID를 사용해서 조회함 
* 3번 : employees 테이블을 전체 스캔함 \(FULL TABLE SCAN\)
* 4번 : departments 테이블과 employees 테이블을 Nested Loop 조인해서 최종 결과를 만들어냄 
* 복습 : NL 조인은 departments 테이블에서 먼저 데이터를 찾고 그다음 employees 테이블을 찾는 것을 의미 = Random Access



