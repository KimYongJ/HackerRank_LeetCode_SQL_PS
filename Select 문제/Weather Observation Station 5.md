- **Weather Observation Station 5**
  - [https://www.hackerrank.com/challenges/weather-observation-station-5/problem?isFullScreen=true](https://www.hackerrank.com/challenges/weather-observation-station-5/problem?isFullScreen=true)
  - **문제 :** STATION 테이블에서 가장 짧은 도시 이름과 가장 긴 도시 이름을 가진 두 도시를 출력하는 문제이며, CITY 컬럼 출력시 그 오른쪽에 CITY컬럼의 길이를 각각 조회합니다. 가장 작거나 큰 CITY 컬럼이 여러개일 경우 알파벳 순으로 가장 먼저 오는 도시 하나를 선택하면 됩니다.
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE STATION (
      ID INT AUTO_INCREMENT PRIMARY KEY,
      CITY VARCHAR(21),
      STATE CHAR(2),
      LAT_N DECIMAL(8, 4),
      LONG_W DECIMAL(8, 4)
  );
  INSERT INTO STATION (CITY, STATE, LAT_N, LONG_W) VALUES
  ('DEF', 'ST', 0.0000, 0.0000),
  ('ABC', 'ST', 0.0000, 0.0000),
  ('PQRS', 'ST', 0.0000, 0.0000),
  ('QWEVQ', 'ST', 0.0000, 0.0000),
  ('W', 'ST', 0.0000, 0.0000),
  ('WQQWEXY', 'ST', 0.0000, 0.0000),
  ('DVAEY', 'ST', 0.0000, 0.0000),
  ('ZZZZZ', 'ST', 0.0000, 0.0000),
  ('REQY', 'ST', 0.0000, 0.0000),
  ('QWXY', 'ST', 0.0000, 0.0000);
  ```
  ```jsx
  [ 정답(1) ]
  SELECT CITY, LEN
  FROM(
  		SELECT	ROW_NUMBER() OVER(ORDER BY LENGTH(CITY) ASC, CITY) MAX_LEN
  		,		ROW_NUMBER() OVER(ORDER BY LENGTH(CITY) DESC, CITY) MIN_LEN
  		,		CITY
  		,		LENGTH(CITY) LEN
  		FROM STATION
  )TEMP
  WHERE MAX_LEN = 1 OR MIN_LEN = 1
  ```
  - **해설**
    - **ROW_NUMBER 함수 :** 해당 함수는 행의 번호를 붙여 줍니다. OVER 안에 정렬 조건을 적어 해당 조건에 따른 번호를 1 부터 ~N 번까지 붙여 줍니다. 이름이 가장 길거나 짧은 것이 1이 되게 하기 위해 LENGTH(CITY)함수에 ASC, DESC 키워드를 붙여 주었습니다. 또한 길거나 짧은 CITY 컬럼이 여러개 일 때 알파벳을 기준으로 오름차순 정렬을 할 수 있도록 했습니다. 서브 쿼리 실행 결과는 아래 사진과 같습니다.
    - (사진1)
    - **출력 :** 출력은 서브쿼리에서 구한 MAX_LEN과 MIN_LEN이 각각 1인 것을 출력합니다.
  ```jsx
  [ 정답(2) ]
  SELECT CITY, LENGTH(CITY) LEN
  FROM station
  ORDER BY LENGTH(CITY) , CITY
  LIMIT 1;

  SELECT CITY, LENGTH(CITY) LEN
  FROM station
  ORDER BY LENGTH(CITY) DESC, CITY
  LIMIT 1;
  ```
  - **해설**
    - 이 문제는 각각의 쿼리 2개를 제출해도 정답으로 맞습니다. 첫 번째 쿼리는 가장 짧은 이름을 갖는 CITY를 출력하고 두번 째 쿼리는 가장 긴 이름을 갖는 CITY를 출력합니다.
