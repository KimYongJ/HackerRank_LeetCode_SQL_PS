- 윈도우함수 문제

  - [https://leetcode.com/problems/consecutive-numbers/](https://leetcode.com/problems/consecutive-numbers/)

    ```jsx
    [ 문제 조건 ]
    create table logs(
    id integer auto_increment primary key,
    num integer
    );

    insert into logs(num) values
    (1),
    (1),
    (1),
    (2),
    (1),
    (2),
    (2)
    ```

    - **문제 :** 해당 테이블에서 num 컬럼의 같은 숫자가 3번 연속으로 출력되는 경우 해당 숫자를 출력하는 문제입니다. ConsecutiveNums이라는 한개의 컬럼을 가진 테이블로 출력합니다. [ 1 1 1 2 1 2 2 ] 가 순서대로 출력 된다면 1이 연속으로 3번 나오고, 2는 연속으로 3번 나온느것이 없기 때문에 정답으로 1만 출력하면됩니다.

    ```jsx
    [ 정답(1) ]
    select distinct num as ConsecutiveNums
      from (
    		  select num
    		  ,      lag(num) over(order by id) as prev_n
    		  ,      lead(num) over(order by id) as next_n
    		  from logs
              order by id
    		)rdata
     where num = prev_n and num = next_n
    ```

    - **해설 :** lag과 lead 함수는 윈도우 함수로써 현재 행의 기준으로 이전이나 이후 행의 데이터를 가져올 때 쓰이며 over절과 함께 사용됩니다.
      - **LAG :** 현재 행에서 지정된 수만큼 이전 행의 데이터를 반환 이전행이 존재하지 않을 경우 기본값(default value)을 반환할 수 있습니다. offset과, default_value는 생략 가능합니다.
        - **형태 :** LAG(column_name, offset, default_value) OVER (ORDER BY column_name)
      - **LEAD :** LAG과 똑같고 다만 현재 행에서 지정된 수만큼 이후 데이터를 반환, 이후 행이 존재하지 않으면 기본값을 반환할 수 있습니다.
        - **형태 :** LEAD(column_name, offset, default_value) OVER (ORDER BY column_name)

    ```jsx
    [ 정답(2) ]
    SELECT distinct a.num as ConsecutiveNums
    from logs a
    inner join logs b on a.id+1 = b.id
    inner join logs c on a.id+2 = c.id
    where a.num = b.num and a.num = c.num
    ```

    - **해설 :** id가 1씩 자동 증가하기 때문에 id기준으로 +1, +2 까지 inner join하여 num이 같으면 출력하도록 만들었습니다.
