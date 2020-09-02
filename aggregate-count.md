# FUNCTION - COUNT\( \)

## COUNT 함수 

* COUNT\( \)는 행 수를 계산하는 함수다. 
* COUNT\(\*\)는 NULL 값을 포함한 모든 행의 수를 계산한다. 
* COUNT\(컬럼\)은 NULL 값을 제외한 행 수를 계산한다. 

{% tabs %}
{% tab title="COUNT\(\*\)" %}
```sql
SELECT COUNT(*)
FROM emp
WHERE employee_id >= 10 ; 
```
{% endtab %}

{% tab title="COUNT\(EMPLOYEE\_ID\)" %}
```sql
SELECT COUNT(employee_id) 
FROM emp ; 
```
{% endtab %}
{% endtabs %}

