# **Friend-Requests-II:-Who-Has-the-Most-Friends**

- [https://leetcode.com/problems/friend-requests-ii-who-has-the-most-friends/](https://leetcode.com/problems/friend-requests-ii-who-has-the-most-friends/)
- **문제**
  - `RequestAccepted` 테이블에는 친구 요청을 보낸 사람의 ID(`requester_id`), 친구 요청을 수락한 사람의 ID(`accepter_id`), 그리고 요청이 수락된 날짜(`accept_date`)가 기록됩니다.
  - 요청을 보낸 사람과 요청을 수락한 사람의 조합은 테이블에서 고유해야 합니다.
  - 가장 많은 친구를 가진 사람과 그 사람의 친구 수를 찾아서 반환해야 합니다.
  - 테스트 케이스는 한 사람만이 가장 많은 친구를 가지도록 설정되어 있습니다.

```jsx
[ 문제 조건 ]
CREATE TABLE RequestAccepted (
    requester_id INT,
    accepter_id INT,
    accept_date DATE,
    PRIMARY KEY (requester_id, accepter_id)
);
INSERT INTO RequestAccepted (requester_id, accepter_id, accept_date) VALUES
(1, 2, '2016-06-03'),(1, 3, '2016-06-08'),
(1, 4, '2016-06-08'),(2, 3, '2016-06-08'),
(3, 4, '2016-06-09');
```

```jsx
[ 정답 ]
SELECT	ID
,		SUM(CNT) NUM
FROM(
	SELECT	accepter_id AS ID
	,		COUNT(*) CNT
	FROM RequestAccepted
	GROUP BY accepter_id
	UNION ALL
	SELECT	requester_id AS ID
	,		COUNT(*) CNT
	FROM RequestAccepted
	GROUP BY requester_id
)TEMP
GROUP BY ID
ORDER BY NUM DESC
LIMIT 1
```

- **해설**
  - 가장 많은 친구를 보유했다는 것은 요청을 가장 많이 보내고, 수락도 가장 많이 한 사람을 찾는 문제입니다. 이것을 간단히 해결하기 위해 요청 아이디 기준으로 그룹하여 수를 세고, 수락 아이디 기준으로 그룹하여 수를 세어 두 테이블의 결과를 UNION ALL을 통해 합쳐줍니다. 이 때 UNION으로 하게 되면 틀립니다. UNION은 두 테이블의 중복을 제거하기 때문에 같은 ID가 요청과 수락을 같은 횟수로 했다면 그 행은 없어지기 때문에 반드시 UINON ALL로 진행해야 합니다.
  - UNION ALL로 두 테이블을 합 친 후 ID기준으로 다시 그룹을 묶어 CNT의 값의 SUM을 구합니다.
  - 그리고 가장 많은 친구를 갖는 한 사람만 출력 해야하기 때문에 SUM의 결과를 기준으로 내림차순 정렬 후 LIMIT 키워드를 사용합니다.
