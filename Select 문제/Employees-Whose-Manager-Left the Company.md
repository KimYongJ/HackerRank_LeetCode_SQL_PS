- **Employees-Whose-Manager-Left the Company**

  - [https://leetcode.com/problems/employees-whose-manager-left-the-company/](https://leetcode.com/problems/employees-whose-manager-left-the-company/)
  - **문제 :** 직원의 manager_id가 회사를 떠난(테이블에 없는) 관리자를 참조하는 직원의 employee_id를 찾는 문제이며 employee_id를 기준으로 오름차순 정렬합니다. 또한 급여가 3만 미만이여야 합니다.

  ```jsx
  [ 문제 조건 ]
  CREATE TABLE Employees (
      employee_id INT,
      name VARCHAR(255),
      manager_id INT,
      salary INT
  );

  INSERT INTO Employees (employee_id, name, manager_id, salary) VALUES
  (1, 'Ahtila', NULL, 60000),
  (3, 'Antonella', 9, 30001),
  (12, 'Hillel', 9, 63000),
  (13, 'Kalel', NULL, 67804),
  (11, 'Kalel', 11, 21241),
  (9, 'Mikaela', NULL, 98957),
  (11, 'Josiah', 6, 24845);
  ```

  ```jsx
  [ 정답 ]
  SELECT EMP1.EMPLOYEE_ID
  FROM EMPLOYEES EMP1
  WHERE EMP1.SALARY < 30000
  AND EMP1.MANAGER_ID IS NOT NULL
  AND NOT EXISTS (
  					SELECT 1
  					FROM EMPLOYEES EMP2
  					WHERE EMP2.EMPLOYEE_ID	= EMP1.MANAGER_ID
  				)
  ORDER BY EMP1.EMPLOYEE_ID

  ```

  - **해설 :** 급여가 3만 미만이면서, 매니저 ID를 갖고 있는 컬럼 중에 메인 쿼리의 매니저 아이디와 서브 쿼리의 직원 아이디가 일치하지 않는 조건을 조회합니다.
