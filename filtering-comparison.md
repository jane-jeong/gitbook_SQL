---
description: Comparison Operators
---

# FILTERING - 비교연산자

## WHERE 절에서 비교연산자 사용해서 기준 컬럼 범위 검색 

### 1\) 비교연산자 : =, &gt;, &gt;=, &lt;, &lt;=

| 비교연산자 | 설 |
| :--- | :--- |
| = | 같은 것을 조회 |
| &lt; | 작은 것을 조회  |
| &lt;= | 작거나 같은 것을 조회  |
| &gt; | 큰 것을 조회  |
| &gt;= | 크거나 같은 것을  조회  |

{% tabs %}
{% tab title="비교연산자" %}
```sql
ISELECT *
FROM employees
where salary >=10000
and salary <= 20000;
```
{% endtab %}

{% tab title="비교연산자" %}
```sql
SELECT *
FROM employees
where salary >=10000
and department_id = 80;
```
{% endtab %}

{% tab title="비교연산자" %}
```sql
SELECT *
FROM employees
where salary >=10000
or department_id = 80;
```
{% endtab %}

{% tab title="비교연산자" %}
```sql
--기준컬럼 내 범위 검색 
SELECT * 
FROM employees 
WHERE salary >= 10000
and salary <= 20000;
```
{% endtab %}

{% tab title="비교연산자" %}
```sql
--기준컬럼 내 범위 검색 쉽게 하는 법 
SELECT * 
FROM employees 
WHERE salary Between 10000 and 20000;
```
{% endtab %}
{% endtabs %}

### 2\) 부정 비교연산자 : !=, ^=, &lt;&gt;, NOT 컬럼명 =, NOT 컬럼명 &gt; 

| 비교연산자 | 설명  |
| :--- | :--- |
| != | 같지 않은 것을 조회  |
| ^= | 같지 않은 것을 조회  |
| &lt;&gt; | 같지 않은 것을 조회  |
| NOT 컬럼 | 같지 않은 것을 조회  |
| NOT 컬럼명 &gt; | 크지 않은 것을 조회  |

