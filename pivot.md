# PIVOT

## PIVOT : 행 데이터를 컬럼으로 변경하는 함수

```text
SELECT * 
FROM (SELECT department_id, salary FROM employees) 
PIVOT (sum(salary) for department_id in (10, 20, 30));
```

* 행 데이터를 컬럼으로
* 인라인 뷰를 써야 한다
* PIVOT 뒤에는 그룹함수를 사용하는 것이다
* 그래서 그룹함수에 써줘야 하는 리소스 컬럼을 FROM에 밝혀줘야 한다.
* department\_id 별로 salary 합을 구할 거면 가상 테이블에 그 둘을 넣어주어야 한다.

