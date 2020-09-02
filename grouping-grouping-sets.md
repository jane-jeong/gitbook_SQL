# GROUP BY GROUPING SETS

## GROUP BY GROUPING SETS 

* GROUP BY GROUPING SETS — 내가 필요한 그룹 조합만 골라서 출력

  ```text
  --GROUPING SETS의 문형 

  SELECT a, b, c, SUM(salary) 
  FROM tablename 
  GROUP BY grouping sets ((a,b), (b,c), ()); 

  /** 출력 결과 
  sum(sal) = {a,b}
  sum(sal) = {b,c}
  sum(sal) = {}
  */

  SELECT depmartment_id, job_id, manager_id, SUM(salary) 
  FROM employees 
  GROUP BY GROUPING SETS ((department_id, job_id), (job_id, manager_id), (manager_id));

  /**결과 해석: department_id, job_id 별로 SUM(salary) 정리한 목록 
  + job_id, manager_id 별로 SUM(salary) 정리한 목록 
  + manager_id 별로 SUM(salary) 정리한 목록을 한꺼번에 출력 */

  --근데 좀 보기 불편한데???
  ```

