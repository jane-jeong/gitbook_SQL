# GROUPING 함수

## GROUPING 함수 

* GROUPING 함수는 ROLLUP, CUBE, GROUPING SETS에서 생성되는 합계 값을 구분하기 위해 만들어진 함수다. 
* 예를 들어, 소계, 합계 등이 계산되면 GROUPING 함수는 1을 반환하고 그렇지 않으면 0을 반환해서 합계값을 식별할 수 있다. 
* 아래 SQL문 실행 결과에서 소계와 합계가 계산된 데이터는 GROUPING 함수에서 1이 출력된 것을 알 수 있다. 
* GROUPING의 반환 값을 DECODE혹은 CASE 문으로 식별해서 SELECT 문으로 소계, 합계를 구별하는 것이다. 

```sql
SELECT department_id, GROUPING(department_id), 
        job_id, GROUPING(job_id), SUM(salary) 
FROM employees 
GROUP BY ROLLUP (department_id, job_id) ; 
```

![](.gitbook/assets/image%20%284%29.png)

