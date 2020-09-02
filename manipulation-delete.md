# DML - DELETE

## DELETE : 데이터 삭제

* 원하는 조건을 검색해서 해당되는 행을 삭제한다.
* DELETE 문에 조건을 입력하지 않으면 모든 데이터가 삭제된다.

## 1\) DELETE FROM 테이블명 WHERE ~

```sql
DELETE FROM emp 
WHERE id = 1 ;

COMMIT; OR ROLLBACK;
```

## 2\) DELETE FROM 테이블명 ;

* 테이블의 모든 데이터를 삭제한다.
* 데이터가 삭제되어도 테이블의 용량은 감소하지 않는다. \(지정한 용량 그대로 남아 있음\)

```sql
DELETE FROM emp ; 

COMMIT; OR ROLLBACK;
```

#### 데이터 딕셔너리에서 테이블 정보 조회하기 \(MAX EXTENTS 컬럼에서 최대 저장 용량 확인 가능\)

* DELETE FROM ~ 으로 데이터를 모두 지워도 테이블 용량은 보존되어 있는 걸 확인할 수 있다.

```sql
SELECT TABLE NAME, MAX EXTENTS 
FROM USER_TABLES ; 
```

### 참고: TRUNCATE TABLE 

* TRUNCATE TABLE은 테이블의 모든 데이터를 삭제하는 동시에, 데이터가 제거되면 테이블의 용량을 초기화한다. 

```sql
TRUNCATE TABLE EMP ; 
```

