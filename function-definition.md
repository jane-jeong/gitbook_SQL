# FUNCTION

```sql
ELECT last_name||first_name, 
             lower(concat(last_name,first_name))
FROM employees;
```

## 함수란?

* 기능의 프로그램 
* 단일행 함수와 여러행\(그룹\) 함수가 있다 
* 입력 &gt; 함수 &gt; 출력 
* 단일행 함수는 1개를 입력하고 1개를 출력한다 
* 함수는 중복해서 쓸 수 있다 

```sql
SELECT last_name||first_name, 
             lower(concat(last_name,first_name))
FROM employees;
```

## DUAL 테이블

* DUAL 테이블은 ORACLE 데이터베이스에 의해서 자동으로 생성되는 테이블이다. 
* ORACLE 데이터베이스 사용자가 임시로 사용할 수 있는 테이블로, 내장형 함수를 실행할 때도 사용할 수 있다. 
* ORACLE 데이터베이스의 모든 사용자가 사용할 수 있다. 

```sql
DESC DUAL ;
```

## 내장형 함수의 종류

| 문자형 내장 함수 | 설명 |
| :--- | :--- |
| ACSII\(문자\) | 문자 혹은 숫자를 ACSII 코드 값으로 변환한다. |
| CHAR\(ASCII 코드 값\) | ACSII 코드 값을 문자로 변환한다. |
| SUBSTR\(문자열, M, N\) | 문자열에서 M번째 위치부터 N개를 자른다. |
| CONCAT |  |
| LOWER |  |
| UPPER |  |
| LENGTH / LEN |  |
| LTRIM |  |
| RTRIM |  |
| TRIM |  |

```sql
SELECT SUBSTR('ABC', 1,2), LENGTH('A BC'), LTRIM('  ABC'), 
       LENGTH(LTRIM('  ABC'))
FROM DUAL ;
```

| 날짜형 내장 함 | 설 |
| :--- | :--- |
| SYSDATE | 오늘의 날짜를 날짜형 타입으로 알려준다 |
| EXTRACT\('YEAR' \| 'MONTH' \| 'DAY' from date\) | 날짜에서 년, 월, 일을 조회한다 |

```sql
SELECT SYSDATE, 
       EXTRACT(YEAR FROM SYSDATE) AS "YEAR", 
       TO_CHAR(SYSDATE, 'YYYYMMDD') AS "TODAY"
FROM DUAL ;
```

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xC22B;&#xC790;&#xD615; &#xB0B4;&#xC7A5; &#xD568;&#xC218;</th>
      <th style="text-align:left">&#xC124;&#xBA85;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">ABS(&#xC22B;&#xC790;)</td>
      <td style="text-align:left">&#xC22B;&#xC790;&#xC758; &#xC808;&#xB300;&#xAC12;&#xC744; &#xB9AC;&#xD134;&#xD55C;&#xB2E4;</td>
    </tr>
    <tr>
      <td style="text-align:left">SIGN(&#xC22B;&#xC790;)</td>
      <td style="text-align:left">&#xC591;&#xC218;, &#xC74C;&#xC218;, 0&#xC744; &#xAD6C;&#xBCC4;&#xD55C;&#xB2E4;</td>
    </tr>
    <tr>
      <td style="text-align:left">MOD(&#xC22B;&#xC790;1, &#xC22B;&#xC790;2)</td>
      <td style="text-align:left">
        <p>&#xC22B;&#xC790;1&#xC744; &#xC22B;&#xC790;2&#xB85C; &#xB098;&#xB204;&#xC5B4;
          &#xB098;&#xBA38;&#xC9C0;&#xB97C; &#xACC4;&#xC0B0;&#xD55C;&#xB2E4;.</p>
        <p>% &#xB97C; &#xC0AC;&#xC6A9;&#xD574;&#xB3C4; &#xB41C;&#xB2E4;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">CEIL/CEILING(&#xC22B;&#xC790;)</td>
      <td style="text-align:left">&#xC22B;&#xC790;&#xBCF4;&#xB2E4; &#xD06C;&#xAC70;&#xB098; &#xAC19;&#xC740;
        &#xCD5C;&#xC18C;&#xC758; &#xC815;&#xC218;&#xB97C; &#xB9AC;&#xD134;&#xD55C;&#xB2E4;</td>
    </tr>
    <tr>
      <td style="text-align:left">FLOOR(&#xC22B;&#xC790;)</td>
      <td style="text-align:left">&#xC22B;&#xC790;&#xBCF4;&#xB2E4; &#xC791;&#xAC70;&#xB098; &#xAC19;&#xC740;
        &#xCD5C;&#xB300;&#xC758; &#xC815;&#xC218;&#xB97C; &#xB9AC;&#xD134;&#xD55C;&#xB2E4;</td>
    </tr>
    <tr>
      <td style="text-align:left">ROUND(&#xC22B;&#xC790;, m)</td>
      <td style="text-align:left">
        <p>&#xC18C;&#xC218;&#xC810; m &#xC790;&#xB9AC;&#xC5D0;&#xC11C; &#xBC18;&#xC62C;&#xB9BC;&#xD55C;&#xB2E4;</p>
        <p>m&#xC758; &#xAE30;&#xBCF8;&#xAC12;&#xC740; 0&#xC774;&#xB2E4;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">TRUNC(&#xC22B;&#xC790;, m)</td>
      <td style="text-align:left">
        <p>&#xC18C;&#xC218;&#xC810; m &#xC790;&#xB9AC;&#xC5D0;&#xC11C; &#xC808;&#xC0AD;&#xD55C;&#xB2E4;</p>
        <p>m&#xC758; &#xAE30;&#xBCF8;&#xAC12;&#xC740; 0&#xC774;&#xB2E4;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">POWER(&#xC22B;&#xC790;, m)</td>
      <td style="text-align:left">&#xC22B;&#xC790;&#xB97C; m&#xBC88; &#xAC70;&#xB4ED;&#xC81C;&#xACF1;&#xD55C;&#xB2E4;</td>
    </tr>
  </tbody>
</table>

```sql
SELECT ABS(-1), SIGN(10), MOD(4,2), CEIL(10.9), FLOOR(10.1), ROUND(10.222,1)
FROM DUAL ;
```

