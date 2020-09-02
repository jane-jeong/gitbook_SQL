# BASE - SQL

## Reference Tutorial Site 

1. W3 School - [https://www.w3schools.com/sql/](https://www.w3schools.com/sql/)
2. SQL tutorials - [https://www.sqltutorial.org/](https://www.sqltutorial.org/)

## What is SQL? \(1\)

SQL은 Structured Query Language의 줄임말이다. 데이터베이스에 '질문'을 하기 위한 언어인데, 모든 사람이 공통의 규칙을 가지고 컴퓨터에게 질문을 할 수 있도록 언어를 구조화해서 잘 만들었다는 의미로 해석하면 되겠다. 

가장 많이 쓰이는 언어가 데이터베이스에 원하는 조건의 데이터를 요청\(Querying\)하는 SELECT 문이기 때문에 Query Language라고 이름을 붙인 듯하다. 하지만 데이터를 조회하는 것뿐만 아니라 SQL 언어는 데이터를 조작하고, 데이터와 데이터베이스를 관리할 수 있는 거의 모든 기능을 모두 수행할 수 있다. 

기능의 성격을 기준으로 DML, DDL, DCL, TCL 등으로 언어의 종류를 구분하곤 한다. SQL 언어의 종류는 아래처럼 정리할 수 있다. 

* DML은 Data Manipulation Language의 줄임말이다. 말그대로 데이터를 조작하는 것이다. 즉, 데이터를 조회하는 SELECT, 데이터를 삽입하는 INSERT, 데이터를 삭제하는 DELETE 구문이 있다. 
* DDL은 Data Definition Language의 줄임말이다. 테이블을 생성하는 CREATE, 테이블 정보를 변경하는 ALTER 등의 구문이 있다. 
* DCL은 Data Control Language의 줄임말이다.  데이터베이스에 대한 사용자의 권한을 부여하는 GRANT 구문과 권한을 회수하는 REVOKE 구문이 있다.
* TCL은 Transaction Control Language의 줄임말이다. 트랜잭션을 처리하는 기능을 수행한다. DML 언으를 수행한 후 트랜잭션이 발생하고, 이때 COMMIT 혹은 ROLLBACK 으로 트랜잭션을 처리해주어야 한다. COMMIT과 ROLLBACK은 SQL 공통 TCL 구문이다. 오라클에는 별도로 SAVEPOINT 구문이 있다. 참고로 DCL 역시 트랜잭션이 발생하지만, DCL 구문 수행과 동시에 자동 커밋되며, 이때 이전 트랜잭션까지 한꺼번에 커밋되기 때문에 이 점, 주의해야 한다.

## What is SQL? \(2\)

데이터베이스를 사용할 때, 데이터베이스에 접근할 수 있는 '구조 질의어'다. 데이터 정의어\(DDL\)와 데이터 조작어\(DML\)를 포함한 데이터베이스용 질의언어\(Query Language\)의 일종이다. SQL은 특정한 데이터베이스 시스템에 한정되지 않아 널리 사용된다. \(SQL은 '언어'일뿐 Oracle이나 MS DBMS에서 SQL 언어는 모두 동일하게 사용할 수 있다. \) SQL은 단순한 질의 기능뿐만 아니라 완전한 데이터 정의 기능과 조작 기능을 갖추고 있다. 온라인 단말기를 통해 대화식으로 사용할 수도 있고, 코볼이나 PL/I, C 등의 호스트 언어로 된 프로그램에 삽입되어서 사용되기도 한다.

* SQL은 Structured Query Language를 의미한다.
* SQL은 데이터베이스에 접속하고 조작할 수 있도록 해준다.
* SQL은1986년 ANSI\(American National Standards Institute\)의 표준이되었고, 1987년에는 ISO\(International Organization for Standardization\) 표준이 되었다.

## What Can do SQL do? 

* SQL은 데이터베이스에 질의를 수행한다.
* SQL은 데이터베이스로부터 데이터를 불러온다/검색한다\(retrieve\).
* SQL은 데이터베이스에 기록\(records\)을 삽입한다.
* SQL은 데이터베이스에서 기록\(records\)을 수정한다.
* SQL은 데이터베이스에서 기록\(records\)을 삭제한다.
* SQL은 새로운 데이터베이스를 생성한다.
* SQL은 데이터베이스에 새로운 테이블을 생성한다.
* SQL은 데이터베이스에 stored procedures를 생성한다.
* SQL은 데이터베이스에 뷰\(views\)를 생선한다.
* SQL은 테이블, 실행계획\(procedure\), 뷰의 권한을 설정한다.

## Using SQL in Your Web Site

데이터베이스에서 데이터를 불러와 보여주어야 하는 웹사이트를 만들기 위해서는

* RDBMS 데이터베이스 프로그램이 필요하다. \(ex. MySQL, SQL Server, MS Access 등\)
* PHP나 ASP와 같은 서버-사이드 스크립팅 언어를 사용해야 한다.
* 원하는 데이터를 불러오기 위해 SQL을 사용해야 한다.
* 페이지를 꾸미기 위해서 HTML / CSS 언어를 사용해야 한다.

## 데이터베이스의 개념 

사무 계산을 할 경우 각각의 업무 전용 데이터 파일을 사용하고 있지만 각 파일에는 중복된 정보가 들어 있는 것이 많다. 이 중복을 피하기 위하여 정보를 일원화하여 처리를 효율적으로 하기 위해서 서로 관련성을 가지며 중복이 없는 데이터의 집합을 데이터 베이스라 한다. 복수 업무에 공통으로 나타나는 데이터를 중심으로 모아서 이들을 상호 유기적으로 결합한 것. 이들 데이터에는 일정한 규칙에 따라 연결하여 이용할 수 있도록 되어 있다. 종래의 업무마다 독립된 파일 처리 바익에 비하여 업무가 확대되어도 새롭게 파일을 준비할 필요가 없고, 각 파일에 같은 데이터가 중복되어 있지 않게 되는 것 등의 이점이 있다. 데이터 베이스를 관리하는 시스템을 데이터 베이스 관리 시스템이라 한다.

## DBMS란?

데이터를 효과적으로 이용할 수 있도록 정리, 보관하기 위한 기본 소프트웨어다. DBMS는 데이터의 추가, 변경, 삭제, 검색 등의 기능을 집대성한 소프트웨어 패키지다. DBMS는 계층형, 네트워크형, 관계형으로 나눠지며 최근에는 관계형이 DBMS의 주류를 이루고 있다.

## RDBMS란?

* RDBMS는 Relational Database Management System을 의미한다. RDBMS는 SQL과 모든 현대적인 데이터베이스 시스템, 예를 들어 MS SQL Server, IBM DB2, Oracle, MySQL 과 Microsoft Access의 기반이 된다. RDBMS 안의 데이터는 테이블이라고 불리는 데이터베이스 오브젝트에 저장이 된다. 테이블이란 관계가 있는 데이터 엔트리의 집합이며 columns\(열\)과 rows\(행\)으로 구성된다.
* 모든 테이블은 'fields'라고 불리는 작은 엔티티로 분해된다. 예를 들어 'Custoemrs'라는 테이블은 CustoemrID, CustomerName, ContactName, Address, City, PostalCode, Country로 구성된다. 즉, 여기서 field란 테이블 안의 모든 record\(=row\)에 대해 특수한 정보를 품도록 설계된 한 column\(열\)을 의미한다.
* 'record'는 'row'로도 불리며, 테이블에 존재하는 독립적인 엔트리다. record\(row\)는 테이블에서 수평적인 엔티티이며, 컬럼\(열\)은 테이블에서 수직적인 엔티티다.

## 머신러닝의 간단한 개념

머신러닝은 '어떻게 하면 분류를 잘할까? 어떻게 하면 군집을 잘 만들까?' 고민하는 거다. 예측은 '회귀분석'이 핵심이고 '회귀분석'의 핵심은 '미분'이다. 미분식\(알고리즘\)은 이미 다 만들어져 있다. 내가 만들 필요 없이 가져다 쓰면 된다.

'내가 해결하려는 문제와 목표, 내 데이터셋에는 어떤 알고리즘을 사용하는 것이 가장 좋은 것인지' 판단하는 능력이 중요하다. 그래서 원리를 이해하는 교양수학이 중요하다.

