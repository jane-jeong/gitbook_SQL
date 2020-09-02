# JOIN - LEFT OUTER JOIN

## OUTER JOIN

조인 조건의 컬럼의 값들이 서로 일치하는 경우 또는 조인조건의 일치되지 않은 값들도 출력해줄때 사용 -\(+\)

### 1\) ANSI 표준

### 2\) ORACLE

```text
#사원정보 다 출력하고 싶을 때
SELECT employee_id, department_name
FROM employees e, departments d
WHERE e.department_id(+) = d.department_id;

#부서정보 다 출력하고 싶을 때
SELECT employee_id, department_name
FROM employees e, departments d
WHERE e.department_id = d.department_id(+); -- 예를 들어 한 번도 판매된 적 없는 상품까지 파악하려면...
```

