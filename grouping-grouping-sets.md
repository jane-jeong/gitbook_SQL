# GROUP BY GROUPING SETS

## GROUP BY GROUPING SETS

* GROUP BY GROUPING SETS — 내가 필요한 그룹 조합만 골라서 출력

{% tabs %}
{% tab title="GROUPING SETS의 문형 " %}
```sql
--GROUPING SETS의 문형 

SELECT a, b, c, SUM(salary) 
FROM tablename 
GROUP BY grouping sets ((a,b), (b,c), ()); 

/** 출력 결과 
sum(sal) = {a,b}
sum(sal) = {b,c}
sum(sal) = {}
*/
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="GROUPING SETS 예제" %}
```sql
SELECT depmartment_id, job_id, manager_id, SUM(salary) 
FROM employees 
GROUP BY GROUPING SETS ((department_id, job_id), (job_id, manager_id), (manager_id));

/**결과 해석: 
(1) department_id, job_id 별로 SUM(salary) 정리한 목록 
(2) job_id, manager_id 별로 SUM(salary) 정리한 목록 
(3) manager_id 별로 SUM(salary) 정리한 목록을 한꺼번에 출력 */
```
{% endtab %}
{% endtabs %}

![](.gitbook/assets/image%20%284%29.png)

![](.gitbook/assets/image%20%285%29.png)

