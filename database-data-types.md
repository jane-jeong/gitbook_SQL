# BASE - DATA TYPE

## 1\) 데이터 타입

{% hint style="info" %}
* number\(p, s\): 가변 길이 숫자 타입 \(p: 전체자리수, s:소수점자리수\)
* varchar2\(4000\): 가변 길이 문자 타입, 최대 크기: 4000
* char\(2000\): 고정 길이 문자 타입. 최대 크기: 2000
  * 고정 길이는 무조건 크기 2000을 차지한다. 공간 낭비를 초래할 수 있다. 그래서 보편적으로 varchar2 타입 사용한다.
* clob\(4gbyte\): 가변 길이 문자 타입 \(4gbyte 필수\)
  * 가변 길이지만 어느 정도 데이터를 확보해두어야 하기 때문에 공간 낭비가 있다. 쓰지 않는 것이 좋다.
* blob\(4gbyte\): 가변 길이 이진 데이터 타입.
  * 이미지 파일 등을 저장해두어야 할 때 사용하는 타입이다. 하지만 관리하기가 불편하다.
* bfile\(4gybte\): 외부 파일에 저장된 이진 데이터 타입이다.
  * blob의 단점을 보완한 것이다. 파일을 직접 저장하지 않는다. 외부 파일에 접근할 수 있도록 '포인터' 정보만 보유하고 있는 방식이다. 이미지\(학생부 사진\) 등 파일을 DB에 저장해두어야 한다면 보편적으로 bfile 타입을 사용한다.
* date: 날짜 데이터 타입
{% endhint %}

## 2\) 문자 타입과 저장 공간

DB에 저장할 수 있는 문자 타입에는 몇 가지가 있는데,

CHAR\(고정길이, max2000\), 가변길이\(VARCHAR2, max4000\), CLOB\(가변길이, 4G\), long\(가변길이, 2G\) 타입들은 DATABASE CHARACTERSET에 영향을 받는다.

```text
SELECT * 
FROM nls_database_parapmeters;
```

가변길이는 공간이 남는 경우 다른 것을 저장할 수 있다. 고정길이는 문자를 다 쓰지 않아도 2000바이트만큼 고정으로 공간을 차지한다. 영문은 1byte, 그 외 공간은 2~4byte 차지한다.

* DATABASE CHARACTERSET
  * 유니코드\(UNICODE\): AL32UTF8, 한글은 3byte. 전세계 출판되는 문자는 모두 표현할 수 있다.
  * VARCHAR2\(10\), 고정길이 CHAR\(10\), CLOB\(4G\), LONG\(2G\)은 DATABASE CHARACTERSET에 종속된다.
  * NLS\_NCHAR\_CHARACTERSET: AL16UTF16 → DATABASE CHARACTERSET
  * KO16MSWIN949: 한글, 한자, 영어, 일어, 2byte \(많은 한국 기업들이 사용한다.\)
* NATAIONAL CHARACTERSET
  * nvarchar2, nchar, nclob 문자 타입은 NATIONAL CHARACTERSET의 영향을 받는다.
  * 유니코드\(UNICODE\): AL16UTF16, 전세계 출판되는 문자는 모두 표현할 수 있다.
  * nvarchar2, nchar, nclob는 AL16UTF16에 종속된다.
  * NLS\_CHARACTERSET AL32UTF8 → NATIONAL CHARACTERSET
* 만약에 글자가 깨져 보인다면 문자 타입을 확인해야 한다. 유니코드는 전 세계 출판되는 문자를 다 저장할 수 있다. 영문은 어떤 타입이든지 1byte 차지한다.

