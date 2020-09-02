---
description: 연결연산자 - 각각의 열을 하나의 열처럼 합쳐서 출력하기 (Concatenation Operator)
---

# SELECT - 연결연산자

## 연결연산자 - 각각의 열을 하나의 열처럼 합쳐서 출력한

* 연결 연산자: 두 개의 세로선\(\| \|\)을 이용한다.
* 리터럴 문자: 테이블에 없는 문자를 사이에 껴서 출력하고 싶다면 두 개의 세로선 사이에 사용하고 싶은 문자를 작은 따옴표에 껴서 작성한다.

  ```text
  --예시: 성과 이름을 붙여서 사원명 출력하기
  SELECT first_name||' '||last_name "사원명"
  FROM employees ;

  /** 출력 결과

  사원명
  ---------
  Ellen Abel 
  ...
  */
  ```

  ```text
  --예시: 사원 이름과 직무명을 한 열에 표현하기
  SELECT first_name||', '||job_id as "Employee"
  FROM employees;

  /** 출력 결과 

  Employee
  ---------
  Ellen, SA_REP
  ...
  */
  ```

### 연결연산자 규칙

* sysdate와 함께 쓸 때는 이렇게

```text
SELECT '오늘 날짜는'||sysdate as "오늘 날짜는"
FROM dual;

/** 출력결과 

오늘 날짜는
------------------
오늘 날짜는20/06/28

*/
```

* 'My name's' 작은 따옴표 안에 또 넣지를 못하는데, 이때는 아래 처럼

```text
SELECT 'My name''s '||last_name as "My name's"
FROM employees;

--q는 리터럴 문자를 표현하기 위한 연산자
--문법: q'[문자]' 
--의미: 대괄호 안에를 문자로 인식하겠다
--[는 ^,!,{,( 등 다양하게 가능
--문자에 느낌표 표현해야 되면 
--다른 특수문자를 q 연산자와 함께 써주면 된다 
SELECT q'[My name's?]'||' '||last_name||'!' "My name's?"
FROM employees;

/** 출력결과 

My name's?
------------------
My name's? Abel!

*/
```

