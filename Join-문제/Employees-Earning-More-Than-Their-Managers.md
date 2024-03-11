- **Employees-Earning-More-Than-Their-Managers**

  - [https://leetcode.com/problems/employees-earning-more-than-their-managers/](https://leetcode.com/problems/employees-earning-more-than-their-managers/)
  - **문제 :** EMPLOYEE 테이블에서 자기의 매니저보다 많은 급여를 받는 직원의 NAME을 출력하는데 컬럼명은 EMPLOYEE로 출력합니다.

  ```jsx
  [ 문제 조건 ]
  CREATE TABLE Employee (
      id INT PRIMARY KEY,
      name VARCHAR(100),
      salary INT,
      managerId INT
  );

  INSERT INTO Employee (id, name, salary, managerId) VALUES
  (1, 'Joe', 70000, 3),
  (2, 'Henry', 80000, 4),
  (3, 'Sam', 60000, NULL),
  (4, 'Max', 90000, NULL);
  ```

  ```jsx
  [ 정답 ]
  SELECT E1.NAME AS EMPLOYEE
  FROM EMPLOYEE E1
  INNER JOIN EMPLOYEE E2
  		ON E1.MANAGERID = E2.ID
  WHERE E1.SALARY > E2.SALARY
  ```

  - **해설 :** INNER JOIN을 하여 자기 자신과 매니저를 한줄로 만든 후 매니저보다 급여가 많은 행을 WHERE 조건에 걸러줍니다.
