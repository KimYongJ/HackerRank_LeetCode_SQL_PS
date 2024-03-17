- **Game-Play-Analysis-I**

  - [https://leetcode.com/problems/game-play-analysis-i/](https://leetcode.com/problems/game-play-analysis-i/)
  - **문제 :** Activity 테이블에서 player_id 당 첫 로그인한 날짜를 찾습니다. 출력은 player_id와 event_date를 출력하는데 날짜 출력시 컬럼명을 first_login으로 합니다.

  ```jsx
  [ 문제 조건 ]
  CREATE TABLE Activity (
      player_id INT,
      device_id INT,
      event_date DATE,
      games_played INT,
      PRIMARY KEY (player_id, device_id, event_date)
  );

  INSERT INTO Activity (player_id, device_id, event_date, games_played) VALUES
  (1, 2, '2016-03-01', 5),
  (1, 2, '2016-05-02', 6),
  (2, 3, '2017-06-25', 1),
  (3, 1, '2016-03-02', 0),
  (3, 4, '2018-07-03', 5);
  ```

  ```jsx
  [ 정답 ]
  SELECT PLAYER_ID
  ,       MIN(EVENT_DATE) AS FIRST_LOGIN
  FROM ACTIVITY
  GROUP BY PLAYER_ID
  ```

  - **해설 :** 아이디를 기준으로 그룹으로 묶었을 때 가장 빠른 날짜, 즉 작은 날짜이기 때문에 MIN함수를 통해 작은 날짜를 불러옵니다.
