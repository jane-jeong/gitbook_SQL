# CONDITIONAL - CASE

## 조건제어 함수 - CASE 

* CASE문은 IF ... THEN ... ELSE - END의 프로그래밍 언어처럼 조건문을 사용할 수 있다. 
* 조건을 WHEN구에 사용하고 THEN은 해당 조건이 참이면 실행되고 거짓이면 ELSE구가 실행된다.

{% tabs %}
{% tab title="CASE 표현식" %}
```sql
CASE 기준값 WHEN 비교1 THEN 비교1참값 
           WHEN 비교2 THEN 비교2참값
           WHEN 비교3 THEN 비교3참값
           ELSE 기본값 
END
```
{% endtab %}

{% tab title="CASE 간단 예제" %}
```sql
SELECT CASE 
        WHEN employee_id = 100 THEN 'A' 
        WHEN employee_id = 101 THEN 'B' 
        ELSE 'C'
    END
FRM emp ; 
```
{% endtab %}
{% endtabs %}

```sql
--CASE 표현식으로 위 DECODE 함수와 유사한 결과 도출하기 
--CASE 표현식에서는 else까지 가능하다.
SELECT employee_id, job_id, salary, 
case job_id when 'IT_PROG' then salary*1.1 
            when 'ST_CLERK' then salary*1.2
            when 'SA_REP' then salary*1.3
            else salary
end revised_salary
FROM employees;

--이렇게 when 절 안에 기준값 넣을 수 있다 
--(Q. when 기준값 1= ~ , when 기준값 2= ~ 이렇게 해도 되려나?)
SELECT employee_id, job_id, salary, 
case when job_id = 'IT_PROG' then salary*1.1 
     when job_id = 'ST_CLERK' then salary*1.2
     when job_id = 'SA_REP' then salary*1.3
     else salary
end revised_salary
FROM employees;

--이렇게 when 절 안에 기준값 넣을 수 있다 (Q. when 기준값 1= ~ , when 기준값 2= ~ 이렇게 해도 되려나?)
SELECT employee_id, first_name||' '||last_name as"name", salary, 
case when salary < 5000 then 'low'
     when salary < 10000 then 'medium'
     when salary < 20000 then 'good'
     else 'excellent'
end "qualified salary"
FROM employees
ORDER BY salary DESC;
--(else = salary >= 20000)
--order by 열 DESC (FROM 뒤에) : 내림차순 

SELECT employee_id, first_name||' '||last_name as"name", salary,
CASE when salary < 5000 then 'low'
     when salary < 10000 then 'medium'
     when salary < 20000 then 'good'
     else 'excellent'
END "qualified salary"
FROM employees
ORDER BY salary ASC;
--order by 열 DESC (FROM 뒤에) : 내림차순 
```

