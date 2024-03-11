- **Employees-With-Missing-Information**

  - [https://leetcode.com/problems/employees-with-missing-information/](https://leetcode.com/problems/employees-with-missing-information/)
  - **문제 :** Employees 테이블과 Salaries 테이블에서 서로 누락된 직원 정보를 찾습니다. 각각의 테이블에 서로 없는 employee_id를 출력하는데 오름차순으로 출력합니다.

  ```jsx
  [ 문제 조건 ]
  CREATE TABLE Employees (
      employee_id INT,
      name VARCHAR(255)
  );

  CREATE TABLE Salaries (
      employee_id INT,
      salary INT
  );

  INSERT INTO Employees (employee_id, name) VALUES
  (2, 'Crew'),
  (4, 'Haven'),
  (5, 'Kristian');

  INSERT INTO Salaries (employee_id, salary) VALUES
  (1, 72617),
  (5, 26557),
  (4, 63539);
  ```

  ```jsx
  [ 정답(1) ]
  SELECT EMPLOYEE_ID
  FROM EMPLOYEES
  WHERE EMPLOYEE_ID NOT IN (SELECT EMPLOYEE_ID FROM SALARIES)
  UNION
  SELECT EMPLOYEE_ID
  FROM SALARIES
  WHERE EMPLOYEE_ID NOT IN (SELECT EMPLOYEE_ID FROM EMPLOYEES)
  ORDER BY EMPLOYEE_ID

  [ 정답(2) ]
  SELECT EMPLOYEE_ID
  FROM(
  		SELECT EMP.EMPLOYEE_ID
  		FROM EMPLOYEES EMP
  		WHERE NOT EXISTS ( SELECT 1 FROM SALARIES SAL WHERE SAL.EMPLOYEE_ID = EMP.EMPLOYEE_ID)
  		UNION
  		SELECT SAL.EMPLOYEE_ID
  		FROM SALARIES SAL
  		WHERE NOT EXISTS ( SELECT 1 FROM EMPLOYEES EMP WHERE EMP.EMPLOYEE_ID = SAL.EMPLOYEE_ID)
  ) EMP
  ORDER BY EMPLOYEE_ID

  ```

  - **해설 :** 서로의 테이블에 없는 EMPLOYEE_ID를 찾는 것이기 때문에 NOT IN 키워드와 NOT EXISTS 키워드를 사용해 문제를 풀어보았습니다.
