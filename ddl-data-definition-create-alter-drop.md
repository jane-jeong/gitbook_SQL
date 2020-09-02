# DDL - CREATE TABLE

## CREATE TABLE : 테이블 생성

### CREATE TABLE 기본 SYNTAX

{% tabs %}
{% tab title="CREATE TABLE 1" %}
```sql
Create Table EMP  --생성되는 테이블명은 영문자로 시작 
( 
    empno number(10) primary key --empno 컬럼을 기본키로 지정 
    ename varchar2(20), --데이터타입을 지정. Number는 숫자, varchar2는 가변길이 문자 
    sal number(6)
); 

--empno, ename, sal은 컬럼명
```
{% endtab %}

{% tab title="CREATE TABLE 2" %}
```sql
Create Table DEPT( 
    deptno varchar2(4) primary key, 
    deptname varchar2(20));
```
{% endtab %}

{% tab title="CREATE TABLE 3" %}
```sql
CREATE TABLE title     --CREATE TABLE 테이블명
(
id number,             --컬럼명1, 데이터타입
name varchar2(10),     --컬럼명2, 데이터타입
day date               --컬럼명3, 데이터타입 
)
tablespace user;       --tablespace 사용할테이블스페이스명
```
{% endtab %}
{% endtabs %}

### COLUMN DATA TYPE

{% hint style="info" %}
* number\(p, s\): 가변 길이 숫자 타입 \(p: 전체자리수, s:소수점자리수\)
* varchar2\(4000\): 가변 길이 문자 타입, 최대 크기: 4000
* char\(2000\): 고정 길이 문자 타입. 최대 크기: 2000
  * 고정 길이는 무조건 크기 2000을 차지한다. 공간 낭비를 초래할 수 있다. 그래서 보편적으로 varchar2 타입 사용한다.
* clob\(4gbyte\): 가변 길이 문자 타입 \(4gbyte 필수\)
  * 가변 길이지만 어느 정도 데이터를 확보해두어야 하기 때문에 공간 낭비가 있다. 쓰지 않는 것이 좋다.
* blob\(4gbyte\): 가변 길이 이진 데이터 타입.
  * 이미지 파일 등을 저장해두어야 할 때 사용하는 타입이다. 하지만 관리하기가 불편하다.
* bfile\(4gybte\): 외부 파일에 저장된 이진 데이터 타입이다.
  * blob의 단점을 보완한 것이다. 파일을 직접 저장하지 않는다. 외부 파일에 접근할 수 있도록 '포인터' 정보만 보유하고 있는 방식이다. 이미지\(학생부 사진\) 등 파일을 DB에 저장해두어야 한다면 보편적으로 bfile 타입을 사용한다.
* date: 날짜 데이터 타입
{% endhint %}

### NULL 값 대신 DEFAULT 값 입력되도록 설정하는 법

```sql
CREATE TABLE emp 
(
id number(4),
name varchar2(30),
day date default sysdate   
--date가 Null일 때 default로 sysdate를 넣어줘
)
tablespace users;
```

### CONSTRAINT : 제약 조건 사용하기

```sql
Create Table EMP(
    empno number(10), 
    ename varchar2(20), 
    sal number(10, 2) default 0,  --number(10,2) 소수점 둘째 자리까지 저장 
    deptno varchar2(4) not null, 
    createdate date default sysdate, 
    constraint emppk primary key(empno)
        consraint deptfk forign key(deptno) 
                                        references dept(deptno)); --DEPT 테이블이 마스터 테이블이 됨
```

### CASCADE : 참조 관계가 있을 경우 참조되는 데이터도 자동으로 삭제할 수 있는 옵션 사용

```sql
--우선 마스터 테이블이 될 DEPT 테이블을 만들고 인스턴스(데이터)를 두 개 입력한다 
CREATE TABLE DEPT 
( 
    deptno varchar2(4) primary key, 
    deptname varchar2(20)
); 

INSERT INTO DEPT VALUES ('1000','인사팀'); 
INSERT INTO DEPT VALUES ('1001','총무팀');
```

```sql
--ON DELETE CASACDE 옵션 사용해서 EMP 테이블을 생성한다 
CREATE TABLE EMP (
    empno number(10), 
    ename varchar2(20), 
    sal number(10,2) default 0, 
    deptno varchar2(4) not null, 
    createdate date default sysdate,
    constraint emppk primary key(empno),
    constraint deptfk foreign key(deptno) 
            references dept(deptno)
            ON DELETE CASCADE 
);

INSERT INTO EMP VALUES (100, '정재은', 1000, '1000', sysdate); 
INSERT INTO EMP VALUES (101, '을지문덕', 2000, '1001', sysdate);
```

#### ON DELETE CASCADE 옵션 사용한 테이블에서 데이터 삭제해보기

```text
DELETE FROM DEPT WHERE DEPTNO='1000'; 
SELECT * FROM EMP; 
SELECT * FROM DEPT;
```

ON DELETE CASCADE 옵션은 자신\(EMP\)이 참조하고 있는 테이블\(DEPT\)이 삭제되면 자동으로 자신도 삭제되는 옵션이다. 이 옵션을 사용하면 참조 무결성을 준수할 수 있다.

반대로, 마스터 테이블\(DEPT\)에는 부서번호가 없는데, 슬레이브 테이블\(EMP\)에는 해당 부서번호가 있는 경우, 데이터 관리를 적절하게 하고 있지 못하다고 할 수 있다. 이 경우는 참조 무결성에 위배된다고 한다.

