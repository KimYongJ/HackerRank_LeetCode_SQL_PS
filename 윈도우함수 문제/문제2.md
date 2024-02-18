- 윈도우함수 문제

  - [https://leetcode.com/problems/department-top-three-salaries/](https://leetcode.com/problems/department-top-three-salaries/)

    ```jsx
    [ 문제 조건 ]
    -- Department 테이블 생성
    CREATE TABLE Department (
        id INT PRIMARY KEY,
        name VARCHAR(255)
    );

    -- Employee 테이블 생성
    CREATE TABLE Employee (
        id INT PRIMARY KEY,
        name VARCHAR(255),
        salary INT,
        departmentId INT,
        FOREIGN KEY (departmentId) REFERENCES Department(id)
    );

    -- Department 테이블에 데이터 삽입
    INSERT INTO Department (id, name) VALUES
    (1, 'IT'),
    (2, 'Sales');

    -- Employee 테이블에 데이터 삽입
    INSERT INTO Employee (id, name, salary, departmentId) VALUES
    (1, 'Joe', 85000, 1),
    (2, 'Henry', 80000, 2),
    (3, 'Sam', 60000, 2),
    (4, 'Max', 90000, 1),
    (5, 'Janet', 69000, 1),
    (6, 'Randy', 85000, 1),
    (7, 'Will', 70000, 1);
    ```

    - **문제 :** 부서별로 가장 높은 급여를 3개 뽑습니다. 그리고 그 급여에 해당하는 모든 인원들을 출력합니다.

    ```jsx
    [ 정답 ]
    select dept.name as Department
    ,      emp.name as Employee
    ,      emp.Salary
    from employee emp
    inner join (
    				select dense_rank() over(partition by emp.departmentId order by emp.salary desc) rnk
    				,      emp.id
    				from employee emp
    		   )remp on remp.rnk between 1 and 3
    		        and remp.id = emp.id
    inner join department dept on dept.id = emp.departmentid
    ```

    - **해설 :** dense_rank 함수를 이용해 부서별로 급여가 가장 높은 순으로 순위를 표현하고, 그장 높은 3개의 급여를 갖는 행만 emp테이블에 다시 inner join을 합니다. 이로 써 해당 급여를 받는 모든 인원을 추출할 수 있습니다.
