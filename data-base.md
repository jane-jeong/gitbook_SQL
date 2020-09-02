# 모델링 - 관계형 데이터베이스

## 관계형 데이터베이스

* 관계형 데이터베이스는 릴레이션에 데이터를 저장하고 관리한다.
* 관계형 데이터베이스의 특징은 릴레이션을 사용해서 집합 연산과 관계 연산을 할 수 있다는 것.

#### 집합 연산

* 합집합 : 두 개의 릴레이션을 하나로 합하는 것. 중복된 행은 한 번만 조회됨.
* 차집합: 본래 릴레이션에는 존재하고 다른 릴레이션에는 존재하지 않는 것을 조회함.
* 교집합: 두 개의 릴레이션 간 공통된 것 조회.
* 곱집합: 각 릴레이션에 존재하는 모든 데이터를 조합하여 연산함.

#### 관계 연산

* 선택 연산\(selection\): 릴레이션에서 조건에 맞는 행\(튜플\)만을 조회
* 투영 연산\(projection\): 릴레이션에서 조건에 맞는 속성만을 조회
* 결합 연산\(join\): 여러 릴레이션의 공통된 속성을 사용해서 새로운 릴레이션을 만들어냄
* 나누기 연산\(division\): 기준 릴레이션에서 나누는 릴레이션이 가지고 있는 속성과 동일한 값을 가지는 행을 추출하고 나누는 릴레이션의 속성을 삭제한 후 중복된 해을 제거하는 연산

#### 테이블의 구조

* 릴레이션은 최종적으로 데이터베이스 관리 시스템\(DBMS\)에서 테이블 형태로 만들어진다.
* 기본키\(Primary Key\)는 하나의 테이블에서 유일성과 최소성을 만족하면서 해당 테이블을 대표하는 키다.
* 테이블은 행과 칼럼으로 구성된다. 그 중에서 행\(row\)은 하나의 테이블에 저장되는 값으로 튜플\(tuple\)이라고도 한다.
* 칼럼\(Column\)은 어떤 데이터를 저장하기 위한 필드\(Field\)로 속성\(Attribute\)이라고도 한다.
* 외래키\(Foreign key\)는 다른 테이블의 기본키를 참조\(조인\)하는 칼럼이다. 예를 들어 EMP 테이블의 부서코드는 DEPT 테이블의 기본키인 부서코드를 참조한다.
* 외래키는 조인\(결합연산\)을 하기 위해 사용한다.
