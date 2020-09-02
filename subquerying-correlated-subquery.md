# CORRELATED SUBQUERY

## 상호관련 서브쿼리란

**메인쿼리의 테이블의 컬럼이 서브쿼리 안에 들어 있는 서브쿼리를 의미한다.**

\(메인쿼리의 값을 서브쿼리에 주고, 서브쿼리를 수행한 다음 그 결과를 다시 메인쿼리로 반환해서 수행하는 쿼리\)

1. 메인 쿼리\(아우터 쿼리\)를 먼저 수행
2. 첫번째 행을 후보 행으로 잡고 후보 행 값을 서브쿼리에 전달
3. 후보행 값을 가지고 서브쿼리 수행
4. 서브쿼리 결과를 사용해서 후보행으로 잡고 있는 기준값하고 비교해서 참이면 출력하고 거짓이면 버린다.
5. 두번째 행을 후보행으로 잡고 \(2번, 3번, 4번을 반복수행 - row의 끝까지\) —-예제 중심으로 기억해보자.

```sql
--manager인 사원 정보를 찾아라. (상호관련 서브쿼리 정석 사용)
SELECT * 
FROM employees
WHERE employee_id in (SELECT manager_id FROM employees);

SELECT manager_id 
FROM employees ;

--아래 처럼 돌리고 있는 것
SELECT *
FROM employees 
WHERE employee_id in (null, 100, 100, 102, 103, 103, ...);

--아래 처럼 돌리고 있는 것
WHERE employee_id = null
or employee_id = 100
or employee_id = 100
or employee_id = 102
or employee_id = 103
or employee_id = 103
...
```

