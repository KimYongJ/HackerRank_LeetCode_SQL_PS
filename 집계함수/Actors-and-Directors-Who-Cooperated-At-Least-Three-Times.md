# **Actors-and-Directors-Who-Cooperated-At-Least-Three-Times**

- [https://leetcode.com/problems/actors-and-directors-who-cooperated-at-least-three-times/](https://leetcode.com/problems/actors-and-directors-who-cooperated-at-least-three-times/)
- **문제 :** ActorDirector 테이블에서 actor_id와 director_id를 찾는데, 3번이상 서로 협력한 적이 있다면 출력합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE ActorDirector (
  actor_id INT,
  director_id INT,
  timestamp INT,
  PRIMARY KEY (timestamp)
);

INSERT INTO ActorDirector (actor_id, director_id, timestamp) VALUES
(1, 1, 0),
(1, 1, 1),
(1, 1, 2),
(1, 2, 3),
(1, 2, 4),
(1, 1, 5),
(2, 1, 6);
```

```jsx
[ 정답 ]
SELECT  ACTOR_ID
,       DIRECTOR_ID
FROM ACTORDIRECTOR
GROUP BY ACTOR_ID, DIRECTOR_ID
HAVING COUNT(1) >= 3
```

- **해설 :** 배우 아이디와 디렉터 아이디로 그룹화한 후 3번이상 같은 값이 있다면 출력해주었습니다.
