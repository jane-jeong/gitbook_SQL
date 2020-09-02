# FILTERING - IS \(NOT\) NULL

## NULL 값 조회하기 

* NULL을 조회할 때는 IS NULL을 사용하고 NULL 값이 아닌 것을 조회할 경우는 IS NOT NULL을 사용한다. 

{% tabs %}
{% tab title="IS NULL" %}
```sql
SELECT * FROM EMP 
WHERE MGR IS NULL ; 
```
{% endtab %}
{% endtabs %}

