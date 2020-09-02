# FUCTION - 집계함수 종류

## 집계함수 종류

| 집계함수  | 설명  |
| :--- | :--- |
| `COUNT( )` | 행 수를 조회한다 |
| `SUM( )` | 합계를 계산한다 |
| `AVG( )` | 평균을 계산한다 |
| `MAX( )`   `MIN( )` | 최대값과 최소값을 계산한다 |
| `STDDEV( )` | 표준편차를 계산한다 |
| `VARIAN( )` | 분산을 계산한다 |

```sql
SELECT last_name, salary, 
       SUM(salary) OVER (PARTITION BY manager_id) SUM_MANAGER
FROM employees; 
```

![SUM\_MANAGER&#xB294; &#xD589; &#xBCC4;&#xB85C; &#xAC19;&#xC740; &#xAD00;&#xB9AC;&#xC790;&#xC758; &#xAE09;&#xC5EC; &#xD569;&#xACC4;&#xB97C; &#xBCF4;&#xC5EC;&#xC900;&#xB2E4;](.gitbook/assets/image%20%282%29.png)

## COUNT 함수

* COUNT\( \)는 행 수를 계산하는 함수다. 
* COUNT\(\*\)는 NULL 값을 포함한 모든 행의 수를 계산한다. 
* COUNT\(컬럼\)은 NULL 값을 제외한 행 수를 계산한다. 

{% tabs %}
{% tab title="COUNT\(\*\)" %}
```sql
SELECT COUNT(*)
FROM emp
WHERE employee_id >= 10 ;
```
{% endtab %}
{% endtabs %}

