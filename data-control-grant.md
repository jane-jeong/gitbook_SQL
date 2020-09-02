# DCL - GRANT

## GRANT 

* GRANT문은 데이터베이스 사용자에게 권한을 부여한다. 
* 권한 : `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `REFERENCES`, `ALTER`, `INDEX`, `ALL`

{% tabs %}
{% tab title="GRANT 기본 문법" %}
```sql
GRANT SELECT, INSERT, UPDATE, DELETE --권한
ON employees
TO hr ; 
```
{% endtab %}
{% endtabs %}

### WITH GRANT/ADMIN OPTION 

* `WITH GRANT OPTION` : 특정 사용자에게 권한을 부여할 수 있는 권한을 부여한다. 권한을 A 사용자가 B에 부여하고 B가 다시 C를 부여한 후에 권한을 취소\(REVOKE\)하면 모든 권한이 회수된다. 
* `WITH ADMIN OPTION` : 테이블에 대한 모든 권한을 부여한다. 권한을 A 사용자가 B에 부여하고 다시 C를 부여한 후에 권한을 취소\(REVOKE\)하면 B 사용자 권한만 취소된다. 

{% tabs %}
{% tab title="WITH GRANT OPTION" %}
```sql
GRANT SELECT, INSERT, UPDATE, DELETE 
ON employees
TO hr WITH GRANT OPTION ; 
```
{% endtab %}
{% endtabs %}



