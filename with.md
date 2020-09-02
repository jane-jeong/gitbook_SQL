# WITH

## WITH

* WITH구문은 서브쿼리를 사용해서 임시 테이블이나 뷰처럼 사용할 수 있는 구문이다. 
* 서브쿼리 블록에 별칭을 지정할 수 있다. 
* 옵티마이저는 SQL을 인라인 뷰나 임시 테이블로 판단한다. 

```sql
WITH viewData AS 
    (SELECT * FROM employees
        UNION ALL 
    SELECT * FROM employees 
  ) -- 서브쿼리를 사용해서 임시 테이블을 만든
  SELECT * FROM viewData WHERE employee_id = 100 ; 
  --별칭을 사용해서 테이블을 SELECT한
```

