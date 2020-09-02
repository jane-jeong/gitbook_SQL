# DDL - ALTER TABLE

## ALTER TABLE : 테이블 변경

* 컬럼 추가, 변경, 삭제 등

## 1\) 컬럼 추가 : ALTER TABLE ~ ADD

```sql
ALTER TABLE EMP 
        ADD (age number(2) default 1);
```

## 2\) 컬럼 변경 : ALTER TABLE ~ MODIFY

```sql
ALTER TABLE EMP 
        MODIFY (ename varchar2(40) not null);
```

## 3\) 컬럼 삭제 : ALTER TABLE ~ DROP COLUMN

```sql
ALTER TABLE EMP 
        DROP COLUMN age ;
```

## 4\) 컬럼명 변경 : ALTER TABLE ~ RENAME COLUMN ~ TO

```sql
ALTER TABLE EMP 
        RENAME COLUMN ename to new_ename ;
```

## 5\) NOLOGGING 옵션 사용

* 데이터베이스에 데이터를 입력하면 로그파일\(log file\)에 그 정보를 기록한다.
* Check Point라는 이벤트가 발생하면 로그파일의 데이터를 데이터 파일에 저장한다.
* NOLOGGING 옵션은 로그파일의 기록을 최소화시켜서 입력 시에 성능을 향상시키는 방법이다.
* NOLOGGING 옵션은 Buffer Cache라는 메모리 영역을 생략하고 기록한다.

```sql
--로그파일의 기록을 최소화하여 입력 성능을 향상시킨다. 
ALTER TABLE emp NOLOGGING;
```

