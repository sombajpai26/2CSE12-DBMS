# <center>Experiment No.8
### Perform the following Query 
### 1. Display all employees with their dept name. 
~~~sql
SELECT E.EMPNO, E.ENAME, D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D
ON E.DEPTNO = D.DEPTNO;
~~~
~~~sql
SELECT E.ENAME, D.DNAME
FROM EMPLOYEE E, DEPARTMENT D
WHERE E.DEPTNO = D.DEPTNO;
~~~
### 2. Display those employees whose manager names is jones, and also display their manager name. 
~~~sql
SELECT 
    E.ENAME AS EMPLOYEE,
    M.ENAME AS MANAGER
FROM EMPLOYEE E
JOIN EMPLOYEE M
ON E.MGR = M.EMPNO
WHERE M.ENAME = 'JONES';
~~~
~~~sql
SELECT A.ENAME AS EMPLOYEE_NAME, B.ENAME AS MANAGER_NAME
FROM EMPLOYEE A, EMPLOYEE B
WHERE A.MGR = B.EMPNO
AND B.ENAME = 'JONES';
~~~
### 3. Display employee name, his job, his dept name, his manager name, his grade and make out of an under department wise.
~~~sql
CREATE TABLE SALGRADE (
    GRADE CHAR(1),
    LOSAL INT,
    HISAL INT
);

INSERT INTO SALGRADE VALUES
('A', 700, 1200),
('B', 1201, 1400),
('C', 1401, 2000),
('D', 2001, 3000),
('E', 3001, 9999);

SELECT e.ENAME, e.JOB, d.DNAME, m.ENAME AS MANAGER, s.GRADE
FROM EMPLOYEE e
JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO
LEFT JOIN EMPLOYEE m ON e.MGR = m.EMPNO
JOIN SALGRADE s ON e.SAL BETWEEN s.LOSAL AND s.HISAL
ORDER BY d.DNAME;
~~~
### 4. List out all the employees name, job, and salary grade and department name for everyone in the company except ‘clerk’. Sort on salary display the highest salary.
~~~sql
SELECT e.ENAME, e.JOB, e.SAL, s.GRADE, d.DNAME
FROM EMPLOYEE e
JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO
JOIN SALGRADE s ON e.SAL BETWEEN s.LOSAL AND s.HISAL
WHERE e.JOB <> 'CLERK'
ORDER BY e.SAL DESC;
~~~
### 5. Display employee name, his job and his manager. Display also employees who are without manager. 
~~~sql
SELECT e.ENAME, e.JOB, m.ENAME AS MANAGER
FROM EMPLOYEE e
LEFT JOIN EMPLOYEE m ON e.MGR = m.EMPNO;
~~~
### 6. List the employee name, job, annual salary, deptno, dept name and grade who earn 36000 a year or who are not clerks. 
~~~sql
SELECT e.ENAME, e.JOB, (e.SAL * 12) AS ANNUAL_SAL,
       e.DEPTNO, d.DNAME, s.GRADE
FROM EMPLOYEE e
JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO
JOIN SALGRADE s ON e.SAL BETWEEN s.LOSAL AND s.HISAL
WHERE (e.SAL * 12) >= 36000
   OR e.JOB <> 'CLERK';
~~~
### 7. List ename, job, annual sal, deptno, dname and grade who earn 30000 per year and who are not clerks. 
~~~sql
SELECT e.ENAME, e.JOB, (e.SAL * 12) AS ANNUAL_SAL,
       e.DEPTNO, d.DNAME, s.GRADE
FROM EMPLOYEE e
JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO
JOIN SALGRADE s ON e.SAL BETWEEN s.LOSAL AND s.HISAL
WHERE (e.SAL * 12) = 30000
  AND e.JOB <> 'CLERK';
~~~
### 8. List out all employees by name and number along with their manager’s name and number also display ‘no manager’ who has no manager. 
~~~sql
SELECT e.EMPNO, e.ENAME,
       COALESCE(CAST(m.EMPNO AS CHAR), 'No Manager') AS MGR_NO,
       COALESCE(m.ENAME, 'No Manager') AS MGR_NAME
FROM EMPLOYEE e
LEFT JOIN EMPLOYEE m ON e.MGR = m.EMPNO;
~~~
~~~sql
SELECT 
    e.EMPNO, 
    e.ENAME,
    IFNULL(CAST(m.EMPNO AS CHAR), 'No Manager') AS MGR_NO,
    IFNULL(m.ENAME, 'No Manager') AS MGR_NAME
FROM EMPLOYEE e
LEFT JOIN EMPLOYEE m 
ON e.MGR = m.EMPNO;
~~~
### 9. Select dept name, dept no and sum of sal 
~~~sql
SELECT d.DEPTNO, d.DNAME, SUM(e.SAL) AS TOTAL_SAL
FROM EMPLOYEE e
JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO
GROUP BY d.DEPTNO, d.DNAME;
~~~
### 10. Display employee number, name and location of the department in which he is working
~~~sql
ALTER TABLE DEPARTMENT
ADD LOCATION VARCHAR(20);
~~~
~~~sql
UPDATE DEPARTMENT SET LOCATION = 'MUMBAI' WHERE DEPTNO = 10;
UPDATE DEPARTMENT SET LOCATION = 'CHENNAI' WHERE DEPTNO = 20;
UPDATE DEPARTMENT SET LOCATION = 'HYDERABAD' WHERE DEPTNO = 30;
UPDATE DEPARTMENT SET LOCATION = 'DELHI' WHERE DEPTNO = 40;
~~~
~~~sql
SELECT e.EMPNO, e.ENAME, d.LOC
FROM EMPLOYEE e
JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO;
~~~
### 11. Display employee name and department name for each employee. 
~~~sql
SELECT e.ENAME, d.DNAME
FROM EMPLOYEE e
JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO;
~~~


