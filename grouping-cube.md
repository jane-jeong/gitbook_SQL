# GROUP BY CUBE

## GROUP BY CUBE 

* rollup 기능을 포함하고 모든 그룹화할 수 있는 것을 만드는 기능이다. 아래와 같은 결과를 모두 한꺼번에 출력하고 싶을 때 사용한다.
* SUM\(sal\) = {a,b,c} SUM\(sal\) = {a,b} SUM\(sal\) = {a.c} SUM\(sal\) = {b,c} SUM\(sal\) = {a} SUM\(sal\) = {b} SUM\(sal\) = {c} SUM\(sal\) = {}

```text
--CUBE 연산자의 문형 

SELECT a, b, c, SUM(salary) --AVG, MAX, MIN 등 그룹함수 사용 가능하다
FROM tablename
GROUP BY CUBE (a, b, c) ;

SELECT department_id, job_id, manager_id, SUM(salary) 
FROM employees 
GROUP BY cube (department_id, job_id, manager_id); 
```

