# SUBQUERY

## 서브쿼리란 

* SQL 문 안의 SELECT 문을 서브쿼리라고 한다.
* 중첩 서브쿼리: 서브쿼리 절을 먼저 수행하고 그 값을 가지고 메인쿼리 절이 사용한다.
  * 1. 이너 쿼리 먼저 수행
  * 1. 이너 쿼리의 수행 값을 가지고 아우터 쿼리\(메인 쿼리\)가 사용

## 서브쿼리 사용법 

* 서브쿼리를 괄호 안에 넣어서 표현하고, SELECT문 / FROM절 / WHERE절에 사용한다.
* 서브쿼리의 위치에 따른 명칭
  * SELECT문에 있는 서브쿼리: 스칼라 서브쿼리 \(1행만 반환\)
  * FROM절에 있는 서브쿼리: 인라인 뷰
  * WHERE절에 있는 서브쿼리: 서브쿼리

```text
SELECT * 
FROM employees 
WHERE salary > (SELECT salary from employees where employee_id=110) ;
--참고: 위 쿼리는 중첩 서브쿼리 

SELECT * 
FROM employees 
WHERE job_id = (SELECT job_id FROM employees WHERE employee_id = 110 );
--참고: 위 쿼리는 중첩 서브쿼리 

SELECT * 
FROM employees
WHERE job_id = (SELECT job_id FROM employees WHERE employee_id = 110 )
and salary > (SELECT salary FROM employees WHERE employee_id = 110 );
/** 해석: employee_id가 110인 사원의 job_id와 같고, employee_id가 110인 
사원의 연봉보다 연봉이 큰 사원 정보를 출력 */
```

## INLINE VIEW : FROM 절의 서브쿼리 

```text
--[문제47] 자신의 부서 평균 급여보다 더 많이 받는 사원을 출력해주세요. 

SELECT * 
FROM employees o
WHERE salary > (SELECT avg(salary) 
								FROM employees 
								WHERE department_id = o.department_id);
```

* 위 쿼리는 악성 코드 문제가 생긴다.
* 위 쿼리의 악성 코드 문제를 해결하기 위해 가상의 '부서별 평균 집합'을 만들어준다.
* Inline view는 FROM 절의 SELECT문\(서브쿼리\)이다.

```text
SELECT *
FROM (SELECT * FROM employees) --FROM절의 서브쿼리=인라인 뷰

SELECT e2.last_name, e2.salary, e1.avg_sal
FROM ( SELECT department_id, avg(salary) avg_sal 
       FROM employees 
       GROUP by department_id) e1, employees e2
WHERE e1.department_id = e2.department_id 
and e2.salary > e1.avg_sal;
--참고: avg(sal)은 컴퓨터가 함수로 인식하기 때문에
--avg(sal)을 컬럼처럼 사용하려면 열 별칭을 사용해야 한다. 
--열별칭에 공백 문자 쓰려면 큰 따옴표 써야 한다. 
--열별칭 불러줄 때 공백 들어가 있으면 오류나니까, 
--"avg sal" 그대로 써줘야 한다.
```

