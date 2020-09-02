# FILTERING - WHERE

## WHERE 절 : 행을 제한하는 / 특정한 행만 뽑는 

* 문자와 날짜를 정의할 때는 작은 따옴표\( '  ' \)로 묶어야 한다. 
* 영문자는 대소문자를 구분하기 때문에 대소문자 정확하게 표현할 것
* 지역마다 날짜 포맷이 다르다. 한국은 'RR/MM/DD'와 'YYYY-MM-DD'\(전세계 기본 포맷\)을 사용한다. 

```text
SELECT * 
FROM employees 
WHERE last_name = 'King'


SELECT * 
FROM employees 
WHERE hire_date = '07/08/10'


SELECT * 
FROM employees 
WHERE employee_id = 100 ;


SELECT*
FROM employees
WHERE salary > 10000;
--위에서 salary는 기준컬럼, 10000은 기준비교값   


SELECT * 
FROM NETFLIX 
WHERE lower(cast) = 'rooney mara';


SELECT * 
FROM employees 
WHERE Initcap(last_name) = 'King'; 
```

## 시스템 날짜 확인하고 NLS 세팅하기 

* 날짜 데이터타입은 굉장히 예민하다. SELECT 문을 사용하는 지역에 따라 날짜 형식이 다르기 때문에 일치시켜주어야 한다. 
* 현재 실행 세션이 어떤 나라로 설정되어 있는지 NLS 확인하고 지역에 따른 VALUE 값 확인한다. \(NLS : National Language Support\) 
* 어느 지역에서도 돌아갈 수 있도록 구문을 짜야 한다면 문자인지, 날짜인지를 명확하게 지시해주어야 한다. 

```text
SELECT * 
FROM nls_session_parameters;
--확인결과: NLS_DATE_FORMAT: RR/MM/DD

--국가 설정 바꾸기
alter session set nls_territory = AMERICA;

--언어 바꾸기 
ALTER session set nls_language = AMERICAN;
ALTER session set nls_language = 'simplified chinese'

--요일 확인하기 (char: character) (day=요일)
SELECT to_char(sysdate, 'day') from dual;
--확인결과: Thursday
```

## WHERE 절에서 문자/숫자/날짜 비교하기 

* 문자/숫자/날짜를 비교할 때는 형을 일치해주는 작업을 해야 한다.
* 문자 vs 숫자💪, 숫자가 더 힘이 세다. "문자가 숫자에게 맞춰준다."

```text
SELECT * 
FROM employees 
WHERE employee_id = 100 ; 
--여기서 employee_id는 NUMBER 타입이고, 100은 숫자다. 형 일치(O)

SELECT * 
FROM employees 
WHERE employee_id = '100' ; 
       --number vs   char 
--여기서 employee_id는 NUMBER 타입, '100'에서의 100은 문자다. 
--작은 따옴표 안에 넣어주면 '이건 문자다'라고 컴퓨터에게 정의해주는 거다. 
--그러니까 여기서는 형 일치가 안되어 있다. 
--그런데 숫자가 힘이 더 세니까, 
--문자인 100이 굽히고 숫자 100으로 바뀌어서 employee_id에 맞춰진다.

--사원번호가 숫자일 것으로 생각하는데(현재는 숫자이지만) 
--경우에 따라서 숫자처럼 보이는 것이 문자일 수도 있으니 
--꼭 TABLE DESC(ription)을 보고 데이터 타입을 확인하는 습관을 들인다. 
--참고: 출력 결과에서 숫자는 오른쪽 정렬, 문자는 왼쪽 정렬된다. 

--만약에 employee_id가 문자(char) 타입이라면 
SELECT * 
FROM employees 
WHERE employee_id = 100 ; 
        --char     -number
--이렇게 작성했을 때 char = number에서 number에 맞춰지니까 
--employee_id 기준 컬럼 데이터를 char -> number로 오라가 자동변형해서 출력한다.
--즉, 아래처럼 되는데 
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

* 문자 vs 날짜💪, "문자가 날짜에게 맞춰준다." \(현재 지역에 맞게 날짜 타입을 입력했을 경우\)

```text
SELECT * 
FROM employees
WHERE hire_date='2003-06-17';
       #date       #char
--char문자 타입이 date에게 맞춰져서 날짜를 검색해준다. 
--현재 세션(지역)의 NLS 날짜 타입이 yyyy-mm-dd이 맞을 때만 그렇게 수행해준다. 
--보통 어느 곳에서도 날짜 타입이 통용될 수 있으려면 한국 포맷('yyyy-mm-dd')이 좋다. 
--확실하게 하려면 to_date를 사용하는 것이 가장 좋다.

SELECT * 
FROM employees
WHERE hire_date='06-17-2003'; --보통 dd-mm-yyyy로 읽히는 포맷
--이런 식으로 이상하게 배열하면 오류난다. 
--오류: ORA-01843: not a valid month
--ORA가 봤을 때 month 자리에 17이 들어와있는데, 17 없다고 띠용하는 것 

--to_date 형 변환 함수 
--문자로 되어 있는 날짜를 시스템의 날짜 타입으로 변환하는 함수
--to_date 함수를 사용하면 NLS 날짜 타입이 어떤 형태이든 개의치 않고 사용할 수 있다. 
--'yyyy-mm-dd'는 '날짜 포맷 요소'인데 다양한 날짜 포맷 요소를 사용할 수 있다. 
SELECT * 
FROM employees
WHERE hire_date = to_date('2003-06-17','yyyy-mm-dd');
       --date            --문자를 날짜로
```

