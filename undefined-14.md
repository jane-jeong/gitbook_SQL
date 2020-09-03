# 최적화 - Table Partition

## 테이블 파티션 

## 파티션\(Partition\)의 기능 

* 파티션은 대용량의 테이블을 여러 개의 데이터 파일에 분리해서 저장할 수 있도록 한다. 
* 테이블의 데이터가 물리적으로 데이터 파일에 저장되면 입력, 수정, 삭제, 조회 성능이 향상된다. 
* 파티션을 각각의 파티션 별로 독립적으로 관리할 수 있다. 즉, 파티션 별로 백업하고 복구가 가능하면 파티션 전용 인덱스를 생성하는 것도 가능하다. 
* 파티션은 오라클 데이터베이스의 논리적 관리 단위인 테이블 스페이스 간에 이동이 가능하다. 
* 데이터를 조회할 때 데이터의 범위를 줄여서 성능을 향상시킨다. 

## RANGE PARTITION 

* Range Partition은 테이블의 컬럼 중에서 값의 범위를 기준으로 해서 여러 개의 파티션으로 데이터를  나누어 정리하는 것이다. 
* \(예\) salary 값 2000~4000은 Datafile.dbf 파일에 저장하고 salary 5000에서 7000 사이의 값은 Datafile2.dbf에 저장한다. 

## LIST PARTITION 

* List Partition은 특정 값을 기준으로 분할하는 방법이다. 
* \(예\) department\_id가 10번인 것은 Datafile.dbf에 저장하고, 20번 인 은 Datafile2.dbf에 저장한다. 

## HASH PARTITION 

* Hash Partition은 데이터베이스 관리 시스템이 내부적으로 해시함수를 사용해서 데이터를 분할한다. 
* 결과적으로 데이터베이스 관리 시스템이 알아서 분할하고 관리하는 것이다. 

## COMPOSITE PARTITION 

* Composite Partition은 여러 개의 파티션 기법을 조합해서 사용하는 것이다. 

## 파티션 인덱스 

* 파티션 인덱스는 4가지 유형의 인덱스를 제공한다. 즉, 파티션 키를 사용해서 인덱스를 만드는 Prefixed Index와 해당 파티션만 사용하는 Local Index 등으로 나누어진다. 
* 오라클 데이터베이스는 Global Non-Prefixed를 지원하지 않는다. 

| 파티션 인덱스    | 설명   |
| :--- | :--- |
| Global Index  | 여러 개의 파티션에서 하나의 인덱스만 조회한다  |
| Local Index  | 해당 파티션 별로 각자의 인덱스를 사용한다  |
| Prefixed Index  | 파티션 키와 인덱스 키가 동일하다  |
| Non Prefixed Index | 파티션 키와 인덱스 키가 다르다  |



