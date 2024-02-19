- UPDATE 문제

  - [https://leetcode.com/problems/swap-salary/](https://leetcode.com/problems/swap-salary/)

    ```jsx
    [ 문제 조건 ]
    create table salary(
    id integer,
    name varchar(30),
    sex varchar(30),
    salaray integer
    );
    #drop table salary;
    insert into salary values(1,'A', 'm',2500);
    insert into salary values(2,'B', 'f',2500);
    insert into salary values(3,'C', 'm',2500);
    insert into salary values(4,'D', 'f',2500);
    select * from salary;
    ```

    - **문제 :** 하나의 update쿼리로 sex컬럼의 m을 f로, f를 m으로 변경하는 문제 입니다.

    ```jsx
    [ 정답 ]
    update salary
    set sex = case when sex = 'm' then 'f' else 'm' end;
    ```

    - **해설 :** update 구문을 하는데 sex에 대입하는 값을 case when으로 분기를 해줍니다. (sex가 m일 때는 f로, f일 때는 m으로) 해당 업데이트문은 실행시마다 m과 f가 바뀌게 됩니다.
