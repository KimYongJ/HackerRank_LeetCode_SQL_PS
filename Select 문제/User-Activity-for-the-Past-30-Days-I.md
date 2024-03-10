# **User-Activity-for-the-Past-30-Days-I**

- [https://leetcode.com/problems/user-activity-for-the-past-30-days-i/](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/)
- 문제 : 2019년 7월27을 포함해서 30일 전까지 웹 사이트 사용자의 수를 출력합니다. 날짜별로 사용자의 수를 출력하면됩니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Activity (
  user_id INT,
  session_id INT,
  activity_date DATE,
  activity_type ENUM('open_session', 'end_session', 'scroll_down', 'send_message')
);
INSERT INTO Activity (user_id, session_id, activity_date, activity_type) VALUES
(1, 1, '2019-07-20', 'open_session'),
(1, 1, '2019-07-20', 'scroll_down'),
(1, 1, '2019-07-20', 'end_session'),
(2, 4, '2019-07-21', 'send_message'),
(2, 4, '2019-07-21', 'open_session'),
(2, 4, '2019-07-21', 'end_session'),
(3, 2, '2019-07-21', 'open_session'),
(3, 2, '2019-07-21', 'send_message'),
(3, 2, '2019-07-21', 'end_session'),
(4, 3, '2019-06-25', 'open_session'),
(4, 3, '2019-06-25', 'end_session');
```

```jsx
[ 정답 ]
SELECT	ACTIVITY_DATE DAY
,		COUNT(DISTINCT USER_ID) ACTIVE_USERS
FROM ACTIVITY
WHERE ACTIVITY_DATE BETWEEN DATE_SUB('2019-07-27', INTERVAL 29 DAY) AND '2019-07-27'
GROUP BY ACTIVITY_DATE
```

- **해설 :** 먼저 원하는 날짜를 조회하기 위해 where 조건에서 2019-07-27 일자보다 29일 전을 구하고, 컬럼에 해당하는 날짜가 2019-07-27을 포함한 30일전 날짜 사이인지 체크합니다. 그 후 group by 를 통해 날짜를 기준으로 그룹화한 후 user_id를 카운팅합니다. 이 때 distinct 키워드를 사용해 중복된 사용자는 카운팅되지 않도록 합니다.
