---
description: COLUMN ALIASES
---

# SELECT - 열별칭

## SELECT 문에서 열 별칭 붙여주기 

산술연산이나 함수 표현식을 사용하면 그 식이 컬럼명에 그대로 출력되는데, SELECT 문을 효율적으로 작성하고 컬럼을 보기 좋게 출력하기 위해 '열 별칭\(Alias\)을 붙여준다. 

## 열 별칭\(Alias\) 생성 규칙 

* 컬럼명이나 컬럼 표현식에 한 칸 띄고 열별칭을 적어주거나 한 칸 띄고 as \(열별칭\)을 적어주면 된다 

```sql
SELECT employees as 사번, salary*12+nvl(commission_pct,0) ann_sal
FROM employees;
```

* 큰 따옴표 안에 넣으면 열별칭을 소문자로 표현하거나, 공백과 특수문자를 포함할 수 있다. + 열별칭을 쓸 때 숫자가 앞에 나오면 오류난다. " " 사용하는 습관 들이자.

{% tabs %}
{% tab title="열 별칭 예제 - 소문자" %}
```sql
SELECT employee_id as 사번, 
				salary*12+nvl(commission_pct,0) "ann sal" 
FROM employees;
```
{% endtab %}

{% tab title="열 별칭 예제 - 숫자와 공백" %}
```sql
SELECT salary*24+nvl(commission_pct, 0) "2년 연봉"
FROM employees; 
```
{% endtab %}
{% endtabs %}

* 열 별칭에는 ' \#, $, \_ ' 특수문자만 가능하다.

```sql
SELECT employee_id as 사번, salary*12+nvl(commission_pct,0) ann#sal
FROM employees;
```

* 열 별칭에 \#, $, \_ 이외의 특수문자를 넣으면 오류가 발생한다.

```sql
SELECT employee_id as 사번, salary*12+nvl(commission_pct,0) ann^sal
FROM employees;

```



