# SET - 집합연산자

## 집합연산자란?

조회\(SELECT\) 쿼리의 결과를 대상으로 연산을 수행하는 연산자.

* SELECT 절의 컬럼 수와 데이터 타입을 일치시켜야 한다.
* 집합 후 열의 이름은 첫 번째 컬럼 이름 또는 별칭으로 출력된다.
* UNION, UNION ALL, INTERSECT, MINUS 연산자가 있다. 

## 1. UNION \(합집합\)

UNION\(합집합\) 연산자는 말그대로 두 테이블을 합쳐준다.

* UNION은 오름차순으로 정렬하며, 중복을 제거한다. 

{% tabs %}
{% tab title="UNION 1" %}
```sql
/** 첫번째 집합 세번째 컬럼 salary는 숫자 타입.
두번째 집합 세번째 컬럼에 상수 써줘도 된다. */
SELECT employee_id, job_id, salary 
FROM employees 
UNION 
SELECT employee_id, job_id, 0
FROM job_history ;
```
{% endtab %}

{% tab title="UNION 2" %}
```sql
/** 의미 없지만 아래처럼 할 수도 있다.
포인트는 to_number. 즉, 숫자 타입이어야 한다는 것 */

SELECT employee_id, job_id, salary 
FROM employees 
UNION 
SELECT employee_id, job_id, to_number(null)
FROM job_history ;
```
{% endtab %}

{% tab title="UNION 3" %}
```sql
--만약에 합쳐주는 열 타입이 문자라면 
--숫자타입으로 형 변환해줘야 한다
SELECT employee_id, job_id, salary 
FROM employees 
UNION 
SELECT employee_id, job_id, to_number('0')
FROM job_history ;
```
{% endtab %}

{% tab title="오류 케이스" %}
```sql
--오류 : 열의 갯수와 데이터 타입을 일치시켜야 한다

SELECT employee_id "사원번호", salary "연봉"
FROM employees

UNION

SELECT employee_id
FROM job_history ;
```
{% endtab %}
{% endtabs %}

## 2. UNION ALL \(중복 제거하지 않는 합집합\)

UNION ALL은 중복을 제거하지 않고, 그 자체로는 정렬을 수행하지 않는 합집합 연산자다. UNION ALL에서 ORDER BY를 사용할 경우 구문 맨 마지막에 사용하고, 정렬할 컬럼은 첫 번째 테이블의 컬럼 이름으로 지정한다. 컬럼 이름은 번거롭고 오류나기 쉽기 때문에, ORDER BY할 때 위치표기법을 사용하는 것을 권장한다.

```sql
--두번째 집합 번째 컬럼에서 null로 가상 열을 만든  것.
SELECT employee_id "사원번호", salary "연봉"
FROM employees

UNION ALL

SELECT employee_id, null 
FROM job_history 
ORDER BY 1 ;
--위치 표기법 사용해서 정렬 수행.
```

## 3. INTERSECT \(교집합\)

두 테이블에서 공통적인 데이터, 교집합만 추출한다. 

{% tabs %}
{% tab title="INTERSECT CASE 1" %}
```sql
# 팀을 옮겼다가 다시 원래 팀으로 옮긴 사람 조회하기 
SELECT employee_id, job_id 
FROM employees

INTERSECT 

SELECT employee_id, job_id 
FROM job_history ;
```
{% endtab %}

{% tab title="INTERSECT CASE 2" %}
```sql
--팀을 한 번 이상 옮긴 사람 조회하기 
SELECT employee_id
FROM employees 
INTERSECT
SELECT employee_id 
FROM job_history;
```
{% endtab %}
{% endtabs %}

INTERSECT는 EXISTS로 동일하게 배선할 수 있다.

{% tabs %}
{% tab title="EXISTS CASE 1" %}
```sql
# 팀을 옮겼다가 다시 원래 팀으로 옮긴 사람 조회하
SELECT *
FROM employees o
WHERE exists ( SELECT 'x' 
                             FROM job_history 
                             WHERE employee_id = o.employee_id
                             and job_id = o.job_id ) ;
```
{% endtab %}

{% tab title="EXISTS CASE 2" %}
```sql
--팀을 한 번 이상 옮긴 사람 조회하기 
SELECT *
FROM employees o 
WHERE exists ( SELECT 'X' 
                             FROM job_history 
                             WHERE employee_id = o.employee_id) ;
```
{% endtab %}
{% endtabs %}

## 4. MINUS

* 한 집합에서 다른 집합\(교집합\) 빼기 : A - \(A INTERSECT B\)  

{% tabs %}
{% tab title="MINUS CASE" %}
```sql
# 한 번도 JOB 바꾸지 않은 사람 조회하기 
SELECT employee_id
FROM employees 
MINUS
SELECT employee_id
FROM job_history ;
```
{% endtab %}
{% endtabs %}

* 위의 MINUS를 사용한 쿼리는 실행계획에서 SORT 함수가 발생해서 효율성은 좋지 않다. INTERSECT와 마찬가지로 MINUS는 NOT EXISTS로 동일하게 배선할 수  있다. 

{% tabs %}
{% tab title="NOT EXISTS" %}
```sql
# 한 번도 JOB 바꾸지 않은 사람 조회하기
SELECT * 
FROM employees o
WHERE not exists ( SELECT 'x' 
                                     FROM job_history 
                                     WHERE employee_id = o.employee_id ) ;
```
{% endtab %}
{% endtabs %}

## 5. 집합연산자와 JOIN의 차이점 \(이상한데\)

아래 예제로 집합연산자와 JOIN의 차이점을 이해해보자.

아래 두 쿼리를 행한 결과값은 같다.

{% tabs %}
{% tab title="CASE" %}
```sql
SELECT e.employee_id, e.last_name, d.department_id, d.department_name 
FROM employees e, departments d 
WHERE e.department_id = d.department_id(+)
UNION
SELECT e.employee_id, e.last_name, d.department_id, d.department_name
FROM employees e, departments d
WHERE e.department_id(+) = d.department_id ;
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="CASE" %}
```sql
SELECT e.employee_id, e.last_name, d.department_id, d.department_name 
FROM employees e FULL OUTER JOIN departments d 
ON e.department_id = d.department_id;
```
{% endtab %}
{% endtabs %}

그런데, 아래 두 쿼리를 실행한 결과값은 다르다.

{% tabs %}
{% tab title="CASE" %}
```sql
SELECT e.last_name, d.department_id, d.department_name 
FROM employees e, departments d 
WHERE e.department_id = d.department_id(+)
UNION
SELECT e.employee_id, e.last_name, d.department_id, d.department_name
FROM employees e, departments d
WHERE e.department_id(+) = d.department_id ;
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="CASE" %}
```sql
SELECT e.last_name, d.department_id, d.department_name 
FROM employees e FULL OUTER JOIN departments d 
ON e.department_id = d.department_id;
```
{% endtab %}
{% endtabs %}

--위 쿼리에서의 employee\_id와는 달리 last\_name은 유일한 값이 아니다.

--last\_name, department\_id, department\_name은 중복이 있을 수 있다.

--즉, NONUNIQUE 컬럼이라는 것.

--그럼, last\_name과 department\_id, department\_name이 모두 같은 사람이 있다

--같은 부서에 last\_name이 같은 사람이 있을 수 있는 것

--그럼 집합연산자 UNION을 쓰면 동명이인이 사라져버린다

--last\_name, department\_id, department\_name 기준으로 가상 테이블을 만들어 합치는 것이기 때문

