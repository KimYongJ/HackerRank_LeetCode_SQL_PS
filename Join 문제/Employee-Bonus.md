- **Employee-Bonus**

  - [https://leetcode.com/problems/employee-bonus/](https://leetcode.com/problems/employee-bonus/)
  - **문제 :** Employee 테이블과 Bonus 테이블은 empId로 엮을 수 있고, Bonus가 1000보다 작은 사람의 이름과, 보너스를 출력합니다. 보너스가 NULL인 컬럼도 출력합니다.

  ```jsx
  [ 문제 조건 ]
  CREATE TABLE Employee (
      empId INT PRIMARY KEY,
      name VARCHAR(100),
      supervisor INT,
      salary INT
  );

  INSERT INTO Employee (empId, name, supervisor, salary) VALUES
  (1, 'Joe', 3, 1000),
  (2, 'Henry', 2, 800),
  (3, 'Sam', NULL, 600),
  (4, 'Max', 3, 900);

  CREATE TABLE Bonus (
      empId INT PRIMARY KEY,
      bonus INT
  );

  INSERT INTO Bonus (empId, bonus) VALUES
  (1, 500),
  (2, 800),
  (3, 1200),
  (4, 700);
  ```

  ```jsx
  [ 정답 ]
  SELECT NAME
  ,       BN.BONUS
  FROM EMPLOYEE EMP
  LEFT OUTER JOIN BONUS BN
          ON BN.EMPID = EMP.EMPID
  WHERE BN.BONUS IS NULL OR BN.BONUS < 1000
  ```

  - **해설 :** 두 테이블을 조인하여 보너스가 NULL이거나 1000 미만인 컬럼을 조회합니다.
