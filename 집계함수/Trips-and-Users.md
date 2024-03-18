# **Trips-and-Users**

- [https://leetcode.com/problems/trips-and-users/](https://leetcode.com/problems/trips-and-users/)
- **문제**
  - Trips 테이블에는 클라이언트 아이디와 드라이버 아이디가 있고, users 테이블에는 users_id와 차단여부, 클라이언트인지, 드라이버인지를 나타내는 role컬럼이 있습니다.
  - 각 날짜에 발생한 여행 요청의 취소율을 계산하는 것입니다. 취소율은 그날의 차단되지 않은 사용자들에 의한 취소된(클라이언트나 드라이버에 의한) 요청의 수를 그날의 차단되지 않은 사용자들의 전체 요청 수로 나누어 계산됩니다.
  - 날짜는 '2013-10-01' 부터 '2013-10-03' 사이에 매일 차단되지 않은 사용자들의 요청(클라이언트와 드라이버 모두 차단되면 안 됨) 으로 제한됩니다. trips 테이블 한 행에 클라이언트 아이디와 드라이버 아이디가 있으므로 둘다 차단되지 않아야 함에 유의하세요
  - 각 날짜의 취소율을 소수점 둘째 자리까지 반올림하여 표시합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Trips (
  id INT,
  client_id INT,
  driver_id INT,
  city_id INT,
  status VARCHAR(255),
  request_at DATE
);
CREATE TABLE Users (
  users_id INT,
  banned VARCHAR(255),
  role VARCHAR(255)
);

[ VERSION 1 ]
INSERT INTO Trips (id, client_id, driver_id, city_id, status, request_at) VALUES
(1, 1, 10, 1, 'completed', '2013-10-01'),
(2, 2, 11, 1, 'cancelled_by_driver', '2013-10-01'),
(3, 3, 12, 6, 'completed', '2013-10-01'),
(4, 4, 13, 6, 'cancelled_by_client', '2013-10-01'),
(5, 1, 10, 1, 'completed', '2013-10-02'),
(6, 2, 11, 6, 'completed', '2013-10-02'),
(7, 3, 12, 6, 'completed', '2013-10-02'),
(8, 2, 12, 12, 'completed', '2013-10-03'),
(9, 3, 10, 12, 'completed', '2013-10-03'),
(10, 4, 13, 12, 'cancelled_by_driver', '2013-10-03');
INSERT INTO Users (users_id, banned, role) VALUES
(1, 'No', 'client'),(2, 'Yes', 'client'),(3, 'No', 'client'),
(4, 'No', 'client'),(10, 'No', 'driver'),(11, 'No', 'driver'),
(12, 'No', 'driver'),(13, 'No', 'driver');

[ VERSION 2 ]
INSERT INTO Trips (id, client_id, driver_id, city_id, status, request_at) VALUES
(1, 1, 10, 1, "cancelled_by_client", "2013-10-04");
INSERT INTO Users (users_id, banned, role) VALUES
(1, 'No', 'client'),(10, 'No', 'driver');

[ VERSION 3 ]
INSERT INTO Trips (id, client_id, driver_id, city_id, status, request_at) VALUES
(1111, 1, 10, 1, "completed", "2013-10-01");
INSERT INTO Users (users_id, banned, role) VALUES
(1,'No','client'),(10, 'Yes', 'driver');
```

```jsx
[ 정답 ]
WITH TEMP AS(
	SELECT	REQUEST_AT
	,		COUNT(CASE WHEN STATUS='COMPLETED' THEN NULL ELSE 1 END) AS CANCEL
	,		COUNT(REQUEST_AT) AS TOTAL
	FROM TRIPS T
	INNER JOIN USERS U1 ON U1.USERS_ID = T.CLIENT_ID
	INNER JOIN USERS U2	ON U2.USERS_ID = T.DRIVER_ID
	WHERE	REQUEST_AT BETWEEN '2013-10-01' AND '2013-10-03'
	AND 	U1.BANNED = 'NO'
	AND 	U2.BANNED = 'NO'
	GROUP BY REQUEST_AT
)
SELECT	REQUEST_AT AS 'DAY'
,		ROUND(CANCEL / TOTAL , 2) AS 'CANCELLATION RATE'
FROM TEMP
```

- **해설**
  - TEMP 테이블
    - 여행 테이블의 드라이버와 클라이언트 모두 차단되지 않은 사람을 구하기 위해 USERS 테이블을 2번 조인합니다.
    - 문제 조건에서 여행일자를 2013-10-01 일부터 3일간으로 제한을 두었으므로 WHERE 조건에서 날자를 제한하고, 차단되지 않은 사용자를 조건에 추가합니다.
    - 취소건을 세기 위해 COUNT 함수안에 CASE WHEN으로 분기를 합니다. NULL을 반환하면 COUNT 함수는 숫자를 세지않습니다.
    - 총 요청건수는 날짜로 간단히 카운팅합니다.
  - 그 후 구해진 취소건과 총 요청건수를 나누고 소수점 3자리에서 반올림하여 답을 출력합니다.
