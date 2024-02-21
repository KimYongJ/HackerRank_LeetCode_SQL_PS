- the-blunder
  - [https://www.hackerrank.com/challenges/the-blunder/problem?isFullScreen=true](https://www.hackerrank.com/challenges/the-blunder/problem?isFullScreen=true)
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE EMPLOYEES (
      ID INT PRIMARY KEY,
      Name VARCHAR(100),
      Salary INT
  );
  INSERT INTO EMPLOYEES (ID, Name, Salary) VALUES
  (1, 'John Doe', 4000),
  (2, 'Jane Doe', 3600),
  (3, 'Alice', 2900),
  (4, 'Bob', 5200);
  ```
  - **문제 :** EMPLOYEES 테이블의 Salary의 평균을 구하고, Salary에서 0이 제거된 숫자들의 평균도구해서 정상적인 평균과 0이 제거된 평균의 차이를 출력합니다. 이 때 소숫점은 올림해야합니다.
  ```jsx
  [ 정답 ]
  SELECT CEIL(AVG(SALARY) - AVG(REPLACE(SALARY, '0','')))
  FROM EMPLOYEES
  ```
