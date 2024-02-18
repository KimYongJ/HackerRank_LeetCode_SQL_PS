- Between 문제
  - [https://www.hackerrank.com/challenges/the-report/problem?isFullScreen=true](https://www.hackerrank.com/challenges/the-report/problem?isFullScreen=true)
    ```jsx
    [ 문제 조건 ]
    CREATE TABLE Students (
        ID INT PRIMARY KEY,
        Name VARCHAR(255),
        Marks INT
    );
    CREATE TABLE Grades (
        Grade INT PRIMARY KEY,
        Min_Mark INT,
        Max_Mark INT
    );
    INSERT INTO Students (ID, Name, Marks) VALUES
    (1, 'Julia', 88),
    (2, 'Samantha', 68),
    (3, 'Maria', 99),
    (4, 'Scarlet', 78),
    (5, 'Ashley', 63),
    (6, 'Jane', 81);
    INSERT INTO Grades (Grade, Min_Mark, Max_Mark) VALUES
    (1, 0, 9),
    (2, 10, 19),
    (3, 20, 29),
    (4, 30, 39),
    (5, 40, 49),
    (6, 50, 59),
    (7, 60, 69),
    (8, 70, 79),
    (9, 80, 89),
    (10, 90, 100);
    ```
    - 문제 : 10~8등급까지는 이름, 등급, 점수 순으로 출력하고 7등급 이하부터는 이름을 null로 표시합니다, 등급에 따라 내림차순으로 출력하고, 같은 등급이 여러명일 경우 학생 이름 기준 알파벳 순으로 오름차순 정렬, 이름이 null인데 같은 등급인 사람들은 점수에 따라 오름차순 정렬합니다.
    ```jsx
    [ 정답 ]
    select case when g.grade < 8 then null else s.name end name
    ,      g.grade
    ,      s.marks
    from Students s
    inner join grades g
    			on s.marks between g.min_mark and g.max_mark
    order by g.grade desc, s.name asc, s.marks asc
    ```
