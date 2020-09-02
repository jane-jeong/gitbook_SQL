# FILTERING - 날짜 범위 검색

## WHERE 절에서 날짜 데이터 범위를 찾을 때는 시/분/초 개념을 주의해야 한다

{% tabs %}
{% tab title="년-월-일 날짜 데이터의 범위 검색" %}
```sql
SELECT * 
FROM employees
WHERE hire_date 
BETWEEN TO_DATE('2003-01-01','yyyy-mm-dd')
AND TO_DATE('2003-12-31','yyyy-mm-dd');

SELECT * 
FROM employees
WHERE hire_date >= to_date ('2003-01-01','yyyy-mm-dd')
and hire_date < to_date ('2004-01-01','yyyy-mm-dd');

--발생 가능 문제: 만약 date가 주문일자 데이터면 시, 분, 초까지 있음 
--시, 분, 초까지 있는 데이터는 주의해야 한다
```
{% endtab %}

{% tab title="시:분:초가 있는 날짜 데이터의 범위 검색 \(예: 주문일자\)" %}
```sql
--주문일자와 같이 시, 분, 초가 있는 데이터는 아래처 바꿔줘야 한다. 
--특정 날의 시:분:초 부터 특정 날의 시:분:초까지 범위 검색을 하려면
SELECT * 
FROM employees
WHERE hire_date >= to_date ('2003-01-01 23:59:59','yyyy-mm-dd hh24:mi:ss')
AND hire_date < to_date ('2003-12-31 23:59:59','yyyy-mm-dd hh24:mi:ss');

--date의 범위를 다룰 때는 꼭 시, 분, 초 개념을 잊지 않을 것
```
{% endtab %}
{% endtabs %}

