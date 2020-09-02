# 형변환 함수

## 명시적 형변환 함수와 암시적 형변환 함

* 형변환이란 두 개의 데이터의 데이터타입이 일치하도록 변환하는 것이다. 
* 형변환은 명시적 형변환과 암시적 형변환으로 구분된다. 
* 명시적\(Explicit\) 형변환은 형변환 함수를 사용해서 데이터 타입을 일치시키는 것으로 개발자가 형변환 함수 사용해서 데이터 타입을 변환해주어야 한다. 
* 암시적\(Implicit\) 형변환은 개발자가 형변환을 하지 않은 경우 DBMS가 자동으로 형변환을 하는 것이다. 암시적 형변환의 범위는 한정적이다. 

### 인덱스 컬럼에 형변환을 수행하면 인덱스를 사용하지 못한다

* 인덱스\(index\)는 데이터를 빠르게 조회하기 위해서 인덱스 키를 기준으로 정렬해 놓은 데이터다. 
* 기본적으로, 인덱스에 변형이 발생하면 인덱스를 사용할 수 없다. \(예외가 있긴 하다.\) 
* 따라서 인덱스가 있어도 인덱스 컬럼에 형변환이 발생하면 인덱스를 사용할 수 없다. 

```sql
SELECT * FROM emp 
WHERE employee_id = '100' ;
```

