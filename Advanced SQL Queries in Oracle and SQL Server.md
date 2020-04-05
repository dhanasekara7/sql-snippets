```sql
/**
https://www.youtube.com/watch?v=pmpzsws4xwA

Analytic-Function(col1, col2, ..)   min(salary)
OVER (
[Query-Partition-Clause]
[Order-By-Clause]
[Windowing-Clause]
)
**/


--1) get dept wise avg salary and employees detail
SELECT department_id, avg(salary) from employees group by department_id;

/*same in analytic with employee detail.
actually to get the employees detail in the above sql we need to self join.
LEAD Function = access next row value
*/

SELECT avg(salary) OVER (partition by department_id) as avg_dept_sal, a.*
FROM employees a
ORDER BY employee_id

-- 2) find details of most recent joinees
SELECT * FROM (
SELECT LEAD(HIRE_DATE) OVER ( PARTITION BY department_id ORDER BY HIRE_DATE) as recent_joinee_by_dept,
a.* from employees a) WHERE recent_joinee_by_dept IS NULL

-- 3) FIND cumulative sum of employee salary
SELECT SUM(SALARY) OVER (PARTITION BY department_id ORDER BY EMPLOYEE_ID) AS CUMU_SUM, A.*
FROM employees a order by employee_id, department_id

-- if we dont do PARTITION BY department_id , LAST row will have the SUM of all salary
SELECT SUM(SALARY) OVER (ORDER BY EMPLOYEE_ID) AS CUMU_SUM, A.*
FROM employees a order by employee_id, department_id

/*
Windowing function
Find two employees salary who joined before me in the same dept
*/

SELECT AVG(SALARY) OVER (PARTITION BY department_id ORDER BY HIRE_DATE ROWS 2 PROCEEDING)
AS CUMU_SUM_PREV_2, A.*
FROM employees a order by employee_id, department_id

```