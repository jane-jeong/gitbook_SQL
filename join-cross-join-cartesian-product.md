# JOIN - CROSS JOIN \(Cartesian\)

## 카테시안 곱 



```text
--조인 조건이 생략이 된 경우
--조인 조건을 잘 못 만든 경우
--첫번째 테이블의 모든 행이 두번째 테이블의 모든 행에 곱으로 연결됨

--1.cartesian product ('연결'하는 것의 일종이지만 주의해야 한다)
SELECT employee_id, department_name 
FROM employees, departments;
/** 다 곱해짐. 모든 부서에 모든 사원이 각각 있는 걸로 되어버렸다. 
카테시안 곱은 조인 조건이 생략되었거나, 조인 조건이 잘못된 것. 
첫번째 테이블의 모든 행이 두번째 테이블의 모든 행에 곱으로 연결됨.
*/ 
```

