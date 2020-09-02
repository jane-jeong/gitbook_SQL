# NVL\(arg1, arg2\)

## NVL 함수 

* NVL \(arg1, arg2\) : arg1이 NULL이면 arg2로 리턴한다.

{% tabs %}
{% tab title="NVL" %}
```sql
NVL(COMMISSION_PCT, 0) 
-- COMMISSION_PCT가 NULL이면 0으로 값을 채워서 출력한다 
```
{% endtab %}

{% tab title="NVL 열별칭 사용" %}
```sql
SELECT employee_id, NVL(commission_pct, 0) as "comm" 
FROM employees ; 
```
{% endtab %}
{% endtabs %}



