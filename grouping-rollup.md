# GROUP BY ROLLUP

## GROUP BY ROLLUP

* GROUP BY 절에 지정된 열 리스트를 오른쪽에서 왼쪽으로 이동하면서 그룹화를 만드는 기능이다. 아래와 같은 결과를 모두 한꺼번에 출력하고 싶을 때 사용한다.
* SUM\(salary\) = {a, b, c}

  SUM\(salary\) = {a, b}

  SUM\(salary\) = {a}

  SUM\(salary\)

```sql
--GROUP BY rollup 연산자 문형

SELECT a, b, c, sum(salary) --AVG, MAX, MIN 등 그룹함수 사용 가능하다
FROM tabename
GROUP BY rollup (a,b,c) ; d

SELECT department_id, job_id, manager_id, SUM(salary) 
FROM employees 
GROUP BY rollup (department_id, job_id, manager_id) ;
```

