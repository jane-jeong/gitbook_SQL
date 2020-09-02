# GROUP BY GROUPING SETS

## GROUP BY GROUPING SETS

* GROUP BY GROUPING SETS — 내가 필요한 그룹 조합만 골라서 출력한다. 
* GROUP BY GROUPING SETS 함수는 GROUP BY에 나오는 컬럼의 순서와 관계없이 다양한 소계를 만들 수 있다. 
* 이때, GROUP BY절에서 나열되는 컬럼의 순서와 관계 없이 개별적으로 모두 처리한다. 
* 즉, 아례 예제 GROUP BY절에서 department\_id와 job\_id의 순서가 바뀌어도 결과는 같다. department\_id별로 합계를 조회하고, job\_id 별로 합계를 각각 조회한다. 즉, 서로 관계 없이 개별적으로 조회되는 것.   

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

![](.gitbook/assets/image%20%283%29.png)

![...&#xC774;&#xD558; &#xC0DD;&#xB7B5;](.gitbook/assets/image%20%288%29.png)

