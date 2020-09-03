# FUNCTION - 비율 함수

## 비율 관련 함수 

비율 관련 함수는 누적 백분율, 순서별 백분율, 파티션을 N분으로 분할한 결과 등을 조회할 수 있다. 

#### 비율 관련 윈도우 함수 

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xBE44;&#xC728; &#xAD00;&#xB828; &#xC708;&#xB3C4;&#xC6B0; &#xD568;&#xC218;</th>
      <th
      style="text-align:left">&#xC124;&#xBA85;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">CUME_DIST</td>
      <td style="text-align:left">
        <p>&#xD30C;&#xD2F0;&#xC158; &#xC804;&#xCCB4; &#xAC74;&#xC218;&#xC5D0;&#xC11C;
          &#xD604;&#xC7AC; &#xD589;&#xBCF4;&#xB2E4; &#xC791;&#xAC70;&#xB098; &#xAC19;&#xC740;
          &#xAC74;&#xC218;&#xC5D0; &#xB300;&#xD55C; &#xB204;&#xC801; &#xC870;&#xD68C;&#xD55C;&#xB2E4;.</p>
        <p>&#xB204;&#xC801; &#xBD84;&#xD3EC;&#xC0C1;&#xC5D0; &#xC704;&#xCE58;&#xB97C;
          0~1 &#xC0AC;&#xC774;&#xC758; &#xAC12;&#xC744; &#xAC00;&#xC9C4;&#xB2E4;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">PERCENT_RANK</td>
      <td style="text-align:left">&#xD30C;&#xD2F0;&#xC158;&#xC5D0;&#xC11C; &#xC81C;&#xC77C; &#xBA3C;&#xC800;
        &#xB098;&#xC628; &#xAC83;&#xC744; 0&#xC73C;&#xB85C; &#xC81C;&#xC77C; &#xB2A6;&#xAC8C;
        &#xB098;&#xC628; &#xAC83;&#xC744; 1&#xB85C; &#xD558;&#xC5EC; &#xAC12;&#xC774;
        &#xC544;&#xB2CC; &#xD589;&#xC758; &#xC21C;&#xC11C;&#xBCC4; &#xBC31;&#xBD84;&#xC728;&#xC744;
        &#xC870;&#xD68C;&#xD55C;&#xB2E4;</td>
    </tr>
    <tr>
      <td style="text-align:left">NTILE</td>
      <td style="text-align:left">&#xD30C;&#xD2F0;&#xC158;&#xBCC4;&#xB85C; &#xC804;&#xCCB4; &#xAC74;&#xC218;&#xB97C;
        ARGUMENT &#xAC12;&#xC73C;&#xB85C; N &#xB4F1;&#xBD84;&#xD55C; &#xACB0;&#xACFC;&#xB97C;
        &#xC870;&#xD68C;&#xD55C;&#xB2E4;</td>
    </tr>
    <tr>
      <td style="text-align:left">RATIO_TO_REPORT</td>
      <td style="text-align:left">&#xD30C;&#xD2F0;&#xC158; &#xB0B4;&#xC5D0; &#xC804;&#xCCB4; SUM(&#xCE7C;&#xB7FC;)&#xC5D0;
        &#xB300;&#xD55C; &#xD589; &#xBCC4; &#xCEEC;&#xB7FC; &#xAC12;&#xC758; &#xBC31;&#xBD84;&#xC728;&#xC744;
        &#xC18C;&#xC218;&#xC810;&#xAE4C;&#xC9C0; &#xC870;&#xD68C;&#xB41C;&#xB2E4;.</td>
    </tr>
  </tbody>
</table>

## PERCENT\_RANK\( \) 

PERCENT\_RANK\(\) 함수는 파티션에서 등수의 퍼센트를 구하는 것이다.

```sql
SELECT department_id, last_name, salary, 
    PERCENT_RANK() OVER(PARTITION BY department_id ORDER BY salary DESC) 
    as percent_salary
FROM employees ; 
```

## NTILE\( \)

NTILE\(4\)는 4등분으로 분할하라는 의미다. 아래의 예에서는 급여가 높은 순으로 1~4등분으로 분할한다. 

```sql
SELECT department_id, last_name, salary, 
    NTILE(4) OVER(ORDER BY salary DESC) as N_TILE
FROM employees ; 
```

