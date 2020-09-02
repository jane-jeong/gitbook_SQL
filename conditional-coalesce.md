# COALESCE\(arg1, arg2, ...\)

## COALESCE\(arg1, arg2, arg3, ...\)

* 인수1이 null이면 인수 2, 인수2가 null이면 인수 3, 인수 3이 null이면 인수 4, ....
* 결과적으로 COALESCE 함수의 결과값은 하나만 나온다. 전체의 경우의 수는 하나다. 

{% tabs %}
{% tab title="COALESCE" %}
```sql
SELECT salary, commission_pct, 
COALESCE(salary*12+commission_pct, salary*12) as "comm_coal"
FROM employees;
```
{% endtab %}

{% tab title="COALESCE 예시" %}
```sql
SELECT salary, commission_pct, 
COALESCE(salary*12+commission_pct, salary*12)
FROM employees;
--결과적으로 값은 하나만 나옴 (경우의 수 하나)
```
{% endtab %}
{% endtabs %}

