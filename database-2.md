# BASE - 사용자 권한 확인하기

## 업무 시작하기 전에 먼저 나의 사용자 권한을 확인하자

### 권한\(Privilege\)이란?

* 권한이란 특정한 SQL문을 수행할 수 있는 권리다.
* 시스템권한\(sys\_privs\)이란 데이터베이스에 영향을 줄 수 있는 권한이다.
* 객체권한\(tab\_privs\)이란 객체를 사용할 수 있는 권한이다. \(ex. 테이블 생성, 데이터 조회 등\)

### 권한을 부여하는 주체 / 방법 / 부여 가능 범위

1. DBA\(DB Administrator\)가 **직접 권한을 부여**하기 \(시스템 권한, 객체 권한 모두 가능\)
2. DBA가 미리 설정한 권한 프리셋 상자인 **role**을 부여하기
3. 객체를 소유한 사용자가 **자신의 객체에 대한 권한을 다른 사용자에게 부여하**기

## \[ CASE 1 \] 사용자가 DBA로부터 받은 시스템 권한 확인하기

```sql
SELECT * FROM user_sys_privs; 
--결과: 딕셔너리 테이블 출력

/**
HR    CREATE VIEW    NO                  --view 생성할 수 있음
HR    UNLIMITED TABLESPACE    NO
HR    CREATE DATABASE LINK    NO      
HR    CREATE SEQUENCE    NO
HR    CREATE SESSION    NO
HR    ALTER SESSION    NO
HR    CREATE SYNONYM    NO */
--유저가 부여받은 권한의 목록임 (NO는 ADMIN OPTION인데 권한 여부가 NO인 것 아니다)
```

* CREATE SESSION: 오라클 DB에 접속할 수 있는 권한 \(유저 계정 로그온 권한\)이다. CREATE SESSION을 끊어버리면 아예 접속이 불가능하다.
* ALTER SESSION: 유저의 session 영역에 한해 session의 무언가를 바꿀 수 있는 권한이다. 예를 들어, ALTER SESSION set nls\_language = AMERICAN; ALTER SESSION set nls\_territory = AMERICA; 이런 것

## \[ CASE 2 \] 사용자가 DBA로부터 받은 role 목록과 그 role을 통해 부여 받은 시스템 권한 확인하기

#### 1\) 사용자가 DBA로부터 받은 role 목록 확인하기

```text
SELECT * FROM session_roles;
```

#### 2\) role을 통해 부여 받은 시스템 권한 확인하기

```text
SELECT * FROM role_sys_privs;
```

#### 3\) DBA로부터 직접 받은 시스템 권한과 role을 통해 부여 받은 시스템권한 모두 확인하기

```text
SELECT * FROM session_privs;
```

## \[ CASE 3 \] 객체 소유자로부터 직접 받은 객체 권한과 내가 다른 사용자에게 부여한 객체 권한을 확인하는 방

```text
--사용자가 DBA나 객체 소유자로부터 받은 객체권환 확인하기 
--내가 다른 사용자에게 부여한 객체권환 확인하기 
SELECT * FROM user_tab_privs;

/**출력 결과 
GRANTEE OWNER TABLE_NAME GRANTOR PRIVILEGE GRATABLE HIERARCHY
------- ----- ---------- ------- --------- -------- ---------
HR        SYS   DBMS_STATS SYS     EXECUTE   NO        NO
*/
```

```text
--role을 통해 받은 객체권환 확인하는 방법 
SELECT * FROM role_tab_privs;
```

## \[ CASE 4 \] 다른 사용자에게 객체 권한 부여해주기

* 객체 권한을 부여해주는 것은 DBA와 객체 소유자 모두 가능하다 

