# BASE - INSTALL & SETTING

## 오라클 SQLD 설치하기

### **1\) java \(jdk\) 설치**

SQLD는 java 기반으로 만들어진 소프트웨어라 먼저 java를 설치해주어야 한다. jdk는 개발 툴이고, jre는 가상머신이다.

#### PC에 java 설치되어 있는지 확인하기

```text
/** cmd 창에 아래처럼 입력해본다 */ 

java -version
```

### **2\) Oracle XE 설치하기 \(Oracle Database Express Edition\)**

Oracle Database Express Edition은 오라클 데이터베이스 중에 무료로 사용할 수 있는 제품이다. 무료라서 아래와 같은 기능 제약이 있다.

_3 Pluggable Databases_

_2 CPUs for foreground processes 2GB of RAM \(SGA and PGA combined\)_

_12GB of user data on disk \(irrespective of compression factor\)_

-설치할 때 오라클 DB의 admin 계정인 SYS의 패스워드를 설정해준다. 기억하기 쉬운 비밀번호로 입력해주자.

### 3\) Command Prompt에서 SQL\*PLUS 접속하기

SQLPLUS는 오라클에서 기본적으로 제공하는 DB 접속 툴이다. 오라클 XE를 설치할 때 자동으로 PATH에 Oracle 디렉토리가 삽입되서, 오라클 XE 설치 후에 cmd에서 sqlplus라고 치면 SQLPLUS로 바로 접속할 수 있다. 오라클 XE 설치한 후에 SYS 계정으로 로그인해본다.

```text
sqlplus /**SQL*PLUS 접속 */
Enter user-name: sys as sysdba /**conn sys as sysdba*/
Enter password: /**오라클 설치할 때 입력했던 비밀번호*/
```

### 4\) RUN SQL Command Line에서 계정 UNLOCK + 계정 만들기

오라클 XE 설치하면 RUN SQL Command Line이 설치되는데 여기서 SQL 언어로 명령할 수 있다. 오라클 XE가 기본적으로 제공하는 데이터베이스 계정 목록을 확인해보고, ACCOUNT\_STATUS가 LOCKED인 계정 잠금 해제해서 데이터베이스 이용해보자.

```text
-- connect 계정이름/계정비밀번호 as 롤 
connect sys/orcale as sysdba 
-- SYS session으로 들어가서 계정 관리 


-- DBA(DB Admin)의 데이터베이스 계정 목록 확인하기
SELECT * FROM dba_users;


-- LOCKED 계정 UNLOCK하기 (sysdba니까 가능하다) 
ALTER USER hr identified by hr account UNLOCK;


-- 새로운 계정 만들기 
CREATE USER (계정이름) IDENTIFIED BY (비밀번호) ; 
-- 계정에 권한 주기 
GRANT CREATE SESSION, CREATE TABLE, CREATE SEQUENCE, CREATE VIEW TO (계정이름) ;


-- 사용자 계정에 테이블 공간 설정 
ALTER USER (계정이름) default tablespace users ; 
-- 테이블 공간에 쿼터 할당
ALTER USER (계정이름) quota unlimited on users ;
```

## QUICK START

### 1\) 생성되어 있는 테이블/뷰 확인하기

TNAME, TABTYPE\(TABLE or VIEW\), CLUSTERID를 확인할 수 있다.

```text
SELECT * 
FROM tab;
```

### 2\) 테이블 생성하기 : CREATE TABLE

```text
--테이블 생성 

CREATE TABLE fruit (
    id varchar2(20) primary key, --아이디 (id가 프라이머리 키)
    name varchar2(10) not null,  --이름
    age number not null,         --나이
    email varchar2(40)           --이메일
) ;

CREATE TABLE Persons (
    ID int NOT NULL PRIMARY KEY,       --아이디(필수입력, primary key)
    LastName varchar(255) NOT NULL,    --성(필수입력)
    FirstName varchar(255),            --이름(필수X) 
    Age int                            --나이(필수X)
);
```

### 3\) 테이블 삭제 : DROP TABLE

```text
--테이블 삭제
DROP TABLE fruit purge ;
```

### 4\) 데이터 추가 : INSERT

```text
--데이터 추가 
INSERT INTO fruit values 
('jane', '정효경', 28, 'aroom1993@gmail.com');
--테이블을 생성했을 때 필드 순서대로 
--value에 해당하는 데이터들을 순서대로 넣어준다
```

### 5\) 데이터 수정 : UPDATE

```text
--데이터 수정
--name을 정효경에서 정재은으로 수정하기
UPDATE fruit set name='정재은' 
WHERE name='정효경' ;
```

### 6\) 데이터 삭제 : DELETE

```text
--테이블에서 1개 행 삭제하기 
DELETE fruit where id='jane';
```

