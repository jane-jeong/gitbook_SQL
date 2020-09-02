# JOIN - CROSS JOIN \(Cartesian\)

## CROSS JOIN \( = CARTESIAN PRODUCT\) 

* CROSS JOIN은 조인 조건 구 없이 2개의 테이블을 하나로 조인한다. 조인구가 없기 때문에 카테시안 곱이 발생한다. 예를 들어, 행이 10개 있는 테이블과 행이 5개 있는 테이블을 크로스 조인하면 50개의 행이 조회된다. 크로스 조인은 FROM 절에서 CROSS JOIN구를 사용하거나, 아무것도 사용하지 않는다. 

```sql
SELECT employee_id, department_name 
FROM employees, departments;

--첫번째 테이블의 모든 행이 두번째 테이블의 모든 행에 곱으로 연결됨
--위 쿼리로 조회하면 모든 부서에 모든 사원이 각각 있는 걸로 되어버린다. 
--통상적으로 카테시안 곱은 조인 조건이 생략되었거나, 조인 조건이 잘못된 경우다. 
```

