# FILTERING - SELECT DISTINCT

## SELECT DISTINCT : 컬럼에서 중복되는 값 제외

* 주의 : DISTINCT는 SELECT 바로 뒤, 중복 제거할 컬럼명 앞에 위치해야 하고, 무조건 딱 한 번 밖에 쓰일 수 없다. 
* 참고 : 중복 행 제거하는 알고리즘은 HASH\(산수/나누기\) 함수다. 나누기의 몫이 아닌 나머지값\(KEY VALUE가 됨\)으로 자료를 관리하는 알고리즘이다.  

```text
SELECT distinct department_id 
FROM employees;


SELECT distinct job_id
FROM employees;


SELECT distinct department_id, job_id 
FROM employees;
--이렇게 하면 둘 다 중복행 제거하지 않기 때문에 
--결과는 20행 나온다
```

## SELECT COUNT\(DISTINCT ~\) : 컬럼에서 중복되는 값 제외하고 행 갯수 카운팅 <a id="select-distinct"></a>

```text
SELECT COUNT(DISTINCT last_name)
FROM employees ;
```

