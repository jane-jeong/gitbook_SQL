# 날짜 함수

## 날짜 계산하기

* date + number = 날짜
* date - number = 날짜
* date - date = 일수
* date + date = error
* date + 시간 = 날짜
* date + 시간 = 날짜

```text

```

## SYSDATE : 현재 날짜와 시간을 리턴하는 함

* sysdate: 현재 서버의 날짜, 시간을 리턴하는 함수
* oracle은 OS에 종속되어 있다.

```text
SELECT sysdate FROM dual;

--dual은 가상의 더미 테이블이다
```

* nls\_session\_parameters → nls\_date\_format을 확인한다

```text
SELECT * FROM nls_session_parameters;
--nls_date_format: RR/MM/DD
```

* TO\_CHAR \(날짜→문자\) 함수 활용해서 날짜에 시간 더하기

```text
--현재 서버시간에 1000일 더하고 아래 날짜시간모델요소로 표현하기
SELECT sysdate, 
to_char(sysdate+1000, 'yyyy-mm-dd hh24:mi:ss.sssss')
FROM dual; 

--시간 더하기: x시간을 더하고 싶다 = x/24로 표현 
--분 더하기: x/(24*60)
--초 더하기: x/(24*60*60) 

--10시간 10분 10초 더하기
SELECT sysdate, 
to_char(sysdate+10/24+10/(24*60)+10/(24*60*60), 
'yyyy-mm-dd hh24:mi:ss.sssss')
FROM dual;
```

* 날짜에서 날짜 빼기 - ROUND\(날짜-날짜\)

```text
SELECT round(sysdate-hire_date+1, 0) "근무일수"
FROM employees;
```

* MONTHS\_BETWEEN: 두 날짜 간의 달수를 리턴하는 함수
  * 결과는 number
  * 현재날짜, 과거날짜 순으로 표현해야 양수 값으로 나온다

```text
SELECT ROUND(months_between(sysdate, hire_date)) "근무달수"
FROM employees;
```

* ADD\_BETWEEN: 달수를 더하거나 빼는 함수

```text
SELECT sysdate, add_months(sysdate, 1),
             add_months(sysdate, -1) 
FROM dual;
```

* TO\_DATE 형변환 함수 활용 - 직접 날짜 넣어서 비교하기

```text
SELECT ROUND ( MONTHS_BETWEEN
( to_date('2020-11-06', 'yyyy-mm-dd'), 
to_date('2020-06-17', 'yyyy-mm-dd'), 1) "공부하는 기간"
FROM employees;
```

* NEXT\_DAY: 입력한 조건에 대하여 기준일과 가장 가까운\(첫번째\) 일자를 알려줌

```text
SELECT next_day(sysdate, 'friday') as "가장 가까운 금요일"
FROM dual;

ALTER SESSION SET nls_langauge = KOREAN ;

SELECT next_day(sysdate, '금요일') as "가장 가까운 금요일"
FROM dual;
```

* LAST\_DAY: 그 달의 마지막 일 리턴하는 함수

```text
SELECT last_day(sysdate) 
FROM dual;

SELECT last_day(to_date('2020-02-01', 'yyyy-mm-dd'))
FROM dual;
```

## 날짜 ROUND / TRUNC 함수

* ROUND\(기준일, 'month'\): 달을 기준으로, 일을 보고 반올림

```text
SELECT ROUND(to_date('2020-06-22', 'yyyy-mm-dd'), 'month') 
FROM dual; 
--결과: 20/07/01
--오라클은 16일부터는 그 다음 달의 1일로 반환

SELECT ROUND(to_date('2020-06-15', 'yyyy-mm-dd'), 'month') 
FROM dual; 
--결과: 20/07/01
--오라클은 15일까지는 그 달의 1일로 반환
```

* ROUND\(기준일, 'year'\): 해를 기준으로, 달을 보고 반올림

```text
SELECT ROUND(to_date('2020-06-16','yyyy-mm-dd'),'year')
FROM dual;
--6월까지는 올해 1월 1일로 

SELECT ROUND(to_date('2020-07-16','yyyy-mm-dd'),'year')
FROM dual;
--7월부터는 다음 해 1월 1일로
```

* TRUNC\(날짜, 'month'\): 그 달의 1일로 반환하는 함수
* TRUNC\(날짜, 'year': 그 해의 1월 1일로 반환하는 함수

```text
SELECT trunc(to_date('2020-06-16','yyyy-mm-dd'),'year')
from dual;
--결과: 20/01/01
```

