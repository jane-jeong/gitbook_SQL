# DML - UPDATE

## UPDATE : 데이터 수정

* 원하는 조건으로 데이터 검색해서 해당 데이터를 수정한다.
* UPDATE 문에 조건문 입력하지 않으면 모든 데이터가 수정되니 주의할 것

## UPDATE 테이블명 SET ~ \(WHERE ~\)

```sql
UPDATE EMP 
	SET name = '조조'
WHERE id = 1; 


COMMIT; OR ROLLBACK;
```

## 주의 : UPDATE 문에서 데이터를 수정할 때 조건절이 나오는 행 수만큼 수정된다

예를 들어, 위의 예에서 id = 1 인 직원이 2명이면 두 명의 name은 모두 '조조'로 수정된다

### \[ 문제 \] 오류 디버깅하기 

```sql
# 디버깅 
```

## UPDATE : 다른 테이블에서 데이터 가져와서 내 테이블 업데이트하기

```sql
/** hr 부서의 department_name을 가져와서 
emp_dept 테이블의 dept_name 모두 변경하기 */

UPDATE emp_dept o 
set dept_name = (select department_name 
                from hr.departments 
                where department_id = o.dept_id );
                
                
COMMIT; OR ROLLBACK;
```

## UPDATE : 다른 테이블에서 가져온 데이터 조작한  내 테이블 업데이트하기

```sql
/** oltp_emp 테이블의 salary 가져오되 10% 상승한 값으로 가져와서 
dw에 넣어 업데이트하기 */

UPDATE dw_emp o 
SET salary = (SELECT salary*1.1 
							FROM oltp_emp 
							WHERE employee_id = o.employee_id) ;
							

COMMIT; OR ROLLBACK;
```



