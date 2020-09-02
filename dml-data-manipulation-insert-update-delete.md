# DML - INSERT

## INSERT : 테이블에 데이터 입력하기 

### INSERT 기본 문법 : INSERT INTO 테이블명 \(열\) VALUES\(데이터\)

* VALUE에서 문자열을 입력하는 경우 작은 따옴표\( ' ' \)를 사용해야 한다. 
* VALUE에 모든 컬럼에 대한 데이터를 입력하는 경우에는 컬럼명 생략할 수 있다.  \(데이터 타입 일치\)

{% tabs %}
{% tab title="INSERT" %}
```sql
INSERT INTO table_name (column1, column2)
VALUES (expression1, expression2) ;
```
{% endtab %}

{% tab title="INSERT EXAMPLE" %}
```sql
INSERT INTO emp(id,name,day)  
values(1,'홍길동',to_date('2020-01-01','yyyy-mm-dd'));

COMMIT; 
```
{% endtab %}

{% tab title="INSERT - 컬럼명 생략" %}
```sql
INSERT INTO table_name
VALUES (expression1, expression2) ;

COMMIT; or ROLLBACK;
```
{% endtab %}
{% endtabs %}

## SELECT 문으로 통째로 입력하는 방법

원본 테이블\(emp\)의 데이터를 조회해서 그 데이터만 새로운 테이블로 삽입할 수 있다. 그대신, 아래 조건을 충족해야 한다. 

* 입력 받는 테이블\(emp\_test\)은 사전에 생성되어 있어야 한다.
* 두 테이블의 열의 갯수와 데이터타입이 일치해야 한다.

#### 샘플 테이블 생성 

{% tabs %}
{% tab title="emp 테이블 생성" %}
```sql
# emp 
# 열: id, name, day
CREATE TABLE emp 
(
id number(4),
name varchar2(30),
day date default sysdate   
--date가 Null일 때 default로 sysdate를 넣어줘
)
tablespace users;

```
{% endtab %}

{% tab title="emp\_test 테이블 생성" %}
```sql
# emp_test
# 열: id, name, day
CREATE TABLE emp_test
(
id number(4),
name varchar2(30),
day date default sysdate   
--date가 Null일 때 default로 sysdate를 넣어줘
)
tablespace users;
```
{% endtab %}
{% endtabs %}

```sql
--emp 테이블의 모든 데이터를 조회해서 emp_test 테이블에 입력한다 
INSERT INTO emp_test 
    SELECT * FROM emp;
commit; 

# 1 행 이(가) 삽입되었습니다.
```

## NOLOGGING 옵 사용 

데이터베이스에 데이터를 입력하면 로그파일\(Log file\)에 그 정보를 기록한다. Check point라는 이벤트가 발생하면 로그파일의 데이터를 데이터 파일에 저장한다. 

NOLOGGING 옵션은 로그파일의 기록을 최소화시켜서 데이터를 입력할 때 성능을 향상시키는 방법이다. NOLOGGING 옵션은 Buffer Casche라는 메모리 영역을 생략하고 기록한다. 

```sql
ALTER TABLE DEPT NOLOGGING ; 
```

