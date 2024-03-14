# **Confirmation-Rate**

- [https://leetcode.com/problems/confirmation-rate/](https://leetcode.com/problems/confirmation-rate/)
- **문제 :** 이 문제는 사용자의 확정 요청 메시지에 대한 확인 비율을 계산하는 문제입니다. CONFIRMED 메시지의 총 수를 해당 사용자의 요청된 모든 메시지의 수로 나눈 것 입니다. 출력은 소수점 3자리에서 반올림 후 2자리를 출력합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Signups (
    user_id INT,
    time_stamp DATETIME
);
CREATE TABLE Confirmations (
    user_id INT,
    time_stamp DATETIME,
    action ENUM('confirmed', 'timeout')
);
INSERT INTO Signups (user_id, time_stamp) VALUES
(3, '2020-08-21 10:16:39'),
(7, '2020-07-13 09:57:49'),
(2, '2020-01-25 23:59:59'),
(6, '2020-12-09 10:39:37');
INSERT INTO Confirmations (user_id, time_stamp, action) VALUES
(3, '2021-01-06 03:40:06', 'timeout'),
(3, '2021-04-08 04:08:46', 'timeout'),
(7, '2021-06-15 17:12:59', 'confirmed'),
(7, '2021-06-13 15:12:58', 'confirmed'),
(2, '2021-06-13 14:59:07', 'confirmed'),
(7, '2021-04-20 08:50:02', 'confirmed'),
(2, '2021-04-28 23:59:59', 'timeout'),
(1, '2021-06-28 23:59:59', 'timeout');
```

```jsx
[ 정답(1) ]
SELECT	S.USER_ID
,		ROUND(SUM(CASE WHEN C.ACTION='confirmed' THEN 1 ELSE 0 END) / COUNT(S.USER_ID),2) AS CONFIRMATION_RATE
FROM SIGNUPS S
LEFT OUTER JOIN CONFIRMATIONS C
	ON S.USER_ID = C.USER_ID
GROUP BY S.USER_ID
[ 정답(2) ]
SELECT	S.USER_ID
,		ROUND(count(CASE WHEN C.ACTION='confirmed' THEN 1 ELSE null END) / COUNT(S.USER_ID),2) AS CONFIRMATION_RATE
FROM SIGNUPS S
LEFT OUTER JOIN CONFIRMATIONS C
	ON S.USER_ID = C.USER_ID
GROUP BY S.USER_ID
```

- **정답(1) 해설 :** 두 테이블을 유저 아이디 기준으로 조인 후 기본 테이블인 SIGNUP 테이블의 유저 아이디로 그룹을 묶어줍니다. 그 후 confirmed 메시지의 합을 구하기 위해 sum 함수 안에 case when으로 조건 분기를 했습니다. 그리고 사용자의 총 메시지의 합을 구하기 위해 count 함수를 사용해 user_id의 수를 헤아린 후 나눠 주었습니다.
- **정답(2) 해설 :** 정답(1)과 내용은 같지만, confirmed 메시지의 수를 구하기 위해 count 함수를 사용했습니다. 그리고 confirmed가 아닐 때는 case when 구문을 통해 null을 반환하도록 만들어 카운팅되지 않도록 했습니다.
