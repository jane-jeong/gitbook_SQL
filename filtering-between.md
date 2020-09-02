# FILTERING - BETWEEN

## BETWEEN A AND B : 기준 컬럼 범위 검색 

* BETWEEN문은 지정된 범위에 있는 값을 조회한다. 
* BETWEEN 1000 AND 2000 : 1000과 2000을 포함하고 1000과 2000 사이의 값을 조회한다 

```text
SELECT * 
FROM employees 
WHERE salary between 10000 and 20000;
```

## NOT BETWEEN A AND B 

```text
--not between: 범위 내 값 제외하고 출력하기  
SELECT *
FROM employees 
WHERE employee_id not between 100 and 102; 
```

