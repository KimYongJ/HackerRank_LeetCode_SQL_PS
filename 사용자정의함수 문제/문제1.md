- 사용자 정의 함수 문제
  - [https://leetcode.com/problems/nth-highest-salary/](https://leetcode.com/problems/nth-highest-salary/)
  - 이 문제에서 주어지는 N을 쿼리상에서 직접 수정(N-1등..)은 불가합니다. SET을 통해 변경해야 합니다.
  ```jsx
  [ 문제 조건 ]
  -- EMPLOYEE 테이블 생성
  CREATE TABLE EMPLOYEE (
      id INT PRIMARY KEY,
      salary DECIMAL(10, 2)
  );

  -- EMPLOYEE 테이블에 레코드 삽입
  INSERT INTO EMPLOYEE (id, salary) VALUES
  (1, 100.00),
  (2, 200.00),
  (3, 300.00),
  (4, 150.00),
  (5, 250.00),
  (6, 350.00),
  (7, 450.00),
  (8, 550.00),
  (9, 650.00),
  (10, 750.00),
  (11, 850.00),
  (12, 950.00);
  ```
  - **문제 :** N 이 주어졌을 때 N번 째로 salary가 높은 사람을 구하고, N번째가 없을 때는 NULL을 출력하는 function을 작성하는 문제입니다.
  ```jsx
  [ 정답(1) ]
  CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
  BEGIN
    RETURN (select MAX(salary) salary
  					from(
  							select distinct salary
  							,		dense_rank() over(order by salary desc) drnk
  							from employee
  						)emp
  					where emp.drnk = N

           );
  END;
  ```
  - **해설 :** dense_rank 함수로 랭킹을 구한 후 N값에 해당하는 salary를 가져옵니다. 이 때 만약 값이 없으면 NULL을 출력해야 하기 때문에 MAX로 감싸줍니다. MAX로 감쌀 경우 값이 없으면 NULL이 출력됩니다.
  ```jsx
  [ 정답(2) ]
  CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
  BEGIN
    SET N = N - 1;
    RETURN (
        SELECT DISTINCT salary
        FROM Employee
        ORDER BY salary DESC
        LIMIT 1 OFFSET N
    );
  END;
  ```
  - **해설 :** LIMIT과 OFFSET 키워드로 간단히 구하는 방법 입니다. LIMIT은 쿼리 결과에서 반환되는 최대 행(row)수를 제한합니다. 전체 10줄을 가져오고 싶다면 LIMIT 10과 같이 사용할 수 있습니다. OFFSET은 쿼리 결과에서 몇 개의 행을 건너뛰고 데이터를 선택할지 지정합니다. 0을 적을 경우 하나도 건너뛰지 않고, 1을 적으면 1줄 건너뛰고 2번째 줄 부터 출력합니다. 그렇기 대문에 SET N = N-1을 해주는 것입니다. 만약 입력되는 N이 1이라면, 가장 첫번 째를 출력해야 하기 때문에 LIMIT은 1을 적어주고, OFFSET은 1-1로 즉, OFFESET 0이 입력되어야 합니다.
  ```jsx
  [ 정답(3) ]
  CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
  BEGIN
    SET N = N - 1;
    RETURN (
        SELECT DISTINCT salary
        FROM Employee
        ORDER BY salary DESC
        LIMIT N,1
    );
  END;
  ```
  - **해설 :** LIMIT는 두개의 인자를 줄 수도 있습니다. LIMIT 1, 2를 적게 된다면, 상위 1개의 다음 2개를 가져옵니다. 첫번 째 인자는 출력하려는 행의 순위에 +1을 한게 출력되고, 두번 째 인자는 몇줄을 출력할 것인지 입력하게 됩니다. LIMIT 2, 3을 적게된다면 상위 3번째 줄부터 3줄을 가져오라는 명령이 됩니다. 위 문제에서는 SET N = N - 1; 구문을 적고 마지막에 LIMIT N,1을 적었는데 이는 주어지는 N의 -1번 째 줄의 다음 줄(즉 N번째 줄)을 출력하고, 출력하는 행은 1개다 라는 의미입니다.
