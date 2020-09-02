# FUNCTION - 행 순서 함수

## 행 순서 관련 함수 

* 행 순서 관련 함수는  상위 행의 값을 하위에 출력하거나 하위 행의 값을 상위 행에 출력하게 할 수 있다. 
* 특정 위치의 행을 가지고 와서 출력할 수 있다. 

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xD589; &#xC21C;&#xC11C; &#xAD00;&#xB828; &#xC708;&#xB3C4;&#xC6B0; &#xD568;</th>
      <th
      style="text-align:left">&#xC124;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">FIRST_VALUE</td>
      <td style="text-align:left">
        <p>&#xD30C;&#xD2F0;&#xC158;&#xC5D0;&#xC11C; &#xAC00;&#xC7A5; &#xCC98;&#xC74C;&#xC5D0;
          &#xB098;&#xC624;&#xB294; &#xAC12;&#xC744; &#xAD6C;&#xD55C;&#xB2E4;</p>
        <p>MIN &#xD568;&#xC218;&#xB97C; &#xC0AC;&#xC6A9;&#xD574;&#xC11C; &#xAC19;&#xC740;
          &#xACB0;&#xACFC;&#xB97C; &#xAD6C;&#xD560; &#xC218; &#xC788;&#xB2E4;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">LAST_VALUE</td>
      <td style="text-align:left">
        <p>&#xD30C;&#xD2F0;&#xC158;&#xC5D0;&#xC11C; &#xAC00;&#xC7A5; &#xB098;&#xC911;&#xC5D0;
          &#xB098;&#xC624;&#xB294; &#xAC12;&#xC744; &#xAD6C;&#xD55C;&#xB2E4;</p>
        <p>MAX &#xD568;&#xC218;&#xB97C; &#xC0AC;&#xC6A9;&#xD574;&#xC11C; &#xAC19;&#xC740;
          &#xACB0;&#xACFC;&#xB97C; &#xAD6C;&#xD560; &#xC218; &#xC788;&#xB2E4;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">LAG</td>
      <td style="text-align:left">&#xC774;&#xC804; &#xD589;&#xC744; &#xAC00;&#xC9C0;&#xACE0; &#xC628;&#xB2E4;</td>
    </tr>
    <tr>
      <td style="text-align:left">LEAD</td>
      <td style="text-align:left">
        <p>&#xC708;&#xB3C4;&#xC6B0;&#xC5D0;&#xC11C; &#xD2B9;&#xC815; &#xC704;&#xCE58;&#xC758;
          &#xD589;&#xC744; &#xAC00;&#xC9C0;&#xACE0; &#xC628;&#xB2E4;</p>
        <p>&#xAE30;&#xBCF8; &#xAC12;&#xC740; 1&#xC774;&#xB2E4;</p>
      </td>
    </tr>
  </tbody>
</table>

### FIRST\_VALUE

```sql
SELECT department_id, last_name, salary, 
    FIRST_VALUE(last_name)               --첫 번째 행을 가지고 온다 
    OVER (PARTITION BY department_id     --부서 파티션을 만든다
    ORDER BY salary DESC                 --부서 내에서 급여가 가장 많은 사람 조
    ROWS UNBOUNDED PRECEDING) as DEPT_A 
FROM employees; 
```

![](.gitbook/assets/image%20%287%29.png)

### LAST\_VALUE

```sql
SELECT department_id, last_name, salary, 
    LAST_VALUE(last_name)               --마지 행을 가지고 온다 
    OVER (PARTITION BY department_id    --부서 파티션을 만든다
    ORDER BY salary DESC                --부서 내에서 급여가 가장 적은 사람 조
    BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING) as DEPT_B
FROM employees; 
```

### LAG

* LAG 함수는 이전 값을 가지고 오는 것. 

```sql
SELECT department_id, last_name, salary, 
    LAG(salary) OVER (ORDER BY salary DESC) AS PRE_SAL 
FROM employees ; 
```

![](.gitbook/assets/image%20%282%29.png)

### LEAD 

* LEAD 함수는 지정된 행의 값을 가지고 오는 것이다. 아래 예제는 salary에서 2번째 행의 값을 가지고 온다. 
* LEAD의 기본 값은 1이고, 첫 번째 행 값을 가지고 오는 것을 의미한다. 

```sql
SELECT department_id, last_name, salary, 
       LEAD(salary, 2) OVER (ORDER BY salary DESC) AS PRE_SAL 
FROM employees ; 
```

![](.gitbook/assets/image%20%2810%29.png)

