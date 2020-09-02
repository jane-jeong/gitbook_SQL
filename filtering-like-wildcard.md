---
description: 'LIKE : 문자 패턴을 찾는 연산자'
---

# FILTERING - LIKE \(+ WILDCARD\)

## LIKE : 문자 패턴을 찾는 연산자 \(숫자 X\)

* LIKE 문은 와일드카드를 사용해서 데이터를 필터링한다. 
* LIKE문에서 와일드를 사용하지 않으면 '='와 같은 결과 값을 출력한다. 

<table>
  <thead>
    <tr>
      <th style="text-align:left">WILDCARD</th>
      <th style="text-align:left">&#xC124;&#xBA85;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">%</td>
      <td style="text-align:left">
        <p>&#xC5B4;&#xB5A4; &#xBB38;&#xC790;&#xB97C; &#xD3EC;&#xD568;&#xD55C; &#xBAA8;&#xB4E0;
          &#xAC83;&#xC744; &#xC870;&#xD68C;&#xD55C;&#xB2E4;. (0&#xAC1C; &#xC774;&#xC0C1;
          &#xD328;&#xD134; &#xCC3E;&#xC74C;)</p>
        <p>&#xC608;&#xB97C; &#xB4E4;&#xC5B4; &apos;&#xC870;%&apos;&#xB294; &#xC870;&#xB85C;
          &#xC2DC;&#xC791;&#xD558;&#xB294; &#xBAA8;&#xB4E0; &#xBB38;&#xC790;&#xB97C;,
          &apos;%1&apos;&#xC740; 1&#xB85C; &#xB05D;&#xB098;&#xB294; &#xBAA8;&#xB4E0;
          &#xBB38;&#xC790;&#xB97C; &#xC870;&#xD68C;&#xD55C;&#xB2E4;.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&lt;</td>
      <td style="text-align:left">
        <p>&#xD55C; &#xAC1C;&#xC778; &#xB2E8;&#xC77C; &#xBB38;&#xC790;&#xB97C; &#xC870;&#xD68C;&#xD55C;&#xB2E4;.
          (1&#xAC1C; &#xD328;&#xD134; &#xCC3E;&#xC74C;)</p>
        <p>&#xC608;&#xB97C; &#xB4E4;&#xC5B4; &apos;&#xC870;_&apos;&#xB294; &#xC870;&#xB85C;
          &#xC2DC;&#xC791;&#xD558;&#xACE0; &#xB450; &#xAE00;&#xC790;&#xB85C; &#xC774;&#xB8E8;&#xC5B4;&#xC9C4;
          &#xBB38;&#xC790;&#xB97C; &#xC870;&#xD68C;&#xD55C;&#xB2E4;. (&#xC608;: &apos;&#xC870;&#xC870;&apos;,
          &apos;&#xC870;1&apos;)</p>
      </td>
    </tr>
  </tbody>
</table>

```text
SELECT *
FROM employees 
WHERE last_name like 'K%';

SELECT *
FROM employees 
WHERE last_name like 'K___';

SELECT *
FROM employees 
WHERE last_name like '_i%';



#잘못된 쿼리의 예
SELECT * 
FROM employees 
WHERE salary like '1%';
#문제점: 여기서 salary 컬럼이 문자열로 바뀌어 버린다. ora가 임의로 TO_CHAR(SALARY) 형변환함수 써버린다. 그래서 FULL SCAN이 된다.

#잘못된 쿼리의 예
SELECT *
FROM employees 
WHERE hire_date like '03%';
#문제점: INTERNAL_FUNCTION(HIRE_DATE) LIKE '03%' 인터널 펑션 쓴다. FULL SCAN.



#like 연산자 쓸 때 '_' 관련된 문제
SELECT *
FROM employees
WHERE job_id like 'SA%';

#가정하는거에요~ 데이터가 아래처럼 되어있다고 하면 
#SA_MAN, SA_REP, SAMAN 
#근데 나는 SA_MAN, SA_REP 이런 애들만 뽑고 싶어요! 이럴 경우에는?

SELECT *
FROM employees
WHERE job_id like 'SA\\_%' escape '\\';
#escape: \\바로 뒤에 있는 것은 문자로 인식하겠다는 선언! \\문자 아니어도 다른 특수문자도 가능.

#가정: SA_%MAN을 찾고 싶으면? SA_로 시작하면서 MAN으로 끝나는 문자 

SELECT *
FROM employees
WHERE job_id like 'SA\\_\\%MAN' escape '\\';

#'SA_%'라는 단어 찾기 
SELECT *
FROM employees
WHERE job_id like 'SA\\_\\%' escape '\\';

#'SA_%MA'라는 찾기

SELECT *
FROM employees
WHERE job_id like 'SA\\_\\%__' escape '\\';

--not like: 특정 문자 패턴을 포함하지 않는 목록 출력하기 
SELECT *
FROM employees
WHERE last_name not like 'K%';
```

## NOT LIKE : 특정 문자 패턴을 포함하지 않는 데이터 출력하기

```text
SELECT *
FROM employees
WHERE last_name not like 'K%';
```

