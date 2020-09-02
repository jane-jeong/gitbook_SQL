# BASE - TRUE / FALSE

## True / False 

```text
SQL(3)_200619
 
#True or False
T and T -> T
T and F -> F
T and null -> null
F and null -> F

T or T -> T
T or F -> T
T or null -> T
F or null -> null

-or의 반대는 and
-not in 연산자에 null 값이 있으면 데이터가 조회되지 않는다
-결과물 데이터가 잘 나왔는지 꼭 검증해야 한다

--T or null
SELECT *
FROM employees
WHERE employee_id in (100,101,null);

SELECT *
FROM employees
WHERE employee_id = 100
or employee_id = 101
or employee_id = null;

--T and null
SELECT *
FROM employees
WHERE employee_id not in (100,101,null);

SELECT *
FROM employees
WHERE employee_id <> 100
and employee_id <> 101
and employee_id <> null;
```

