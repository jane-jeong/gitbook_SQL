---
description: 다중열(다중행) 서브쿼리 - 쌍비교와 비쌍비교
---

# 쌍비교/비쌍비교

## 다중열\(다중행\) 서브쿼리 - 쌍비교와 비쌍비교

```sql
#쌍비교
SELECT *
FROM employees
WHERE (manager_id, department_id) in ( SELECT manager_id, department_id 
                                       FROM employees
                                       WHERE first_name = 'John' );
# 얘가 다중행, 다중열 서브쿼리 

#비쌍비교                                         
SELECT *
FROM employees
WHERE manager_id in (SELECT manager_id 
                     FROM employees 
                     WHERE first_name = 'John')
AND department_id in (SELECT department_id 
                      FROM employees
                      WHERE first_name = 'John');
```