* 위 예시에서 employee\_id 컬럼은 숫자형 타입인 반면, 일치 조건에 걸린 '100'은 문자열이다. 이때, DBMS 내부적으로 자동으로 TO\_CHAR\(employee\_id\)로 암시적 형변환해서 데이터 타입을 일치시킨다. 
* employee\_id는 숫자형 타입이고 기본키\(primary key\)이기 때문에 자동으로 인덱스가 생성되어 있는 컬럼이다. 하지만, 암시적 형변환으로 employee\_id가 TO\_CHAR\(employee\_id\)가 되기 때문에 인덱스를 사용할 수  없다. 
* 이럴 때는 **컬럼이 암시적으로 변형되지 않도, 검색 조건인 '100'을 TO\_NUMBER\('100\)으로 명시적 형변환해**서 컬럼과 데이터 타입을 일치시켜 비교한다. 

## 명시적 형변환 함수의 종류

| 명시적 형변환 함수 | 설명 |
| :--- | :--- |
| TO\_NUMBER\(문자열\) | 문자열을 숫자로 변환한다. |
| TO\_DATE\(문자열, FORMAT\) | 문자열을 지정된 FORMAT의 날짜형으로 변환한다. |
| TO\_CHAR\(숫자 혹은 날짜, \[FORMAT\]\) | 숫자 혹은 문자를 지정한 FORMAT의 문자로 변환한다. |

## 1\) TO\_NUMBER : 숫자로 형변환하는 함수

```sql
SELECT * 
FROM employees 
WHERE to_number(employee_id) = 100 ; 
--실행계획(F10)을 확인해보면, FULL SCAN이 된다. 
--기준 컬럼을 변환하게 되면 그 기준 컬럼의 인덱스를 쓸 수 없으니(Q) FULL TABLE SCAN이 된다. 
--그것보다는 100 쪽을 문자 타입 '100' 혹은 to_char(100)으로 바꿔주는 게 더 낫겠지

--다시 employee_id가 숫자 타입인 상황으로 돌아와서, 
SELECT * 
FROM employees 
where employee_id=to_number('100');
       --number    -number로 형 변환됨 
--이 경우는 기준 컬럼 데이터가 변환되는 것이 아니기 때문에 INDEX SCAN이다.
```

## 2\) TO\_DATE : 날짜로 형변환하는 함수

문자로 되어 있는 날짜를 시스템의 날짜 타입으로 변환하는 함수다. to\_date 함수를 사용하면 NLS 날짜 타입이 어떤 형태이든 개의치 않고 사용할 수 있다. 'yyyy-mm-dd'는 '날짜 포맷 요소'인데 다양한 날짜 포맷 요소를 사용할 수 있다.

```sql
SELECT * 
FROM employees
WHERE hire_date = to_date('2003-06-17','yyyy-mm-dd');
       --date            --문자를 날짜로
```

## 4\) TO\_CHAR : 문자로 형변환하는 함수

날짜 형식을 특정한 날짜 문자로 변환해준다.

* date를 문자형으로 변환하는 함수
* to\_char\(날짜, '날짜시간모델요소'\)

```sql
SELECT to_char(sysdate, 'day') from dual;
--확인결과: Thursday
```

```sql
SELECT sysdate, to_char(sysdate, 'yyyymmddhh24miss')
FROM dual; 

SELECT to_char(sysdate, 'yyyy year month mon mm')
FROM dual; 
--year, month는 날짜를 언어문자로 표현해달라는 것. 
--이렇게 쓰면 nls_language에 종속되니 확인하고 사용할 것 

SELECT to_char(sysdate, 'syyyy year month mon mm')
FROM dual;
--syyyy는 기원후. 굳이 s 쓰지 않아도 자동으로 들어간다. 

SELECT to_char(sysdate, 'ddd dd d') 
FROM dual;
--ddd는 365일 중에 지금 몇 일째냐
--dd는 이번 달 중에 몇 일째냐
--d는 이번 주 중에 몇 일쨰냐 

SELECT to_char(sysdate, 'ddd dd d day dy')
FROM dual; 
--day: 요일 
--dy: '월요일'에서 '요일' 뺌 

SELECT to_char(sysdate, 'ww w') 
FROM dual; 
--ww: 그 해에서 기준일이 몇 주 째인지?
--w: 그 달에서 기준일이 몇 주 째인지? 
--결과: 25 4 

SELECT to_char(sysdate, 'q')
FROM dual; 
--q: 분기 

SELECT to_char(sysdate+100, 'q"분기"')
FROM dual; 
--열별칭이 아니라 문법이기 때문에 
--내가 표현하려고 하는 요소 바로 옆에
--"" 큰 따옴표로 붙여주고 싶은 단어를 붙인다 

SELECT to_char(sysdate, 'hh:mi:ss.sssss')
from dual;

SELECT to_char(sysdate, 'hh12:mi:ss.sssss')
from dual;
--hh의 기본은 12시간. hh=hh12. 
--24시간으로 바꿔주려면 hh24로 표현하기 

SELECT to_char(sysdate, 'hh24:mi:ss.sssss')
from dual;

SELECT to_char(sysdate, 'hh12:mi:ss.sssss am pm')
from dual;
--am pm이라고 쓴다고 오전 오후로 바로 나오는 게 아니라 알아서 변환해준다. 
--am->오후로 뜰 수도 있고, pm->오전으로 뜰 수도 있다.

SELECT to_char(sysdate, 'hh:mi:ss.sssss')
from dual;
--초는 다섯자리까지 밖에 못 쓴다.

--기원전/기원후 표현 (bc 또는 ad 둘 다 똑같다. 둘 중 하나만 쓰면 된다. 기원후=서기)
SELECT to_char(sysdate, 'bc ad syyyy hh:mi:ss.sssss')
from dual;
```

## TO\_CHAR, TO\_NUMBER

* TO\_NUMBER: '숫자문자' → '숫자'로 형변환 함수
* TO\_CHAR: '숫자' → '숫자문자'로 형변환함수

```sql
SELECT to_number('10') 
from dual;
--결과: 10 

SELECT employee_id, salary, to_char(salary, '000,999.000')
FROM employees;
#결과: 024,000.000

SELECT employee_id, salary, to_char(salary, '999,999.000')
FROM employees;
--결과: 24,000.000

--통화 포맷 확인
SELECT * FROM nls_session_parameters;

--'l' 알파벳 l 을 숫자 앞에 붙여주면 nls 통화 기호 붙음  
SELECT employee_id, salary, to_char(salary, 'l999,999.000')
FROM employees;
--결과: ￦24,000.000
--999는 자릿수 채워지지 않으면 굳이 0 쓰지 않는다

SELECT employee_id, salary, to_char(salary, 'l000,999.000')
FROM employees;
--결과: ￦024,000.000
--000은 자릿수 채워지지 않으면 0으로 채운다 

SELECT * from nls_session_parameters;
ALTER session set nls_territory = GERMANY ;

SELECT employee_id, salary, to_char(salary, 'l999G99D00')
FROM employees;
#결과: €240.00,00

ALTER session set nls_territory = FRANCE ;
ALTER session set nls_territory = KOREA ;

SELECT employee_id, salary, to_char(salary, 'l999G99D00')
FROM employees;

--통화 기호나 '.',',' 부호 상관 없이 결과값 출력하려면 
--'l999G99D00'이런 식으로 출력하면 된다 

--만국 공통 통화 기호 $를 붙일 수도 있다 
SELECT employee_id, salary, to_char(salary, '$999G99D00')
FROM employees;
```

## YY와 RR - 날짜 연도의 '세기' 개념

```sql
--날짜의 '세기' 개념과 그 표현 
--YY 타입이 뭐고, RR 타입이 무엇인지 

--1995가 나오네? 2095일 수도 있는데 
SELECT to_char(to_date('95-10-27','rr-mm-dd'),'yyyy')
FROM dual;

--yy-mm-dd에서는 2095가 나오네?
SELECT to_char(to_date('95-10-27','yy-mm-dd'),'yyyy')
FROM dual;

#왜 세기를 쓰지 않고 연도만 썼을까? 
    #storage 낭비

--YY: 현재 년도의 세기를 반영 
--RR: 
/**                             지정된 연도 
               0~49                                 50~99
현재연도
0~49  반환날짜는 현재 세기를 반영             반환날짜는 이전 세기를 반영
50~99 반환날짜는 이후 세기를 반영             반환날짜는 현재 세기를 반영 
*/

--1995가 나오네? 2095일 수도 있는데 
SELECT to_char(to_date('95-10-27','rr-mm-dd'),'yyyy')
FROM dual;

/**
현재년도 데이터 입력날짜(지정된연도) rr? yy?
현재 1994, 지정연도 95-10-27 = rr은 1995, yy는 1995 
현재 1994, 지정연도 17-10-27 = rr은 2017, yy는 1917
현재 2001, 지정연도 17-10-27 = rr은 2017, yy는 2017
현재 2048, 지정연도 52-10-27 = rr은 1952, yy는 2052
현재 2051, 지정연도 47-10-27 = rr은 2147, yy는 2051
*/
```

