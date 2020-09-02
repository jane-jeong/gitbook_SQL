---
description: Logical Operators
---

# FILTERING - 논리연산자

## SQL의 논리연산자

[https://www.sqltutorial.org/sql-logical-operators/](https://www.sqltutorial.org/sql-logical-operators/)

| **Operator** | **Meaning** |
| :--- | :--- |
| [ALL](https://www.sqltutorial.org/sql-all/) | Return true if all comparisons are true |
| [AND](https://www.sqltutorial.org/sql-and/) | Return true if both expressions are true \(모두 만족해야 참\) |
| [ANY](https://www.sqltutorial.org/sql-any/) | Return true if any one of the comparisons is true. |
| [BETWEEN](https://www.sqltutorial.org/sql-between/)  A AND B | Return true if the operand is within a range \(A와 B 사이의 값을 조회\) |
| NOT BETWEEN A AND B | A와 B 사이에 해당되지 않는 데이터를 조회한다 |
| [EXISTS](https://www.sqltutorial.org/sql-exists/) | Return true if a subquery contains any rows |
| [IN](https://www.sqltutorial.org/sql-in/) \(리스트\) | Return true if the operand is equal to one of the value in a list \(OR 의미. 리스트 값 중에 하나만 일치해도 조회한다.\) |
| NOT IN | 리스트와 불일치하는 것을 조회한다. \(AND 개념\) |
| [LIKE](https://www.sqltutorial.org/sql-like/) | Return true if the operand matches a pattern \(특정 문자열과 일치하는 데이터를 조회한다.\) |
| NOT LIKE | 특정 문자열과 일치하지 않는 데이터를 조회한다. |
| [NOT](https://www.sqltutorial.org/sql-not/) | Reverse the result of any other Boolean operator. \(참이면 거짓으로 바꾸고, 거짓이면 참으로 바꿈\) |
| [OR](https://www.sqltutorial.org/sql-or/) | Return true if either expression is true \(조건 중 하나만 만족해도 참\) |
| [SOME](https://www.sqltutorial.org/sql-any/) | Return true if some of the expressions are true |
| IS NULL | NULL 값을 조회한다 |
| IS NOT NULL | NULL 값이 아닌 것을 조회한다 |

