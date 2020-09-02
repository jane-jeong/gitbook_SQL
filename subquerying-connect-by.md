---
description: 'CONNECT BY : 계층형 조회 서브쿼리'
---

# CONNECT BY

## CONNECT BY

CONNECT BY는 계층형으로 데이터를 조회할 수 있는 것으로, ORACLE 데이터베이스에서 지원한다. 계층형 조회란, 예를 들어 상위 부장에서 차장, 차장에서 과장, 과장에서 대리, 대리에서 사원 순으로 트리 형태의 구조를 탐색하면서 조회하는 것이다. 역방향도 가능하다. 

CONNECT BY는 트리\(TREE\) 형태의 구조로 질의를 수행하는 것으로 START WITH 구는 시작 조건을 의미하고 CONNECT BY PRIOR은 조인 조건이다. ROOT 노드로부터 하위 노드의 질의를 실행한다. 

{% hint style="info" %}
케이스1: 인사팀에서 사원 DB를 관리하고 있다. 임직원 간의 관리자 계층구조를 파악하려고 한다. 즉, 특정 관리자 밑으로 어떻게 사원 계층구조가 만들어져있는지 확인하거나, 특정 임직원 위로 직속 상사 계층구조가 어떻게 만들어져있는지 확인하는 것이다. 이러한 계층구조를 파악할 때 CONNECT BY절과 START WITH절이 사용된다.
{% endhint %}

```sql
--CASE1 임직원 계층구조 파악하기 

--1) employee_id가 101번인 사원의 부하 직원의 계층구조를 출력해주세요.
SELECT employee_id, last_name, manager_id 
FROM employees 
START WITH employee_id=101 
CONNECT BY prior employee_id = manager_id ; 
/**
해석: 바로 전 단계의 employee_id(101번에서 시작)가 manager_id인 사람을 출력한다. 
(즉, manager_id가 101번인 사원들 = 101번이 매니저인 사람들) 
    그 중 가장 첫번째 행의 employee_id를 manager_id로 가지고 있는 사람을 출력한다. 
        그 중 가장 첫번째 행의 employee_id를 manager_id로 가지고 있는 사람을 출력한다. 
    없으면 다시 manager_id=101번인 사원들 중 두번째 행을 출력한다. 
        그 중 가장 첫번째의 행의 employee_id를 manager_id로 가지고 있는 사람을 출력한다.
  ......반복 ) */

--2) 100번 사원의 상사 계층 구조를 출력해주세요. 
SELECT employee_id, last_name, manager_id 
FROM employees 
START WITH employe_id=100
CONNECT BY prior manager_id = employee_id ; 
/** 해석: 
바로 전 단계의 manager_id가 employee_id와 같은 사람을 출력해.
employee_id=100인 사람의 manager_id가 employee_id가 같은 사람을 출력
= 100번 사원의 매니저를 보여주세요. = 100번 사원의 매니저 출력. (employee_id = a)
employee_id가 a인 사람의 매니저 아이디가 사원번호인 사람= a의 매니저를 출력해라 
그러니까 줄줄이 직속 상사가 출력된다. 
*/
```

{% hint style="info" %}
케이스2: 온라인 쇼핑몰에서 상품 카테고리의 DB를 만들었다. 그 DB 안의 상품 카테고리의 계층구조를 파악하려고 한다. 즉, 특정 카테고리의 하위 카테고리 계층 구조를 파악하거나, 혹은 특정 카테고리의 상위 카테고리 계층 구조가 어떻게 되는지 확인하고자 하는 것이다. 이때 사용되는 것이 CONNECT BY절과 START WITH절이다.
{% endhint %}

