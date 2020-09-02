# DCL - REVOKE

## REVOKE

* REVOKE문은 데이터베이스 사용자에게 부여된 권환을 회수한다. 
* `REVOKE privileges ON object FROM user ;`

{% tabs %}
{% tab title="REVOKE 기본 문법" %}
```sql
REVOKE SELECT, INSERT, UPDATE, DELETE --권한
ON employees
FROM hr ;
```
{% endtab %}
{% endtabs %}

