---
description: Arithmetic Operator
---

# SELECT - 산술연산자

## 산술연산자 쓰기 

### 1\) 사칙연산이 모두 가능한 건 NUMBER 타입만 가능하다

```text
SELECT salary*12, salary/12, salary+100, salary-100
FROM employees ; 
```

### 2\) DATE 타입은 더하기와 빼기만 가능하다 

```text
SELECT hire_date+100, hire_date-100 
FROM employees ; 
```

### 3\) 문자\(CHAR, VARCHAR2\) 타입은 사칙연산 불가

### 4\) 연산자 우선순위 

1. 곱하기와 나누기 \( \* , / \) 
2. 더하기와 빼기 \( +, - \)
3. 같은 순위가 같이 있을 때는 왼쪽에서 오른쪽 
4. 우선 순위를 모르는 사람을 위해 괄호로 표현해주자 
5. 연산자 우선순위를 바꾸고 싶을 때는 괄호로 표현해준다 

