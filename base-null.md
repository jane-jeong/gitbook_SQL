# BASE - NULL

## NULL 값이란 무엇일까? 

#### Null 값이란 무엇일까?

* NULL은 사용할 수 없거나, 할당되지 않았거나, 알 수 없거나, 적용할 수 없는 값이다. '값이 없는 것'이다. NULL은 0이나 공백이 아니다. 스페이스 바를 치는 것\(공백\)도 NULL이 아니다. NULL은 아예 어떠한 것도 들어오지 않은 것이다.

#### Null 값이 있을 때 연산은 어떻게 할까?

* 존재하지 않는 것에 대해서는 연산이 불가능하다.
* NULL 값이 포함된 것은 그 합은 무조건 NULL이다.
* NULL이 있을 경우 계산 수행될 수 있도록 하려면 프로그래밍을 해줘야 한다. NULL 관련 함수 참고.

#### NULL 정리

* NULL은 모르는 값을 의미한다.
* NULL은 값의 부재를 의미한다. 
* NULL과 모든 비교는 NULL을 반환한다. 
* NULL과 숫자 혹은 날짜를 더하면 NULL이 된다. 
* NULL 값은 비교 연산자로 비교할 수 없다. 만약 비교 연산자로 NULL을 비교하면 FALSE가 나온다.

## NULL 값 조회하기 

* NULL을 조회할 때는 IS NULL을 사용하고 NULL 값이 아닌 것을 조회할 경우는 IS NOT NULL을 사용한다. 

{% tabs %}
{% tab title="IS NULL" %}
```sql
SELECT * FROM EMP 
WHERE MGR IS NULL ; 
```
{% endtab %}

{% tab title="IS NOT NULL" %}
```sql
SELECT * FROM EMP 
WHERE MGR IS NOT NULL ; 
```
{% endtab %}
{% endtabs %}

#### 

