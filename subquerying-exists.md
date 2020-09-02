# EXISTS

## EXISTS : 상호관련 서브쿼리 중 많이 사용하는 함수

```sql
--위와 경우에 상호관련 서브쿼리를 쓴다. 존재 여부를 찾을 때 
--그런데 문제가 있다. 한 번 찾으면 그만 찾아도 되는데, 계속 찾고 있는 것.
--그래서 상호관련 서브쿼리의 일종이지만, 문제를 보완한 exists 함수가 탄생

--manager인 사원 정보를 찾아라. (exists 표현법 사용)
SELECT * 
FROM employees o 
WHERE EXISTS (SELECT 'x' FROM employees WHERE manager_id = o.employee_id);
--exixst 함수는 상호관련 서브쿼리 중 가장 많이 쓰이는 함수다. 
--o.employee_id 후보행이 기준행(manager_id)와 같으면 ture->출력하고
--다르면 false->버린다

----exists 
--후보행 값이 서브쿼리에 존재하는 지를 찾는 연산자 
--후보행 값이 서브쿼리에 존재하면 TRUE 우리가 찾는 데이터다. 검색 종료 
--후보행 값이 서브쿼리에 존재하지 않으면 FALSE. 계속 검색해. 

--exists 연산자면 무조건 상호관련 서브쿼리
```

