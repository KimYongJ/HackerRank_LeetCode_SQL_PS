- SUB Query 문제

  - [https://www.hackerrank.com/challenges/earnings-of-employees/problem](https://www.hackerrank.com/challenges/earnings-of-employees/problem)

    ```jsx
    [ 문제 조건 ]
    create table employee(
    id integer,
    name varchar(30),
    months integer,
    salary integer
    );

    select * from employee;

    insert into employee values(1,'a',15,1968);
    insert into employee values(2,'b',1,3443);
    insert into employee values(3,'c',17,1608);
    insert into employee values(4,'d',7,1345);
    insert into employee values(5,'e',11,2330);
    insert into employee values(6,'f',16,4372);
    insert into employee values(7,'g',8,1771);
    insert into employee values(8,'h',6,2017);
    insert into employee values(9,'i',5,3396);
    insert into employee values(10,'j',9,3573);
    ```

    - **문제 :** 일한 개월 수 \* salary 중 가장 큰 값을 고르고 그 값을 갖는 사람이 몇명인지 찾는 문제 입니다.

    ```jsx
    [ 정답 (id는 실제 문제에서 employee_id로 적어야 함) ]
    select 	max(earnings) as earnings
    ,		count(1) as cnt
    from (
    		select id, months * salary as earnings
    		from employee
    )emp
    where earnings = (select max(months*salary) as earnings from employee)
    ```

    - **해설 :** 먼저 from절안에 id와 일한 개월 \* 급여(earnings)를 구한 뒤 where 조건에서 가장 큰 earnings를 대입해 행들을 구해옵니다. 그 후 select 조건에서 max와 count를 사용해 group을 지어 가장 큰 earnings 값과 가장 큰 earnings 값을 갖고있는 사람의 수를 구합니다.
