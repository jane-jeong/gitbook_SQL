# FILTERING - IN

## IN : 각 목록의 값과 일치하는 값을 찾는 연산자 

* IN 연산자는 OR의 의미를 가지고 있어서 하나의 조건만 만족해도 조회된다. 
* 단, IN 연산자는 성능이 좋지는 않은 편. 

{% tabs %}
{% tab title="IN" %}
```sql
SELECT *
FROM employees 
WHERE employee_id = 100
OR employee_id = 101
OR employee_id = 102;
--이렇게 찾고 싶을 때,IN 연산자를 사용할 수 있다. 
--각 목록의 값과 일치하는 값을 찾는 연산자: IN
--BUT 참고: IN 연산자는 성능이 좋지 않다.
```
{% endtab %}

{% tab title="IN 2" %}
```sql
SELECT *
FROM employees 
WHERE employee_id in (100,101,102);
--in 연산자는 각각 SELECT를 다 던진다. 즉 위 쿼리문에선 SELECT를 세 번 던지는 것.
--INDEX를 계속 계속 다시 타는 것.
--in 연산자는 각 목록의 값이 넓을 때. 즉, 100, 200, 369 이런 식으로 찾을 때 사용한다.
```
{% endtab %}

{% tab title="IN 3" %}
```sql
--100 다음 행이 101, 다음 행이 102가 나오는 것이 확실하다면 between 연산자 사용한다.
--각 목록의 값이 촘촘하게 붙어 있는 경우는 범위 스캔으로 가자 (비교연산자와 between)
SELECT *
FROM employees
WHERE employee_id between 100 and 102;
```
{% endtab %}
{% endtabs %}

## NOT IN : 리스트에 있는 값 제외하고 출력하는 연산자 

* IN이 OR의 의미를 포함하는 것과 반대로, NOT IN은 AND의 의미를 포함하고 있다. 

{% tabs %}
{% tab title="NOT IN - 목록에 있는 데이터 제외하고 검색하기" %}
```sql
SELECT *
FROM employees 
WHERE employee_id NOT IN (100,101,102);
```
{% endtab %}
{% endtabs %}

## IN 문에 여러 컬럼 사용하기 

{% tabs %}
{% tab title="IN 조건에 여러 컬럼 지정하기" %}
```sql
SELECT * 
FROM emp 
WHERE job_id, last_name 
IN (('ST_CLERK', 'King'), ('SA_SAP', 'James')) ; 
```
{% endtab %}
{% endtabs %}

