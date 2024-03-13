# **Find-Followers-Count**

- [https://leetcode.com/problems/find-followers-count/](https://leetcode.com/problems/find-followers-count/)
- **문제 :** 각 사용자의 팔로워 수를 찾아야 합니다. USER_ID기준 오름차순 정렬 후 출력합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Followers (
    user_id INT,
    follower_id INT,
    PRIMARY KEY(user_id, follower_id)
);
INSERT INTO Followers (user_id, follower_id) VALUES
(0, 1),
(1, 0),
(2, 0),
(2, 1);
```

```jsx
[ 정답 ]
SELECT  USER_ID
,       COUNT(FOLLOWER_ID) FOLLOWERS_COUNT
FROM FOLLOWERS
GROUP BY USER_ID
ORDER BY USER_ID
```

- **해설 :** USER_ID로 그룹한 후 FOLLOWER_ID를 COUNT함수에 넣어 개수를 파악합니다.
