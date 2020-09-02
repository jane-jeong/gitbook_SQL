# 문자 함수

## 단일행 함수 - 문자 함수 \(15개\)

### 1\) upper : 대문자 변환 함수

### 2\) lower : 소문자 변환 함수

### 3\) initcap : 첫글자는 대문자, 나머지는 소문자로 변환하는 함수

### 4\) concat : 연결연산자와 동일한 기능. 2개만 연결.

```text
--concat
SELECT last_name||first_name, 
             lower(concat(last_name,first_name))
FROM employees;
```

### 5\) length: 문자의 길이를 반환하는 함수

```text
SELECT last_name, length(last_name) 
FROM employees ;

SELECT length('홍길동')
FROM dual;
```

### 6\) lengthb: 문자의 바이트 값으로 반환하는 함수

```text
SELECT lengthb('빅데이터'), lengthb('bigdata')
FROM dual ;
```

### 7\) instr: 문자의 위치를 반환하는 함수

```text
SELECT instr(last_name,'a')
FROM dual;

SELECT instr('aabccb','b'), instr('aabccb','b'1,2)
--1: 시작위치
--2: 두번째 나오는 b 찾아
```

### 8\) substr: 문자를 추출하는 함수

```text
SELECT last_name, substr(last_name,1,2), substr(last_name,4),
substr(last_name,-1,1) 
FROM employees;
/** 
1: 첫번째 글자부터 
2: 두 글자 뽑아내겠다 
4: 네번째 글자부터 다 뽑아내겠다 
-1: 제일 뒤 위치에서, 1: 한 글자만 뽑아내겠다  
*/
```

### 9\) substrb: 문자를 바이트 수만큼 추출하는 함수

```text
SELECT substrb('가나다라마', 1, 6)
FROM dual ; 
--1: 첫번째 위치부터 
--6: 6바이트만큼 추출한다
```

### 10\) trim: 접두, 접미 문자를 자르는 함수. 연속되는 글자 모두 제거됨

```text
SELECT trim('a' from 'aabbca') 
FROM dual; 
--결과: bbc

SELECT last_name, trim('K' from last_name)
FROM employees
WHERE last_name loke 'K%';
```

### 11\) ltrim: 접두 문자를 자른느 함수

### 12\) rtrim: 접미 문자를 자르는 함수

```text
SELECT trim('a' from 'aabbca'),
             ltrim('aabbca','a'), rtrim('aabbca','a')
FROM dual;
--결과: bbc, bbca, aabbc
```

```text
--공백 제거하기
SELECT trim(' ' from '  b bc  '),ltrim('  b bc',' '),
rtrim('b bc    ',' ')
FROM dual;
--결과: b bc, b bc, b bc  
--중간에 있는 공백 문자는 제거할 수 없다
```

### 13\) repalce: 문자를 다른 문자로 치환하는 함수. 공백 제거할 때도 사용

```text
SELECT replace('100-001','-','%'), replace('100001','0','*'),
replace('   abc d ', ' ', '')
FROM dual; 
--결과: 100%001,1****1,abcd
```

### 14\) lpad: 문자의 자리를 고정시킨 후 문자값을 오른쪽을 기준으로 채우고 왼쪽 빈 공백을 다른 값으로 채우는 함수

### 15\) rpad: 문자의 자리를 고정시킨 후 문자값을 왼쪽을 기준으로 채우고 오른쪽의 빈 공백을 다른 값으로 채우는 함수

```text
SELECT salary, lpad(salary, 10, '*'), rpad(salary, 10, '*')
FROM employees;
--결과: 24000,*****24000,24000*****
```