```sql
--쇼핑몰 FRONTEND에서는 카테고리 클릭-클릭해서 간단하게 보는데 
--BACKEND에서는 이런 계층구조로 DB에서 불러오는 SQL 쿼리가 설계되어 있는 것
--예를 들어, 쿠팡에서 식품-즉석식품,신선식품,어쩌구저쩌구, ~~~ 이렇게 카테고리가 있으면 

--1) 특정 카테고리의 하위 계층 구조 출력하기 
SELECT category_id, mother_category_id, product_id, title, price --mother_cateogry_id는 그 카테고리의 상위 카테고리
FROM products
START WITH category_id = 1 --'식품'의 카테고리_아이디가 1이라고 가정 
CONNECT BY prior category_id = mother_category_id ; --전 단계의 카테고리 아이디를 상위 카테고리 아이디로 가지고 있는 놈들을 찾아 
--1번에서 시작 
    --1번을 상위 카테고리 아이디로 가지고 있는 첫번째 놈을 찾아 
        --10번(즉석식품)이요. 
        --그럼 10번을 상위 카테고리 아이디로 가지고 있는 첫번째 놈을 찾아
            --100번(즉석밥)이요. 
            --그럼 100번을 상위 카테고리 아이디로 가지고 있는 첫번째 놈을 찾아
            --없어요. 
        --그래? 그러면 다시 10번을 상위 카테고리 아이디로 가지고 있는 두번째 놈을 찾아. 
            --200번(즉석카레)요. 
            --그럼 200번을 상위 카테고리 아이디로 가지고 있는 첫번째 놈을 찾아. 
            --없어요. 
        --그래? 그러면 다시 10번을 상위 카테고리 아이디로 가지고 있는 세번째 놈을 찾아. 
            --없어요. 
    --그래? 그러면 1번을 상위 카테고리 아이디로 가지고 있는 두번째 놈을 찾아. 
        --...

--2) 특정 카테고리의 상위 계층 구조 출력하기 
SELECT category_id, mother_category_id, product_id, title, price 
FROM products
START WITH category_id = 10
CONNECT BY category_id = prior mother_category_id 
/** 해석: 10번 카테고리의 상위 카테고리를 찾아. 계속 찾아. 끝날 때까지 ---- */
```

## LEVEL

* CONNECT BY절로 계층구조를 보여줄 때, 출력 결과에서 보기 너무 불편하기 때문에. 임의로 레벨 가상 열을 만들어줄 수 있다. 즉, LEVEL은 CONNECT BY와 쌍인 연산자이자 가상 열이다.
* --LEVEL 개념 --START WITH가 첫번째 레벨 \(레벨1\) --그 다음이 두번째 레벨 \(레벨2\) --그 다음이 세번째 레벨 \(레벨3\) --다시 돌아오게 되면 다시 두번째 레벨 \(레벨2\)

```sql
SELECT LEVEL, employee_id, last_name, manager_id
FROM employees 
START WITH employee_id = 101
CONNECT BY prior employee_id = manager_id ;
```

## LEVEL + LPAD 함수

* 조금 시각적으로 보기 좋게 표현하기 위해 정렬하는 기준 열에서 LPAD를 가지고 자릿수로 LEVEL을 표현해준다.

```sql
SELECT LEVEL, lpad(' ',2*level-2,' ')||last_name, manager_id
FROM employees 
START WITH employee_id = 101
CONNECT BY prior employee_id = manager_id ; 

/** 출력 결과: last_name 앞에 레벨 별로 공백을 넣어줌으로써 
시각적으로 계층구조를 표현할 수 있다. */
```

## ORDER SIBLINGS BY

* 조금 더 보기 좋게 정렬하기 위해, 레벨 구조는 그대로 두면서 그 레벨 안에서 특정 기준을 가지고 정렬시키고 싶을 때 ORDER SIBLINGS BY를 사용한다.
* ORDER SIBLINGS BY 안에는 LEVEL 개념이 녹아있다. 즉, LEVEL과 쌍인 개념이다.

```sql
--ORDER SIBLINGS BY 

SELECT LEVEL, lpad(' ',2*level-2,' ')||last_name, manager_id
FROM employees 
START WITH employee_id = 101
CONNECT BY prior employee_id = manager_id 
ORDER SIBLINGS BY last_name ; 

/** 계층구조는 그대로 유지된 채 같은 레벨 안에서만 
last_name 알파벳 기준으로 행들이 정렬된다*/

--LEVEL 열이 없어도 lpad 안에 level이 들어있어서 결과가 똑같이 실행된다.
```

## CONNECT BY 키워드 

계층형 조회에서 최대 계층의 수를 구하기 위한 문제는 MAX\(LEVEL\)을 사용해서 최대 계층 수\(트리의 최대 깊이\)를 구한다. 즉, 계층형 구조에서 마지막 LEAF NODE의 계층 값을 구한다. 

| CONNECT BY 키워드 | 설명 |
| :--- | :--- |
| LEVEL | 검색 항목의 깊이를 의미한다. 즉, 계층구조에서 가장 상위 레벨이 1이 된다. |
| CONNECT\_BY\_ROOT  | 계층 구조에서 가장 최상위 값을 표시한다. \(1로 표시\)  |
| CONNECT\_BY\_ISLEAF | 계층 구조에서 가장 최하위 값을 표시한다. \(1로 표시\) |
| SYS\_CONNECT\_BY\_PATH | 계층 구조에서 전체 전개 경로를 표시한다.  |
| NOCYCLE | 순환 구조가 발생지점까지만 전개된다.  |
| CONNECT\_BY\_ISCYCLE  | 순환 구조 발생 지점을 표시한다.  |

## \[문제\] SQL에서 1부터 100까지 출력해보세요.

```sql
SELECT LEVEL 
FROM dual 
START WITH 1 
CONNECT BY <= 100;
```

