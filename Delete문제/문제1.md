- DELETE 문제
  - [https://leetcode.com/problems/delete-duplicate-emails/](https://leetcode.com/problems/delete-duplicate-emails/)
    ```jsx
    [ 문제 조건 ]
    create table person(
    id integer,
    email varchar(30)
    );
    #drop table person;
    select * from person;
    insert into person values(1, 'aaa@email.com');
    insert into person values(2, 'aaa@email.com');
    insert into person values(3, 'bbb@email.com');
    insert into person values(4, 'ccc@email.com');
    insert into person values(5, 'ccc@email.com');
    ```
    - **문제 :** 중복된 이메일을 모두 삭제하는데, 삭제시 id값이 가장 작은 이메일만 남도록 해야 합니다.
    ```jsx
    [ 정답(1) ]
    delete from person
    where id not in (
    					select p.id
    					from (
    							select MIN(id) as id
    							from person
    							group by email
    						)p
    				)
    ```
    - **해설 :** where 조건에서 email을 기준으로 그룹을 묶어 id값이 가장 작은 것만 모은 row들을 생성한 후, not in 연산자로 그룹지은 id가 아닌 것만 삭제하도록 했습니다. 이 때 group by 구문을 from절안에 넣지 않으면 [**SQL Error [1093] [HY000]: You can't specify target table 'person' for update in FROM clause]** 오류가 발생합니다. 그 이유는 MySQL에서는 UPDATE나 DELETE를 할 때 해당 쿼리의 FROM 절에서는 같은 테이블을 직접 참조할 수 없도록 제한하고 있기 때문입니다. 이는 MySQL이 해당 쿼리를 실행하는 동안 테이블의 데이터에 대한 일관성을 유지하기 위한 조치 입니다. 그렇기에 from안에 select문을 작성해야 합니다.
    ```jsx
    [ 정답(2) ]
    delete p1
    from person p1
    inner join person p2 on p1.email = p2.email
    where p1.id > p2.id
    ```
    - **해설 :** delete에 inner join을하여 해결한 방법으로 self 조인으로 행을 강제로 늘린 후 p1의 id가 p2의 id보다 큰것을 골라내면 중복된 행을 뽑아낼 수 있고, 그 후 delete 명령어 옆에 테이블 p1을 적어주면 중복된 행이 삭제됨과 동시에 가장작은 id만 남게 됩니다.
