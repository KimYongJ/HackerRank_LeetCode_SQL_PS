- SUB Query 문제

  - [https://www.hackerrank.com/challenges/challenges/problem?isFullScreen=true](https://www.hackerrank.com/challenges/challenges/problem?isFullScreen=true)

    ```jsx
    [ 문제 조건 ]
    CREATE TABLE Hackers (
        hacker_id INT PRIMARY KEY,
        name VARCHAR(255) NOT NULL
    );
    CREATE TABLE Challenges (
        challenge_id INT PRIMARY KEY,
        hacker_id INT,
        FOREIGN KEY (hacker_id) REFERENCES Hackers(hacker_id)
    );

    INSERT INTO Hackers (hacker_id, name) VALUES
    (5077, 'Rose'),
    (21283, 'Angela'),
    (62743, 'Frank'),
    (88255, 'Patrick'),
    (96196, 'Lisa');
    INSERT INTO Challenges (challenge_id, hacker_id) VALUES
    (61654, 5077),
    (58302, 21283),
    (40587, 88255),
    (29477, 5077),
    (1220, 21283),
    (69514, 21283),
    (46561, 62743),
    (58077, 62743),
    (18483, 88255),
    (76766, 21283),
    (52382, 5077),
    (74467, 21283),
    (33625, 96196),
    (26053, 88255),
    (42665, 62743),
    (12859, 62743),
    (70094, 21283),
    (34599, 88255),
    (54680, 88255),
    (61881, 5077);
    ```

    - **문제 :** 각 hacker_id당 문제 갯수에 따른 정보를 내림차순하는데, 이 때 같은 문제 갯수를 만든 학생들은 제거합니다. 단 그냥 제거하는 것이 아니라 이들이 만든 문제 갯수가 가장큰 문제 갯수보다 작은 경우만 삭제 합니다.

    ```jsx
    [ 정답(1) ]
    with rdata as (
                     select c.hacker_id,count(1) as cnt
                     from challenges c
                     group by c.hacker_id
                  )
    select  r.hacker_id
    ,       h.name
    ,       r.cnt
    from rdata r
    inner join Hackers h
          on h.hacker_id = r.hacker_id
    where r.hacker_id not in (
                                select r.hacker_id
                                from rdata r
                                inner join (
                                             select count(1) as same_num, cnt.cnt
                                             from(
                                                    select *
                                                    from rdata
                                                  )cnt group by cnt
                                           ) sd on sd.cnt = r.cnt
    							              where sd.same_num >= 2
    							              and r.cnt != (
                                                select max(r.cnt) max_num
                                                from rdata r
                                              )
                              )
    order by r.cnt desc, r.hacker_id

    [ 정답(2) ]
    with rdata as(
                   select h.hacker_id
                   ,      h.name
                   ,      count(1) as cnt
                   ,      count(1) over(partition by count(1)) as same_num # partition by는 group by 와 같지만 group by 처럼 행을 직접 줄이면서 그룹화하지 않음
                   ,      max(count(1)) over() as max_num # over 는 윈도우 함수로 특정 집계 함수를 현재 행의 집합에 적용할 때 사용한다. over절을 사용함으로써 특정 그룹화 없이 전체 행에 대해 MAX집계를 적용한다.
                   from Hackers h
                   inner join challenges c on c.hacker_id = h.hacker_id
                   group by h.hacker_id, h.name
                 )
    select r.hacker_id
    ,      r.name
    ,      r.cnt
    from rdata r
    where r.cnt = r.max_num
    or    same_num = 1
    order by r.cnt desc , r.hacker_id
    ```

    - **해설 :** 정답(1)은 문제풀이 필요한 값들을 직접 명시한것이고 정답(2)는 윈도우 함수를 사용해 길이를 줄인 것입니다. partition by를 사용해 같은 cnt값인 것들의 숫자를 헤아리고, max함수와 over를 같이 사용해 모든 행 중 가증 큰 값을 찾습니다.
