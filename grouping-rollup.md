# GROUP BY ROLLUP

## GROUP BY ROLLUP

* ROLLUP은 GROUP BY 컬럼에 대해서 서브토탈을 만들어준다. ROLLUP을 할 때 GROUP BY구에 컬럼이 두 개 이상 오면 순서에 따라 결과가 달라진다. 
* GROUP BY 절에 지정된 열 리스트를 오른쪽에서 왼쪽으로 이동하면서 그룹화를 만든. 아래와 같은 결과를 모두 한꺼번에 출력하고 싶을 때 사용한다.
* SUM\(salary\) = {a, b, c}

  SUM\(salary\) = {a, b}

  SUM\(salary\) = {a}

  SUM\(salary\)

```sql
--GROUP BY rollup 연산자 문형
SELECT a, b, c, sum(salary) --AVG, MAX, MIN 등 그룹함수 사용 가능하다
FROM table_name 
GROUP BY rollup (a,b,c) ; d


SELECT department_id, job_id, manager_id, SUM(salary) 
FROM employees 
GROUP BY ROLLUP (department_id, job_id, manager_id) ;
```

* 부서별, 직업별 ROLLUP을 실행하면 부서별 합계, 직업별 합계, 전체합계까 모두 조회된다. 
* ROLLUP으로 실행되는 컬럼별로 서브토탈을 만들어준다. 

