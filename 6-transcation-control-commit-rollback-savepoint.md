# TCL - COMMIT

## COMMIT

* COMMIT은 INSERT, DELETE, UPDATE 문으로 변경한 데이터를 데이터베이스에 반영하는 명령
* 변경 전 이전 데이터는 잃어버린다.
* 커밋이 완료되면 다른 모든 데이터베이스 사용자는 변경된 데이터를 볼 수 있다.
* 데이터베이셔 변경으로 인한 LOCK이 해제된다.
* 커밋이 완료되면 다른 모든 데이터베이스 사용자는 변경된 데이터를 조작할 수 있다.
* 커밋을 실행하면 하나의 트랜잭션 과정을 종료한다.

```sql
commit ; 
```

{% hint style="info" %}
**AUTO COMMIT\(자동 커밋\)되는 경**

* SQL\*PLUS 프로그램을 정상적으로 종료하는 경우 자동 커밋
* DDL, DCL 사용하는 경우 자동 커밋
* "set autocommit on;"을 SQL\*PLUS에서 실행하면 자동 커밋
{% endhint %}

## ROLLBACK

* ROLLBACK을 실행하면 데이터에 대한 변경 사용을 모두 취소하고 트랜잭션을 종료한다.
* INSERT, UPDATE, DELETE문의 작업을 모두 취소한다. 단, 이전에 커밋한 곳까지만 복구한다.
* ROLLBACK을 실행하면 LOCK이 해제되고 다른 사용자도 데이터베이스 행을 조작할 수 있다.

```sql
rollback; 
```

## SAVEPOINT

* SAVEPOINT는 트랜잭션을 작게 분할하여 관리하는 것으로 SAVEPOINT를 사용하면 지정된 위치까지만 트랜잭션을 ROLLBACK할 수 있다.
* SAVEPOINT의 지정은 SAVEPOINT &lt;SAVEPOINT명&gt;을 실행한다.
* 지정된 SAVEPOINT까지만 데이터 변경을 취소하고 싶은 경우는 "ROLLBACK TO &lt;SAVEPOINT명&gt;"을 실행한다.
* 만약, ROLLBACK을 실행하면 SAVEPOINT와 관계없이 변경된 모든 데이터를 취소한다.

```sql
savepoint t1; 
# Savepoint created. 

update emp set enmae='관우' where empno=1003; 
# 1 row updated.  

savepoint t2;          # 여기 이 지점으로 돌아옴
# Savepoint created. 

update emp set enmae='장비' where empno=1004; 
# 1 row updated.  

select ename from emp where empno in <1003, 1004>; 
# ENAME 
--------
관우 
장비 

rollback to t2;       # t2 지점으로 돌아간다 
# Rollback Completed. 

select ename from emp where empno in <1003, 1004>; 
# ENAME 
--------
관우 
test5
```

