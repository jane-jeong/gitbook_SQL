# FILTERING - ROWNUM / ROWID

## ROWNUM

* ROWNUM은 SELECT문의 결과에 대해서 논리적인 일련번호를 부여한다.
* ROWNUM은 조회되는 행 수를 제한할 때 많이 사용된다. 
* ROWNUM을 사용해서 한 개의 행을 가지고 올 수 있으나, 여러 개의 행을 가지고 올 때는 인라인 뷰\(+열 별칭\)를 사용해야 한다. 

{% tabs %}
{% tab title="ROWNUM으로 한 개 행 조회하기" %}
```sql
SELECT * 
FROM emp 
WHERE ROWNUM <= 1;
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title=" ROWNUM / 인라인 뷰로 여러 개의 행 조회하기" %}
```sql
SELECT * 
FROM (SELECT ROWNUM list, last_name FROM emp) --list는 열 별칭. 열별칭 사용해야 한다.
WHERE list <= 5 ;
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title=" 웹사이트 게시판 페이징할 때 많이 사용되는 SELECT 문" %}
```sql
-- 게시판 1페이지: 1부터 20까지의 행을 조회
SELECT * 
FROM ( SELECT ROWNUM list, contents FROM board) 
WHERE list between 1 AND 20 ;
```
{% endtab %}
{% endtabs %}

## ROWID

* ROWID는 ORACLE 데이터베이스 내에서 데이터를 구분할 수 있는 유일한 값이다. 
* ROWID는 `SELECT ROWID, EMPNO FROM EMP`와 같은 SELECT 문으로 확인할 수 있다. 
* ROWID는 데이터가 어떤 데이터 파일, 어떤 블록에 저장되어 있는지를 알 수 있다.

### ROWID의 구조

| 구조 | 길이 | 설명 |
| :--- | :--- | :--- |
| 오브젝트 번호 |  |  |
| 상대 파일번호 |  |  |
| 블록 번호 |  |  |
| 데이터 번호 |  |  |

{% tabs %}
{% tab title=" ROWID로 행 조회하기" %}
```sql
SELECT rowid, last_name
FROM employee ;
```
{% endtab %}
{% endtabs %}

