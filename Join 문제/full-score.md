- full-score

  - [https://www.hackerrank.com/challenges/full-score/problem?isFullScreen=true](https://www.hackerrank.com/challenges/full-score/problem?isFullScreen=true)
  - **문제 :** 두 개 이상의 챌린지에서 만점을 획득한 해커들의 hacker_id와 이름을 출력하는 쿼리를 작성하는 문제 입니다. 출력은 해커가 만점을 획득한 챌린지의 총 수에 따라 내림차순으로 정렬합니다. 만약 한 명 이상의 해커가 동일한 수의 챌린지에서 만점을 받았다면, 그들을 hacker_id에 따라 오름차순으로 정렬하세요.

  ```jsx
  [ 문제 조건 ]
  -- Hackers Table
  CREATE TABLE Hackers (
      hacker_id INT PRIMARY KEY,
      name VARCHAR(255)
  );

  INSERT INTO Hackers (hacker_id, name) VALUES
  (5580, 'Rose'),
  (8439, 'Angela'),
  (27205, 'Frank'),
  (52423, 'Patrick'),
  (52348, 'Lisa'),
  (57645, 'Kimberly'),
  (77726, 'Bonnie'),
  (83082, 'Michael'),
  (86870, 'Todd'),
  (90411, 'Joe');

  -- Difficulty Table
  CREATE TABLE Difficulty (
      difficulty_level INT PRIMARY KEY,
      score INT
  );

  INSERT INTO Difficulty (difficulty_level, score) VALUES
  (1, 20),
  (2, 30),
  (3, 40),
  (4, 60),
  (5, 80),
  (6, 100),
  (7, 120);

  -- Challenges Table
  CREATE TABLE Challenges (
      challenge_id INT PRIMARY KEY,
      hacker_id INT,
      difficulty_level INT,
      FOREIGN KEY (hacker_id) REFERENCES Hackers(hacker_id)
  );

  INSERT INTO Challenges (challenge_id, hacker_id, difficulty_level) VALUES
  (4810, 77726, 4),
  (21089, 27205, 1),
  (36566, 5580, 7),
  (66730, 52423, 6),
  (71055, 52348, 2);

  -- Submissions Table
  CREATE TABLE Submissions (
      submission_id INT PRIMARY KEY,
      hacker_id INT,
      challenge_id INT,
      score INT,
      FOREIGN KEY (hacker_id) REFERENCES Hackers(hacker_id),
      FOREIGN KEY (challenge_id) REFERENCES Challenges(challenge_id)
  );
  INSERT INTO Submissions (submission_id, hacker_id, challenge_id, score) VALUES
  (68628, 77726, 36566, 30),
  (65300, 77726, 21089, 10),
  (40326, 52423, 36566, 77),
  (8941, 27205, 4810, 10),
  (83554, 77726, 66730, 30),
  (43353, 52423, 66730, 0),
  (55385, 52348, 71055, 20),
  (39784, 27205, 71055, 23),
  (94613, 86870, 71055, 30),
  (7394, 52348, 36566, 0),
  (93058, 86870, 36566, 30),
  (7344, 8439, 66730, 92),
  (2721, 8439, 4810, 36),
  (523, 5580, 71055, 4),
  (49105, 52348, 66730, 0),
  (55877, 57645, 66730, 80),
  (38355, 27205, 66730, 35),
  (3924, 8439, 36566, 80),
  (97397, 90411, 66730, 100),
  (84162, 83082, 4810, 40),
  (97431, 90411, 71055, 30);
  ```

  ```jsx
  [ 정답 ]
  SELECT	HK.HACKER_ID
  ,		HK.NAME
  FROM SUBMISSIONS SM
  INNER JOIN HACKERS HK		ON HK.HACKER_ID				= SM.HACKER_ID
  INNER JOIN CHALLENGES CH 	ON CH.CHALLENGE_ID 			= SM.CHALLENGE_ID
  INNER JOIN DIFFICULTY DIFF	ON DIFF.DIFFICULTY_LEVEL 	= CH.DIFFICULTY_LEVEL
  WHERE DIFF.SCORE = SM.SCORE
  GROUP BY 	HK.HACKER_ID
  ,			HK.NAME
  HAVING COUNT(SM.SCORE) > 1
  ORDER BY COUNT(SM.SCORE) DESC , HK.HACKER_ID
  ```

  - **해설 :** 먼저, SUBMISSIONS 테이블을 기준으로 설정하고, 주어진 관계를 따라 HACKERS, CHALLENGES, 그리고 DIFFICULTY 테이블을 INNER JOIN 합니다. 이는 SUBMISSIONS 테이블에서 필요하지 않은 정보를 제거하기 위한 것입니다. 만점을 받은 해커들을 선별하기 위해, 난이도별 만점 점수와 SUBMISSIONS 테이블의 SCORE가 일치하는 데이터를 WHERE 절로 필터링합니다. 이후, 만점을 받은 챌린지의 수를 계산하기 위해 GROUP BY와 HAVING 절을 사용하여, 만점을 받은 챌린지가 2개 이상인 해커들만을 추려냅니다. 마지막으로, 같은 수의 만점을 받은 해커들의 경우, 해커 ID에 따라 오름차순으로 정렬하여 결과를 출력합니다.
