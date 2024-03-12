# **Percentage-of-Users-Attended-a-Contest**

- [https://leetcode.com/problems/percentage-of-users-attended-a-contest/](https://leetcode.com/problems/percentage-of-users-attended-a-contest/)
- **문제 :** 각 경연 대회에 등록한 사용자의 비율을 계산하고, 비율을 기준으로 내림차순 출력하고, 값이 같으면 contest_id 기준으로 오름차순 출력합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Users (
    user_id INT,
    user_name VARCHAR(100)
);
CREATE TABLE Register (
    contest_id INT,
    user_id INT
);
INSERT INTO Users (user_id, user_name) VALUES
(6, 'Alice'),
(2, 'Bob'),
(7, 'Alex');
INSERT INTO Register (contest_id, user_id) VALUES
(215, 6),
(209, 2),
(208, 2),
(210, 6),
(208, 6),
(209, 7),
(209, 6),
(215, 7),
(208, 7),
(210, 2),
(207, 2),
(210, 7);
```

```jsx
[ 정답(1) ]
SELECT	CONTEST_ID
 ,		ROUND(COUNT(USER_ID) / MAX(TOTAL) *100,2) PERCENTAGE
FROM REGISTER R
CROSS JOIN (
			SELECT COUNT(*) TOTAL
			FROM USERS
)A
GROUP BY CONTEST_ID
ORDER BY PERCENTAGE DESC, CONTEST_ID

[ 정답(2) ]
SELECT	CONTEST_ID
 ,		ROUND(COUNT(USER_ID) / (SELECT COUNT(*) FROM USERS) *100,2) PERCENTAGE
FROM REGISTER R
GROUP BY CONTEST_ID
ORDER BY PERCENTAGE DESC, CONTEST_ID
```

- **정답(1) 해설 :** 등록한 유저들의 총 수를 구해야 하기 때문에 크로스 조인하면서 모든 유저들을 구해옵니다. 크로스 조인 후 테이블 상태는 아래 사진과 같습니다.
  사진(1)
  그 후 CONTEST_ID 기준으로 그룹을 지어, 각 경연대회에 등록한 사용자 수와 총 유저수를 나누고 100을 곱해 비율을 구해옵니다.
- **정답(2) 해설 :** 정답(1)의 서브쿼리를 select절로 올린것만 차이날 뿐 다른 것은 없습니다.
