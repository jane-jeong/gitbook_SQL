# JOIN - OUTER JOIN \(ORACLE\)

## OUTER JOIN \(ORACLE\) 

* OUTER JON은 두 개의 테이블 간에 교집합\(EQUI JOIN\)을 조하고 한 쪽 테이블에만 있는 데이터도 함께 포함시켜서 조회한다. 
* LEFT OUTER JOIN : 왼쪽 테이블 전체 행을 포함 \(오른쪽 테이블 쪽에 \(+\) 기호 사용\)
* RIGHT OUTER JOIN : 오른쪽 테이블 전체 행을 포함 \(왼쪽 테이블 쪽에 \(+\) 기호 사용\)
* FULL OUTER JOIN : 왼쪽 테이블 전체 행, 오른쪽 테이블 전체 행 포함 \(양쪽 테이블에 \(+\) 기호 사용\) 

{% tabs %}
{% tab title="RIGHT OUTER JOIN" %}
```sql
SELECT * 
FROM employees e and departments d
WHERE e.department_id (+) = d.department_id ; 
```
{% endtab %}

{% tab title="LEFT OUTER JOIN" %}
```sql
SELECT * 
FROM employees e and departments d
WHERE e.department_id = d.department_id(+) ; 
```
{% endtab %}

{% tab title="FULL OUTER JOIN" %}
```sql
SELECT * 
FROM employees e and departments d
WHERE e.department_id(+) = d.department_id(+) ; 
```
{% endtab %}
{% endtabs %}

## 

