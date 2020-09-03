# 최적화 - Index

## 인덱스 

인덱스는 데이터를 빠르게 검색할 수 있는 방법을 제공한다. 인덱스는 인덱스 키\(예: `employee_id` \)로 정렬\(sort\)되어 있기 때문에 원하는 데이터를 빠르게 조회한다. 인덱스는 오름차순/내림차순 탐색이 가능하다. 하나의 테이블에 여러 개의 인덱스를 생성할 수 있고 하나의 인덱스는 여러 개의 컬럼으로 구성될 수 있다. 테이블을 생성할 때 기본키\(PK\)에는 자동으로 인덱스가 만들어지고 인덱스의 이름은 `SYSXXXX` 로 생성된다. 

## 인덱스의 구조 

인덱스의 구조는 Root Block, Branch Block, Leaf Block으로 구성되고 Root Block은 인덱스 트리에서 가장 상위에 있는 노드를 의미하며 Branch Block은 다음 단계의 주소를 가지고 있는 포인터로 되어 있다. Leaf Block은 인덱스 키와 ROWID로 구성되고 인덱스 키는 정렬되어서 저장되어 있다. Leaf Block은 Double linked list 형태로 되어 있어서 양방향 탐색이 가능하다. Leaf BLock에서 인덱스 키를 읽으면 ROWID를 사용해서 employees 테이블의 행을 직접 읽을 수 있다. 

## 인덱스 생성 

인덱스는 CREATE INDEX 문을 사용해서 생성할 수 있다. 인덱스를 생성할 때는 한 개 이상의 컬럼을 사용해서 생성한다. 인덱스 키는 기본적으로 오름차순으로 정렬되고 CRATE INDEX 문을 작성할 때 DESC 구를 포함하면 내림차순으로 정렬한다. 

```sql
# last_name은 오름차순, salary는 내림차순 정렬해서 ind_emp 인덱스를 생성한다 
CREATE INDEX ind_emp ON employees (last_name ASC, salary DESC) ; 
```

## 인덱스 스캔 

### 인덱스 유일 스캔 \(Index Unique Scan\) 

Unique Index Scan은 인덱스의 키 값이 중복되지 않는 경우, 해당 인덱스를 사용할 때 발생한다. 예를 들어, employee\_id가 중복되지 않는 경우 특정 하나의 employee\_id를 조회한다. 

```sql
SELECT *
FROM employees 
WHERE employee_id = 100 ; 
```

### 인덱스 범위 스캔 \(Index Range Scan\) 

Index Range Scan은 SELECT 문에서 특정 범위를 조회하는 WHERE 문을 사용할 경우 발생한다. 예를 들어, Like, Between이 대표적이다. 물론 데이터 양이 적은 경우는 인덱스 자체를 실행하지 않고 TABLE FULL SCAN이 될 수 있다. Index Range Scan은 인덱스의 Leaf Block의 특정 범위를 스캔한 것이다. 

```sql
SELECT *
FROM employees 
WHERE employee_id >= 100 ; 
```

### 인덱스 전체 스캔 \(Index Full Scan\) 

인덱스 풀 스캔은 인덱스에서 검색되는 인덱스 키가 많은 경우에 Leaf Block의 처음부터 끝까지 전체를 읽어 들인다. 

```sql
SELECT last_name, salary 
FROM employees
WHERe last_name like 'K%' AND salary > 1000 ; 
```

### 참고 : 테이블 풀 스캔 시 High Water Mark의 의미 

테이블 풀 스캔은 테이블의 모든 데이터를 읽은 것을 의미한다. 테이블을 읽을 때 High Water Mark 이하까지만 테이블 풀 스캔을 한다. High Water Mark는 테이블에 데이터가 저장된 블록에서 최상위 위치를 의미하고 데이터가 삭제되면 High Water Mark가 변경된다. 

