- SUB Query 문제

  - [https://leetcode.com/problems/department-highest-salary/](https://leetcode.com/problems/department-highest-salary/)

    ```jsx
    [ 문제 조건 ]
    CREATE TABLE Department (
        id INT PRIMARY KEY,
        name VARCHAR(255) NOT NULL
    );
    INSERT INTO Department (id, name) VALUES
    (1, 'IT'),
    (2, 'Sales');
    CREATE TABLE Employee (
        id INT PRIMARY KEY,
        name VARCHAR(255),
        salary INT,
        departmentId INT,
        FOREIGN KEY (departmentId) REFERENCES Department(id)
    );

    INSERT INTO Employee (id, name, salary, departmentId) VALUES
    (1, 'Joe', 70000, 1),
    (2, 'Jim', 90000, 1),
    (3, 'Henry', 80000, 2),
    (4, 'Sam', 60000, 2),
    (5, 'Max', 90000, 1);
    ```

    - **문제 :** 각 부서 당 가장 높은 salary를 받는 사람에 대해 순서 없이 출력하는 문제 입니다.

    ```jsx
    [ 정답(1) ]
    select dept.name as Department, emp.name as Employee, emp.salary AS Salary
    from employee emp
    inner join department dept
    	on dept.id = emp.departmentId
    where emp.salary in (
    						select max(emp2.salary)
    						from employee emp2
    						where emp2.departmentId = emp.departmentId
    						group by emp2.departmentId
    					)
    ```

    - **해설 :** emp테이블을 departmentId 기준으로 group by 해서, max salary를 추출합니다. 이 때 **[ where emp2.departmentId = emp.departmentId ]** 조건을 필수로 넣어 주어야 정답으로 인정되는데 이 코드를 넣어야 현재 메인 쿼리에서 선택된 직원(emp)과 같은 부서에 속한 직원들(emp2)만을 대상으로 최대 급여를 계산하도록 합니다.

    ```jsx
    [ 정답(2) ]
    select dept.name as Department, emp.name as Employee, emp.salary AS Salary
    from employee emp
    inner join department dept
    	on dept.id = emp.departmentId
    where ( emp.departmentId ,emp.salary )in (
    						select emp2.departmentId, max(emp2.salary)
    						from employee emp2
    						group by emp2.departmentId
    					)
    ```

    - **해설 :** 서브 쿼리에 **[ where emp2.departmentId = emp.departmentId ]** 구문을 빼고 where 절에 emp.departmentId 조건을 추가해서 할 수도 있습니다.

    ```jsx
    [ 정답(3) ]
    select dept.name as Department, emp.name as Employee, emp.salary AS Salary
    from employee emp
    inner join (
                    select emp2.departmentId, max(emp2.salary) as salary
                    from employee emp2
                    group by emp2.departmentId
    			)emp2 on emp2.departmentId = emp.departmentId
                      AND emp2.salary   =   emp.salary
    inner join department dept
    	on dept.id = emp.departmentId
    ```

    - **해설 :** inner join으로도 문제를 해결할 수 있습니다.

    ```jsx
    [ 정답(4) ]
    select dept.name as Department
    ,      emp.name as Employee
    ,      emp.salary as Salary
    from employee emp
    inner join (
    				select emp.id
    				,      dense_rank() over(partition by emp.departmentid order by emp.salary desc) rnk
    				from employee emp
               )emp_rnk on emp_rnk.id = emp.id
    inner join department dept on dept.id = emp.departmentid
    where emp_rnk.rnk = 1
    ```

    - **해설 :** dense_rank함수를 사용하고, over 함수에 partition by를 써서 부서 id별로 그룹을 지은 후 emp테이블의 salary를 내림차순 정렬하면 부서별로 가장 급여가 높은사람들의 순위가 생성됩니다. dense_rank는 중복 순위를 적어 주기 때문에 문제 조건과 부합해 사용할 수 있습니다. dense_rank를 rank로 바꿔도 동일한 결과를 얻을 수 있습니다.
