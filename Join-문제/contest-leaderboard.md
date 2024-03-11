- contest-leaderboard
  - [https://www.hackerrank.com/challenges/contest-leaderboard/problem?isFullScreen=true](https://www.hackerrank.com/challenges/contest-leaderboard/problem?isFullScreen=true)
  - **문제 :** Submissions 테이블에서 해커 별로 challenge_id 컬럼 값마다 최고의 score를 모두 합해서 출력하는 문제입니다. 이 때, score의 합이 0인 해커는 제외 합니다. 출력시 score의 총합을 기준으로 내림차순하고, 해커의 아이디 별로 오름차순 정렬합니다.
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE Hackers (
      hacker_id INT PRIMARY KEY,
      name VARCHAR(255)
  );
  CREATE TABLE Submissions (
      submission_id INT PRIMARY KEY,
      hacker_id INT,
      challenge_id INT,
      score INT,
      FOREIGN KEY (hacker_id) REFERENCES Hackers(hacker_id)
  );
  INSERT INTO Hackers (hacker_id, name) VALUES
  (4071, 'Rose'),
  (4806, 'Angela'),
  (26071, 'Frank'),
  (49438, 'Patrick'),
  (74842, 'Lisa'),
  (80305, 'Kimberly'),
  (84072, 'Bonnie'),
  (87868, 'Michael'),
  (92118, 'Todd'),
  (95895, 'Joe');
  INSERT INTO Submissions (submission_id, hacker_id, challenge_id, score) VALUES
  (67194, 74842, 63132, 76),
  (64479, 74842, 19797, 98),
  (40742, 26071, 49593, 20),
  (17513, 4806, 49593, 32),
  (69846, 80305, 19797, 19),
  (41002, 26071, 89343, 36),
  (52826, 49438, 49593, 9),
  (31093, 26071, 19797, 2),
  (81614, 84072, 49593, 100),
  (44829, 26071, 89343, 17),
  (75147, 80305, 49593, 48),
  (14115, 4806, 49593, 76),
  (6943, 4071, 19797, 95),
  (12855, 4806, 25917, 13),
  (73343, 80305, 49593, 42),
  (84264, 84072, 63132, 0),
  (9951, 4071, 49593, 43),
  (45104, 49438, 25917, 34),
  (53795, 74842, 19797, 5),
  (26363, 26071, 19797, 29),
  (10063, 4071, 49593, 96);
  ```
  ```jsx
  [ 정답 ]
  select   sub.hacker_id
  ,        Hackers.name
  ,        sum(max_score) sum_score
  from (
          select   hacker_id
          ,        max(Submissions.score) max_score
          ,        challenge_id
          from Submissions
          group by Submissions.hacker_id , challenge_id
  )sub
  inner join Hackers on Hackers.hacker_id = sub.hacker_id
  group by sub.hacker_id , Hackers.name
  having sum(max_score) != 0
  order by sum_score desc , sub.hacker_id
  ```
  - **해설 :** 본 쿼리는 각 해커(hacker_id)가 참여한 챌린지(challenge_id) 마다 얻은 점수(score)를 집계하여 해커별로 최고 점수를 구하고, 그 점수들의 총합을 계산합니다. 이를 위해 서브쿼리를 사용하여 각 해커가 각 챌린지에서 얻은 최대 점수를 찾아내고, 외부 쿼리에서 이 점수들을 합산하여 총 점수를 구합니다. 그 후, 총 점수가 0이 아닌 해커들에 대해서만 결과를 필터링하기 위해 **`HAVING`** 절에 조건을 명시합니다.
  - 최종적으로, 해커의 이름과 총점을 출력하기 위해 **`Hackers`** 테이블과 조인을 수행하고, 총점이 높은 순으로 정렬하여 출력합니다. 동일한 총점을 가진 해커가 여러 명 있을 경우, 해커 아이디(hacker_id)의 오름차순으로 정렬하여 결과를 반환합니다.
