# 숫자 함수

## 단일행 함수 - 숫자 함수 

### 1\) round: 지정된 소수점 자릿수로 값을 반올림하는 함수

```sql
SELECT round(45.926,2), round(45.926,1), round(45.926,0),
			 round(45.926,-1), round(45.926,-2)
FROM dual;
--결과: 45.93, 45.9, 46, 50,	0
```

### 2\) trunc: 지정된 소수점 자릿수를 기준으로 버리는 함수

```sql
SELECT trunc(45.926,2),trunc(45.926,1),trunc(45.926,0),
			 trunc(45.926,-1),trunc(45.926,-2)
FROM dual;
--결과: 45.92,	45.9, 	45, 	40, 	0
```

### 3\) mod: 어떤 값을 나눈 나머지를 반환하는 함수

```sql
SELECT mod(12,5)
FROM dual;
--결과: 2
```

### 4\) ceil: 숫자값을 가장 큰 정수로 반환하는 함수 \(정수로 올림\)

```sql
SELECT ceil(10.1),ceil(10.0),ceil(10.0001),ceil(10.0009)
FROM dual;
--결과: 11, 10, 11, 11
```

### 5\) floor: ceil 함수와 반대되는 함수. 무조건 절삭한다.

```sql
SELECT floor(10.1),floor(10.0),floor(10.0001),floor(10.0009)
FROM dual;
--결과: 10, 10, 10, 10
```

### 6\) power: 거듭제곱 함수

```sql
SELECT 2*2*2*2*2, power(2,5)
FROM dual;
--결과: 32
```

