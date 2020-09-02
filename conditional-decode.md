# CONDITIONAL - DECODE

## 조건제어 함수 - DECODE

* SQL에서는 DECODE 문으로 IF문을 구현할 수 있다. 
* DECODE문에서는 특정 조건이 참이면 A, 거짓이면 B로 리턴하게 할 수 있다. 
* **1\) DECODE\(기준값, 비교값, 비교1참값, 비교1거짓값\)** 
* **기준값이 비교값과 같다면 비교1참값 리턴. 기준값이 비교값과 같지 않다면 비교1거짓값 리턴.**
* **2\) DECODE\(기준값, 비교값1, 비교1참값, 비교2, 비교2참값, 비교3, 비교3참값\)**
* **기준값이 비교값1이라면 비교1참값을 리턴. 만약, 기준값이 비교값1이 아니고 비교값2라면 비교2참값 리턴. 만약, 비교값2도 아니고 비교값3이라면 비교3참값 리턴.** 
* 단, DECODE 함수는 같은 것\(=\)만 비할 수 있고, 크거나 작은 것은 비교할 수 없다.

```sql
SELECT DECODE(employee_id, 100, 'TRUE', 'FALSE') 
FROM employees ; 
--employee_id가 100과 같으면 'TRUE'를 리턴하고, 같지 않으면 'FALSE'를 리턴 
```

```sql
--아래와 같은 IF 구문을 실행하고 싶다고 생각했을 때 (아래는 pl/sql 쿼리문)
--TMI : dicision tree. 머신러닝에서 하는 건 모두 IF로 함 
IF job_id= 'IT_PROG' then 
    salary*1.1
elsif job_id = 'ST_CLERK' then 
    salary*1.2 
elsif job_id = 'SA_REP' then 
    salary*1.3 
else 
    salary 
END IF;
```

```sql
/** 아래처 DECODE 함수를 쓴다 (행 이름에 '' 콤마 씌워야 한다. 문법이다)

DECODE(기준,비교값1,비교1참값,비교값2,비교2참값,비교값3,비교3참값)

기준값이 비교값1이라면 비교1참값, 그리고 혹시 기준값이 비교값1이 아니
기준값이 비교값 2이면, 비교2참값 리턴해, 그리고 혹시 기준값이 비교값 2가 아니, 
기준값이 비교값 3이면 비교3참값 리턴해 */

SELECT employee_id, job_id, salary, 
decode(job_id,'IT_PROG',salary*1.1,'ST_CLERK',
salary*1.2,'SA_REP',salary*1.3) 
FROM employees
WHERE 
decode(job_id,'IT_PROG',salary*1.1,'ST_CLERK',
salary*1.2,'SA_REP',salary*1.3) is not null;

/** DECODE 함수는 크거나, 작은 것은 연산할 수 없고, 같은 것만 연산할 수 있다 */
```

