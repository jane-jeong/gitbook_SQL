---
description: 자신의 테이블을 참조할 때 사용하는 조인 방식
---

# JOIN - SELF JOIN

## SELF JOIN

자신의 테이블을 참조할 때 사용하는 조인 방식이다. 각기 다른 테이블 별칭을 사용한다. 

```sql
--1
SELECT employee_id, last_name, manager_id
FROM employees e;

--2
SELECT employee_id, last_name
FROM employees m;

--1+2
SELECT e.employee_id, e.last_name, m.employee_id, m.last_name
FROM employees e, employees m
WHERE e.manager_id = m.employee_id(+)
order by e.employee_id
```

