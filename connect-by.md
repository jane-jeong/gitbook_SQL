# FUNCTION - 순위 함수 RANK\( \)

## 순위 함수

* 윈도우 함수는 특정 항목과 파티션에 대해서 순위를 계산할 수 있는 함수를 제공한다. 
* 순위 함수는 `RANK`, `DENSE_RANK`, `ROW_NUMBER` 함수가 있다. 

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xC21C;&#xC704; &#xD568;&#xC218;</th>
      <th style="text-align:left">&#xC124;&#xBA85;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>RANK() </code>
      </td>
      <td style="text-align:left">
        <p>&#xD2B9;&#xC815; &#xD56D;&#xBAA9; &#xBC0F; &#xD30C;&#xD2F0;&#xC158;&#xC5D0;
          &#xB300;&#xD574;&#xC11C; &#xC21C;&#xC704; &#xACC4;&#xC0B0;</p>
        <p>&#xB3D9;&#xC77C;&#xD55C; &#xC21C;&#xC704;&#xB294; &#xB3D9;&#xC77C;&#xD55C;
          &#xAC12;&#xC774; &#xBD80;&#xC5EC;&#xB428;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>DENSE_RANK()</code>
      </td>
      <td style="text-align:left">&#xB3D9;&#xC77C;&#xD55C; &#xC21C;&#xC704;&#xB97C; &#xD558;&#xB098;&#xC758;
        &#xAC74;&#xC218;&#xB85C; &#xACC4;&#xC0B0;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ROW_NUMBER()</code>
      </td>
      <td style="text-align:left">&#xB3D9;&#xC77C;&#xD55C; &#xC21C;&#xC704;&#xC5D0; &#xB300;&#xD574;&#xC11C;
        &#xACE0;&#xC720;&#xC758; &#xC21C;&#xC704;&#xB97C; &#xBD80;&#xC5EC;&#xD55C;&#xB2E4;</td>
    </tr>
  </tbody>
</table>

## RANK\( \) 

* `RANK()` 함수는 순위를 계산하고, 동일한 순위에게는 같은 순위를 부여한다. 
* `RANK() OVER (PARTITION BY job_id ORDER BY salary DESC)` 는 job\_id로 파티션을 만들고 job\_id별 순위를 조회하게 한다. 

```sql
SELECT last_name, salary, job_id, RANK() OVER (ORDER BY salary DESC) ALL_RANK, 
       RANK() OVER(PARTITION BY job_id ORDER BY salary DESC) JOB_RANK 
FROM employees ;
```

![... &#xC774;&#xD558; &#xC0DD;&#xB7B5;](.gitbook/assets/image%20%286%29.png)

## DENSE\_RANK\( \) 

* `DENSE_RANK()`는 동일한 순위를 하나의 건수로 인식해서 조회한다. 

```sql
SELECT last_name, salary, RANK() OVER (ORDER BY salary DESC) RANK, 
       DENSE_RANK() OVER (ORDER BY salary DESC) DENSE_RANK 
FROM employees ;
```

![DENSE\_RANK&#xC5D0;&#xB294; 3&#xC704;&#xAC00; &#xC788;&#xB2E4;. &#xC989; &#xBAA8;&#xB4E0; &#xC21C;&#xC704;&#xAC00; &#xC788;&#xB2E4;.](.gitbook/assets/image%20%2813%29.png)

## ROW\_NUMBER\( \) 

* `ROW_NUMBER()` 함수는 동일한 순위에 대해서 고유의 순위를 부여한다. 

```sql
SELECT last_name, salary, 
  RANK() OVER (ORDER BY salary DESC) ALL_RANK, 
  ROW_NUMBER() OVER (ORDER BY salary DESC) ROW_NUM
FROM employees ;   
```

![&#xB3D9;&#xC77C;&#xD55C; &#xC21C;&#xC704;&#xC5D0; &#xB300;&#xD574;&#xC11C; &#xAC01;&#xAC01; &#xACE0;&#xC720;&#xC758; &#xB85C;&#xC6B0; &#xB118;&#xBC84;&#xB97C; &#xBD80;&#xC5EC;&#xD574;&#xC900;&#xB2E4;](.gitbook/assets/image%20%2810%29.png)

