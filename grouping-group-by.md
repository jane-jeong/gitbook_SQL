# GROUP BY / HAVING

## GROUP BY 

* GROUP BY는 테이블에서 소규모 행을 그룹화하여 합계, 평균, 최대 값, 최소 값 등을 계산할 수 있다. 
* HAVING 구에 조건문을 사용한다. 
* ORDER BY를 사용해서 정렬할 수 있다. 

{% tabs %}
{% tab title="GROUP BY" %}
```sql
SELECT employee_id, SUM(salary) 
FROM emp
GROUP BY employee_id ; 
```
{% endtab %}
{% endtabs %}

## HAVING 

* GROUP BY에 조건절을 사용하려면 WHERE이 아닌, HAVING을 사용해야 한다. WHERE 절은 GROUP BY 이전에 수행하며, GROUP BY에서는 WHERE 절에서 필터링된 데이터를 받아 사용한다. 

{% tabs %}
{% tab title="HAVING" %}
```sql
SELECT employee_id, SUM(salary) 
FROM emp
WHERE employee_id >= 50 
GROUP BY employee_id
HAVING SUM(salary) >= 10000 ; 
```
{% endtab %}
{% endtabs %}

