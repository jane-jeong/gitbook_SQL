---
description: key 컬럼이 일치되는 것을 이용해 테이블을 연결한다.
---

# JOIN - INNER JOIN \(EQUI\)

## EQUI\(등가\) 조인

* 조인은 여러 개의 릴레이션

## INNER JOIN = EQUI, SIMPLE, 등가 조인

key 컬럼이 일치되는 것을 이용해 테이블을 연결한다.

```sql
--조인 조건의 컬럼의 값들이 서로 일치하는 경우
--"=" 연산자를 사용한다
--WHERE절로 조인 조건 술어를 기술한다

--key 값이 일치되는 걸 연결하는 것 

SELECT e.employee_id, d.department_name 
FROM employees e, departments d
WHERE e.department_id = d.department_id ;
--지금 여기서는 WHERE 절이 조인 조건을 만드는 역할을 할 거다 
--key는 department_id. department_id로 찾아 갈거다. 
--department_id가 각각 어떤 테이블에 들어 있는지 명확하게 정의해주어야 한다. 
--정의방법: 테이블명.컬럼명 
--스토리지 절약하고 성능 높이기 위해 별칭 사용해준다. 
--테이블 뒤에 별칭 붙이면 된다
--SELECT 문에서의 컬럼에도 컬럼 앞에 접두어 붙여주면 더 빨리 찾아갈 수 있다. 주소 바로 붙여주는 것. 
--결과: 106건 나옴

--테이블 별칭 사용
SELECT employee_id, department_name
FROM employees e, departments d
WHERE e.department_id = d.department_id;

SELECT employee_id, department_name
FROM employees e, departments d
WHERE e.department_id = d.department_id;  
--1쪽지표 = m쪽지표(결과 값은 m쪽지표 행 수와 동일해야 함)

SELECT employee_id, department_name, l.city, c.country_name
FROM employees e, departments d, locations l, countries c
WHERE e.department_id = d.department_id
AND d.location_id = l.location_id
AND l.country_id = c.country_id
AND e.last_name like '%i%'; 
--비 조인 조건 술어
```

