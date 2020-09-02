# SORTING - ORDER BY

## ORDER BY : SELECT 조회 결과를 정렬한다 

* ORDER BY 절은 무조건 마지막 절에 기술한다 
* ASC : 오름차순 \(기본값\) 
* DESC : 내림차순 
* ORDER BY 절에 표현식, 열 별칭 사용할 수 있다 

{% tabs %}
{% tab title="ORDER BY 1" %}
```sql
SELECT employee_id, last_name, salary
FROM employees
WHERE department_id = 50
order by salary;
```
{% endtab %}

{% tab title="ORDER BY 2" %}
```sql
SELECT employee_id, last_name, salary*12 as ann_sal
FROM employees
WHERE department_id = 50
order by salary*12 desc;
```
{% endtab %}

{% tab title="ORDER BY 3" %}
```sql
SELECT employee_id, last_name, salary*12 as ann_sal
FROM employees
WHERE department_id = 50
order by ann_sal desc;
```
{% endtab %}

{% tab title="ORDER BY 4" %}
```sql
SELECT employee_id, last_name, salary*12 as "ann_sal"
FROM employees
WHERE department_id = 50
order by "ann_sal" desc;
```
{% endtab %}

{% tab title="ORDER BY 2개 컬럼" %}
```sql
SELECT * FROM emp 
ORDER BY ENAME ASC, SAL DESC ;
```
{% endtab %}
{% endtabs %}

## ORDER BY 위치 표기법 

{% tabs %}
{% tab title="ORDER BY 위치표기 1" %}
```sql
SELECT employee_id, last_name, salary*12 as "ann_sal"
FROM employees
WHERE department_id = 50
order by 3 desc;
```
{% endtab %}

{% tab title="ORDER BY 위치표기 2" %}
```sql
SELECT department_id, last_name, salary
FROM employees
order by 1 asc,3 desc;

```
{% endtab %}

{% tab title="ORDER BY 위치표기 3" %}
```sql
SELECT employee_id, last_name, hire_date
FROM employees
order by 3 desc;
```
{% endtab %}
{% endtabs %}

## ORDER BY 주의점 

* ORDER BY가 정렬을 하는 시점은 SELECT문의 다른 모든 절의 명령을 실행한 후 데이터를 출력하기 바로 직전이다.
* ORDER BY는 정렬을 하기 때문에 데이터베이스 메모리를 많이 사용하게 된다. 즉, 대량의 데이터를 정렬하게 되면 정렬로 인한 성능저하가 발생한다. 
* ORACLE 데이터베이스에서는 메모리 내부에 할당된 SORT\_AREA\_SIZE를 사용한다. 만약 SORT\_AREA\_SIZE가 너무 작으면 성능 저하가 발생한다. 
* 정렬을 회피하기 위해서는 인덱스를 생성할 때 사용자가 원하는 형태로 오름차순 혹은 내림차순으로 으로 생성해야 한다. 

## INDEX를 사용한 정렬 회피 

정렬은 ORACLE 데이터베이스에 부하를 주기 때문에 인덱스를 사용해서 ORDER BY 회피할 수 있다. 

#### 샘플 데이터 입력 

{% tabs %}
{% tab title="샘플 테이블 생성" %}
```sql
CREATE TABLE emp (
    empno number(10) primary key, 
    ename varchar2(20), 
    sal number(10)
    ) ; 
    
INSERT INTO emp VALUES(1000, 'james', 10000); 
INSERT INTO emp VALUES(2000, 'Adam', 20000); 
INSERT INTO emp VALUES(3000, 'Jane', 30000); 
```
{% endtab %}
{% endtabs %}

위와 같은 테이블 emp에서 SELECT 문을 실행하면 기본적으로 EMPNO를 기준으로 오름차순 정렬해서 출력한다. EMPNO가 PRIMARY KEY\(기본키\)이기 때문에 자동으로 오름차순 인덱스가 생성되는 것.

{% tabs %}
{% tab title="인덱스 내림차순 지정해주기" %}
```sql
SELECT /*+ INDEX_DESC(A) */ *
FROM EMP A ;  
```
{% endtab %}
{% endtabs %}

위와 같이 /\*+ INDEX\_DESC\(A\) \*/ 힌트를 사용해 EMP 테이블에 생성된 인덱스를 내림차순으로 읽게 지정하면 ORDER BY EMPNO DESC를 사용한 것과 같이 EMPNO 인덱스를 내림차순으로  읽을 수 있다. 

