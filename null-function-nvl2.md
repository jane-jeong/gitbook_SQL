---
description: '인수 1이 null이 아니면 인수 2, 인수1이 null이면 인수 3'
---

# NVL2\(arg1, arg2, arg3\)

## NVL2 \(arg1, arg2, arg3\)

* arg1이 NULL이 아니면 arg2를 출력하고, arg1이 NULL이면 arg3을 출력한다. 
* NVL 함수와 DECODE를 하나로 만든 것이다. 

{% tabs %}
{% tab title="NVL2 예시" %}
```sql
SELECT NVL2(commission_pct, 'NULL X', 'NULL O')
FROM employees;

/** COMMISSION_PCT가 NULL이 아니면 'NULL X'를 출력하고 
NULL이면 'NULL O'를 출력한다 */
```
{% endtab %}

{% tab title="NVL2 예시 2" %}
```sql
SELECT NVL2(commission_pct, salary*12+commission_pct, salary*12) "nvl2"
FROM employees;
```
{% endtab %}
{% endtabs %}

