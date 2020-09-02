# GROUP BY CUBE

## GROUP BY CUBE

* CUBE는 CUBE 함수에 제시한 컬럼에 대해서 결합 가능한 모든 집계를 계산한다. 다차원 집계를 제공해서 다양하게 데이터를 분석할 수 있게 해준다. 
* 예를 들어, 부서와 직업을 CUBE로 사용하면 부서별 합계, 직업별 합계, 부서별 직업별 합계, 전체 합계가 조회된다. 즉, 조합할 수 있는 모든 경우의 수를 조합해 집계하는 것이다. 
* rollup 기능을 포함하고 모든 그룹화할 수 있는 것을 만드는 기능이다. 아래와 같은 결과를 모두 한꺼번에 출력하고 싶을 때 사용한다.
* SUM\(sal\) = {a,b,c} SUM\(sal\) = {a,b} SUM\(sal\) = {a.c} SUM\(sal\) = {b,c} SUM\(sal\) = {a} SUM\(sal\) = {b} SUM\(sal\) = {c} SUM\(sal\) = {}

{% tabs %}
{% tab title="CUBE 연산자의 문형 " %}
```sql
SELECT a, b, c, SUM(salary) --AVG, MAX, MIN 등 그룹함수 사용 가능하다
FROM table_name
GROUP BY CUBE (a, b, c) ;
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="CUBE 예제 " %}
```sql
SELECT department_id, job_id, SUM(salary) 
FROM employees 
GROUP BY CUBE (department_id, job_id);
```
{% endtab %}
{% endtabs %}

* 출력 결과 해석 - 전체합계, 직업별 합계, 부서별 합계, 부서별 직업별 합계 조회 
* 1행 : 전체 합계 
* 2행 : 

![...&#xC774;&#xD558; &#xC0DD;&#xB7B5;](.gitbook/assets/image%20%2813%29.png)

