# FILTERING - AND, OR, NOT

## NOT : 조건에 해당되지 않는 것을 조회할 때

```text
--not in 
SELECT *
FROM employees 
WHERE employee_id not in (100,101,102);

--not between 
SELECT *
FROM employees 
WHERE employee_id not between 100 and 102;  

--not like 
SELECT *
FROM employees
WHERE last_name not like 'K%';


--NULL 값 아닌 것 찾는 연산자 : is not null 
--NULL이 아닌 데이터를 가지고 분석하자! 라고 할 때
--is not null 
SELECT * 
FROM employees 
WHERE department_id is not null;
```

