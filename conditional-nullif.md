---
description: 인수 1이 인수 2와 같으면 NULL. 인수 1과 인수 2가 같지 않으면 인수 1 리턴.
---

# NULLIF\(arg1, arg2\)

## NULLIF \(arg1, arg2\)

* arg1이 arg2와 같으면 NULL 값 반환하고, arg1과 arg2가 같지 않으면 arg1을 리턴한다.
* arg1 = arg2 -&gt; NULL
* arg1 != arg2 -&gt; arg1 

{% tabs %}
{% tab title="NULLIF" %}
```sql
SELECT NULLIF(1,1), NULLIF(1,2)
FROM dual;
--결과: NULL, 1
```
{% endtab %}

{% tab title="NULLIF 예시 2" %}
```sql
SELECT last_name, first_name, 
         NULLIF(LENGTH(last_name), LENGTH(first_name))
FROM employees;

/** last_name과 first_name의 문자 길이가 동일하면 NULL을 출력하고 
last_name과 first_name의 문자 길이가 동일하지 않으면 last_name을 출력한다 */
```
{% endtab %}
{% endtabs %}

