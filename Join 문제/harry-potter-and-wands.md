- harry-potter-and-wands

  - [https://www.hackerrank.com/challenges/harry-potter-and-wands/problem?isFullScreen=true](https://www.hackerrank.com/challenges/harry-potter-and-wands/problem?isFullScreen=true)
  - **문제**
    - "Wands" 테이블과 "Wands_Property" 테이블에서 데이터를 조합하여, 론이 관심을 가질 수 있는 각 마법봉의 id, age, coins_needed, power를 선택합니다.
    - 선택된 마법봉은 내림차순으로 정력(power)이 정렬되어야 합니다. 만약 두 개 이상의 마법봉이 같은 정력을 가지고 있다면, 나이(age)의 내림차순으로 정렬해야 합니다.
    - 또한, 선택해야 하는 마법봉은 암흑 마법에 사용되지 않는(non-evil), 즉 "is_evil" 값이 0인 마법봉이어야 하며, 높은 정력과 오래된 나이를 가진 마법봉 중에서 가장 적은 금갤리언(coins_needed)이 필요한 마법봉을 찾아야 합니다.

  ```jsx
  [ 문제 조건 ]
  -- Wands 테이블 생성
  CREATE TABLE Wands (
      id INT PRIMARY KEY,
      code INT,
      coins_needed INT,
      power INT
  );
  -- Wands_Property 테이블 생성
  CREATE TABLE Wands_Property (
      code INT PRIMARY KEY,
      age INT,
      is_evil BOOLEAN
  );
  -- Wands 테이블에 데이터 추가
  INSERT INTO Wands (id, code, coins_needed, power) VALUES
  (1, 4, 3688, 8),
  (2, 3, 9365, 3),
  (3, 3, 7187, 10),
  (4, 3, 734, 8),
  (5, 1, 6020, 2),
  (6, 2, 6773, 7),
  (7, 3, 9873, 9),
  (8, 3, 7721, 7),
  (9, 1, 1647, 10),
  (10, 4, 504, 5),
  (11, 2, 7587, 5),
  (12, 5, 9897, 10),
  (13, 3, 4651, 8),
  (14, 2, 5408, 1),
  (15, 2, 6018, 7),
  (16, 4, 7710, 5),
  (17, 2, 8798, 7),
  (18, 2, 3312, 3),
  (19, 4, 7651, 6),
  (20, 5, 5689, 3);

  -- Wands_Property 테이블에 데이터 추가
  INSERT INTO Wands_Property (code, age, is_evil) VALUES
  (1, 45, 0),
  (2, 40, 0),
  (3, 4, 1),
  (4, 20, 0),
  (5, 17, 0);
  ```

  ```jsx
  [ 정답 ]
  SELECT   Wands.id
  ,        Wands_Property.age
  ,        Wands.coins_needed
  ,        Wands.power
  FROM Wands
  inner join Wands_Property on Wands_Property.code = Wands.code
  where (Wands.power ,Wands_Property.age , Wands.coins_needed )
      in(
              SELECT    MAX(Wands.power) power
              ,        max(Wands_Property.age)age
              ,        min(Wands.coins_needed) coins
              FROM Wands
              inner join Wands_Property on Wands_Property.code = Wands.code
              where Wands_Property.is_evil = 0
              group by    Wands_Property.code
              ,            Wands_Property.age
              ,            Wands.power
          )
  order by Wands.power desc, Wands_Property.age desc;

  ```

  - **해설 :** code와 age, power를 기준으로 그룹을 지어 가장 높은 power와 age, coin을 select합니다. 그리고 메인 쿼리에 in 절을 활용해 같은 데이터만 select하도록 했습니다.
